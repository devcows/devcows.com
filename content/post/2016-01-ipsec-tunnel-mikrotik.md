---
title: "Create an IPsec tunnel between 2 Mikrotik routers and dynamic public IPs"
slug: "create-an-ipsec-tunnel-between-2-mikrotik-routers-and-dynamic-public-ips"
date: "2016-01-26"
tags:
  - "mikrotik"
  - "vpn"
  - "ipsec"
author: "ADRIAN"
image: "media/mikrotik_ipsec.png"
---

In this post we are going to create an IPsec VPN tunnel between two remote sites using Mikrotik routers with dynamic public IPs . By default, Mikrotik does not allow to use FQDN (domain names) to setup an IPsec tunnel, so we are going to create some scripts to update the IPsec configuration whenever the local or remote IPs change.

The network layout is as follows:

{{% img src="media/mikrotik-ipsec-1.png" alt="Mikrotik IPsec" baseurl="true" %}}

The first thing to take into account is that LAN addresses must be different between Site 1 and Site 2. In our example, Site 1 uses LAN 192.168.1.0/24, whereas Site 2 uses 192.168.2.0/24. You can replace these networks with the ones in your infrastructure.

Another thing to consider is if your routers are behind a NAT. In this case you will have to make sure to forward port 500 (UDP) to the Mikrotik router.

In order to configure the IPsec tunnel, we have to setup the proposal, the peer, and the policy. We are going to provide the commands to configure Site 1, so once you finish with the guide, start over reverting the source and destination LAN addresses to configure Site 2.

First, let’s create an IPsec proposal:

```
/ip ipsec proposal add name=proposal1 auth-algorithms=md5 enc-algorithms=3des pfs-group=modp1024 disabled=no
```

Now, let’s create the peer. Replace the “test” secret with whatever password you want to use. Leave the address as it is as we will update it later from a script.

```
/ip ipsec peer add address=10.0.0.2 port=500 auth-method=pre-shared-key secret=test send-initial-contact=yes nat-traversal=no proposal-check=obey hash-algorithm=md5 enc-algorithm=3des dh-group=modp1024 generate-policy=no comment="myIPsec"
```

And, finally, let’s create a policy that will identify interesting traffic that should go through the IPsec tunnel. Again, let’s leave the “sa-src-address” and “sa-dst-address” as shown.

```
/ip ipsec policy add action=encrypt disabled=no src-address=192.168.1.0/24 dst-address=192.168.2.0/24 level=require ipsec-protocols=esp protocol=all tunnel=yes sa-src-address=10.0.0.1 sa-dst-address=10.0.0.2 proposal=proposal1 comment="myIPsec"
```

The IPsec portion is now configured in Site 1. But we need to add a couple of NAT rules to accept the IPsec traffic.

The following NAT rule will allow us to reach IPs on the remote LAN from our local network. It is important that this rule is placed in the first position.

```
/ip firewall nat add chain=srcnat src-address=192.168.1.0/24 dst-address=192.168.2.0/24 place-before=0 action=accept comment="IPsec traffic NAT bypass"
```

Add also this rule If we do not already have a NAT rule to masquerade internal traffic.

```
/ip firewall nat add chain=srcnat src-address=192.168.1.0/24 place-before=1 action=masquerade comment="Masquerade internal network"
```

Now, we need to create an account in a dynamic DNS service that will allow the remote site to always find out the other site’s public IP. In this guide we are using the No-IP.com service and provide scripts to update the IP of No-IP hosts. You are free to use whatever dynamic DNS service you want.

Once you have created an account and a host for Site 1, go ahead and the following script to update the No-IP host and the IPsec policy in the event of an IP change.

The script source is located here: https://gist.github.com/adrianmo/e54fbcd2c9d3cce80260

It may be more convenient to create the script from the UI, whether it is the web UI or Winbox. Enable “read”, “write”, and “test” policies, paste the script in the source field and replace the variables within the “Script Settings” section with your information. If you have followed the guide, leave the “IPsecComment” variable as it is. Replace the “WANInter” with the WAN interface that has the public IP of Site 1.

{{% img src="media/mikrotik-ipsec-2.png" alt="Mikrotik IPsec" baseurl="true" %}}

You can run the script manually and check the logs to verify whether the No-IP host and the IPsec policy are updated successfully.

```
/log print
```

Now we need to create an scheduler to run the script every time period. We considered that a 10 minute interval is quite balanced, but you can adjust it to your particular needs.

```
/system scheduler add disabled=no interval=10m name=no-ip_ddns_scheduler on-event=”no-ip_ddns_update” policy=read,write,test start-date=jan/01/1970 start-time=00:00:01
```

At this point Site 1 No-IP host should update automatically whenever its public IP changes and will also update the IPsec policy accordingly. Now we need to update Site 2 public IP in the IPsec peer and policy configuration, so create a No-IP host for Site 2 if you don’t have it already. Do not worry about the IP that this host is resolving to, it will be updated in Site 2 when we repeat the steps on Site 2.

The script to update the IPsec peer and policy when Site 2 public IP changes can be found here: https://gist.github.com/adrianmo/92e305123b521b7a4400

Again, create a script from the UI and replace “RemoteNOIPHost” with the host name of Site 2.

{{% img src="media/mikrotik-ipsec-3.png" alt="Mikrotik IPsec" baseurl="true" %}}

You can run the script manually and check the logs to verify that the IPsec peer and policy are updated successfully. For testing purposes, you can manually modify the IP from the No-IP control panel and verify that the script updates the IPsec configuration with the new IP.

```
/log print
```

We are now done with the configuration on Site 1, so it is time to move to Site 2 and go through it again configuring the IPs in the reverse order.

If you feel so inclined, please let us know how it went and leave some feedback if you find it useful.
