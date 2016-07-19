---
title: "Update Deluge version on your Raspberry PI"
slug: "update-deluge-version-on-your-raspberry-pi"
date: "2015-06-15"
tags:
  - "deluge"
  - "raspberry pi"
author: Adrian Moreno
banner: "media/raspberry-pi.png"
---

Unfortunately, at the time of writing this post the latest version available from Raspbian repositories is 1.3.3. And you may not use other repositories since they will probably not provide packages for ARM devices such as the Raspberry PI.

There are different reasons for updating Deluge to the latest version. One of them is that 1.3.3 does not support Magnet links, which is a very common way of loading in torrents to the client. Another reason might be fix the “Connection Failed. Check logs for details” when trying to configure the Deluge downloader on CouchPotato. This error occurs because Deluge updated its secure transport protocol in one of the newest versions.

Uninstall any previous version of Deluge
---

If you already have a previous version of Deluge installed, uninstall it.

```
sudo apt-get remove deluged
sudo apt-get remove deluge-web
sudo apt-get autoremove
```

Download and install the newest Deluge version
---

First, let’s stop Deluge in case it is still running.

```
sudo service deluge-daemon stop
```

or

```
sudo /etc/init.d/deluge-daemon stop
```

Install a few dependencies needed to compile and run Deluge. Most of them will probably be already installed in your system.

```
sudo apt-get install python python-twisted python-twisted-web python-openssl python-simplejson python-setuptools intltool python-xdg python-chardet geoip-database python-libtorrent python-notify python-pygame python-glade2 librsvg2-common xdg-utils python-mako
```

```
sudo reboot
```

Create a folder where you will download Deluge on and cd into it.

```
mkdir deluge
cd deluge/
```

Now download the latest version of Deluge from their website. At the time of writing the latest version was 1.3.11, but you can check for the a newer version here and update the URL from the following commands.

```
wget http://download.deluge-torrent.org/source/deluge-1.3.11.tar.bz2
tar xvf deluge-1.3.11.tar.bz2
cd deluge-1.3.11/
```

Let’s clean the build (just in case) and compile it.

```
python setup.py clean -a
python setup.py build
```

Now we can install the new version of Deluge.

```
sudo python setup.py install
sudo python setup.py install_data
```

And delete the files we have downloaded and extracted since they are no longer needed.

```
cd ../..
sudo rm -Rf deluge/
```

Verify that the new Deluge version is working fine.

```
deluged
deluge-web
```

Go to `http://[raspberry_IP]:8112/` and verify that you can see the Deluge web interface.

Configure Deluge to autostart on boot
---

Verify that you already have the following config file at `/etc/default/deluge-daemon` with the content below or create it if you don’t have it.

```
sudo nano /etc/default/deluge-daemon
```

And the content.

```
# Configuration for /etc/init.d/deluge-daemon

# The init.d script will only run if this variable is not empty.
DELUGED_USER="pi"

# Should we run at startup?
RUN_AT_STARTUP="YES"
```

You must also have the script to run the Deluge daemon and web UI as a Linux service. Let’s verify you have it there.

```
sudo nano /etc/init.d/deluge-daemon
```

If you don’t have it just download it into `/etc/init.d/`:

```
sudo wget -O /etc/init.d/deluge-daemon http://cdn5.howtogeek.com/wp-content/uploads/gg/up/sshot5151aa042ad11.txt
```

Fix the permissions of the init script.

```
sudo chmod 755 /etc/init.d/deluge-daemon
```

And update the RC.

```
sudo update-rc.d deluge-daemon defaults
```

Create the directories to keep the logs from the Deluge daemon and the web UI.

```
sudo mkdir -p /var/log/deluge/daemon
sudo mkdir /var/log/deluge/web
```

And give it permission to the pi user.

```
sudo chmod -R 755 /var/log/deluge
sudo chown -R pi:pi /var/log/deluge
```

Edit the init script to modify a few lines.

```
sudo nano /etc/init.d/deluge-daemon
```

Replace `DAEMON1`, `DAEMON1_ARGS`, `DAEMON2`, and `DAEMON2_ARGS` variables by these ones.

```
DAEMON1=/usr/local/bin/deluged
DAEMON1_ARGS="-d -L warning -l /var/log/deluge/daemon/warning.log"
DAEMON2=/usr/local/bin/deluge-web
DAEMON2_ARGS="-L warning -l /var/log/deluge/web/warning.log"
```

Restart the service.

```
sudo service deluge-daemon restart
```

Let’s set a logrotate rule to handle the Deluge logs.

```
sudo nano /etc/logrotate.d/deluge
```

And set the following content.

```
/var/log/deluge/*/*.log {
weekly
missingok
rotate 7
compress
notifempty
copytruncate
create 600
}
```

Make the Deluge web UI to automatically connect to the daemon

To do that, we just need modify the config file of the web UI. But first, let’s stop the daemon.

```
sudo service deluge-daemon stop
```

Now, open the config file.

```
sudo nano /root/.config/deluge/web.conf
nano ~/.config/deluge/web.conf
```

And replace this line.

```
“default_daemon”: “”,
```

By this one.

```
“default_daemon”: “127.0.0.1:58846″,
```

The Deluge web interface will now automatically connect to the daemon.

Create a Deluge username and password to allow access to other apps
---

You may have other applications such as CouchPotato that integrate with Deluge to automatically load in Torrent files. To allow access to Deluge from external applications, you have to specify a username and password.

First, let’s set the proper permissions to the directories and files.

```
sudo chmod 770 ~/.config/
sudo chmod 770 ~/.config/deluge
sudo chmod 660 ~/.config/deluge/auth
```

And now append a new user and password to the auth file. Replace `username` and `password` with whatever values you want.

```
echo username:password:10 >> ~/.config/deluge/auth
```

Now let’s restart the daemon for the change to take effect.

```
sudo service deluge-daemon restart
```

If you feel so inclined, please let us know how it went and leave some feedback if you find it useful.
