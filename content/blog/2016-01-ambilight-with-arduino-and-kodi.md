---
title: "Homemade ambilight with Arduino and Kodi"
slug: "arduino-ambilight-xbmc"
date: "2016-01-15"
tags:
  - "ambilight"
  - "arduino"
  - "xbmc"
  - "kodi"
authors: [Guillermo Guerrero]
banner: "media/ambilight.jpg"
aliases:
  - "/blog/arduino-ambilight-kodi"
---

The Ambilight system is a gadget for TV to enjoy the TV shows. The system is composed by a concrete RGB LEDs (25 or 50 LEDs) and the LEDs reproduce the border color from TV. This post explains how create a homemade Ambilight system and connect to TV with [Kodi](http://kodi.tv).


## Components

- 50 LEDS => 2 x [12mm Diffused Thin Digital RGB LED Pixels (Strand of 25) - WS2801]: [Link Ebay](http://www.ebay.es/itm/12mm-Round-5V-Digital-RGB-LED-Pixels-Strand-of-50-WS2801-Waterproof-IP65-/161453014817?pt=UK_Computing_Other_Computing_Networking&amp;hash=item2597597f21)
- Arduino uno: [Link Dx](http://www.dx.com/p/uno-r3-atmega328p-uno-r3-development-board-deep-blue-285620)
- Male + Female DC Power Converter Connector Adapters (Optional to connect leds): [Link Dx](http://www.dx.com/p/male-female-dc-power-converter-connector-adapters-w-terminal-blocks-for-cctv-camera-pair-105084#.VLwoWC7F9TA)
- 5V 2A Power Adapter Charger: [Link Dx](http://www.dx.com/p/5v-2a-power-adapter-charger-for-security-camera-scanner-black-5-5-x-2-1mm-eu-plug-159396#.VLwo2C7F9TA)

Total price: 100€ (approximately)


## Connection_schema

{{% img class="img-responsive center-block" src="media/ambilight_wiring-diagram.png" alt="Ambilight5" baseurl="true" style="height: 400px;" %}}


## Making_of

<ol>
  <li>
    <p>
      Soldering the array of 25 LEDs in one. After test the array:<br />
      {{% img class="img-responsive center-block" src="media/ambilight1.png" alt="Ambilight1" baseurl="true" style="height: 400px;" %}}
    </p>
  </li>

  <li>
    <p>
      Prepare back LED support with TV shape (VESA and connectors). Fix LEDs in the support.<br />
      {{% img class="img-responsive center-block" src="media/ambilight2.png" alt="Ambilight2" baseurl="true" style="height: 400px;" %}}
    </p>
  </li>

  <li>
    <p>
      Install the LED support on TV back (VESA).<br />
      {{% img class="img-responsive center-block" src="media/ambilight3.png" alt="Ambilight3" baseurl="true" style="height: 400px;" %}}

      <br />
      <br />

      {{% img class="img-responsive center-block" src="media/ambilight4.png" alt="Ambilight4" baseurl="true" style="height: 400px;" %}}
    </p>
  </li>
</ol>


## Software

- [Kodi](http://kodi.tv/download)
- [Boblight Xbmc](http://kodi.wiki/view/Add-on:XBMC_Boblight)
- [Boblight Service](https://code.google.com/p/boblight)
- [Arduino code](https://learn.adafruit.com/adalight-diy-ambient-tv-lighting/download-and-install)
- [Boblight config maker](http://www.tweaking4all.com/home-theatre/xbmc/boblight-config-maker)


## Demos

Video 1:
<iframe frameborder="0" height="450" id="ytplayer" src="http://www.youtube.com/embed/QiZHNcrvsQw" type="text/html" width="100%"></iframe>

Video 2:
<iframe frameborder="0" height="450" id="ytplayer" src="http://www.youtube.com/embed/eNhAsUhEIEE" type="text/html" width="100%"></iframe>
