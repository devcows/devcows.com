---
title: "Homemade ambilight with Arduino and Xbmc"
slug: "arduino-ambilight-xbmc"
date: "2016-01-15"
tags:
  - "ambilight"
  - "arduino"
  - "xbmc"
author: "GUILLERMO"
---

Homemade ambilight system for TV displays with Arduino and Xbmc.

## Images

<div class="carousel slide" id="myCarousel">
	<ol class="carousel-indicators">
		<li class="active" data-slide-to="0" data-target="#myCarousel"></li>
		<li data-slide-to="1" data-target="#myCarousel"></li>
		<li data-slide-to="2" data-target="#myCarousel"></li>
		<li data-slide-to="3" data-target="#myCarousel"></li>
	</ol>

	<div class="carousel-inner">
		<div class="item active">
      {{% img class="img-responsive center-block" src="media/content_ambilight1.png" alt="Ambilight1" baseurl="true" style="height: 400px;" %}}
		</div>

		<div class="item">
      {{% img class="img-responsive center-block" src="media/content_ambilight2.png" alt="Ambilight2" baseurl="true" style="height: 400px;" %}}
		</div>

		<div class="item">
      {{% img class="img-responsive center-block" src="media/content_ambilight3.png" alt="Ambilight3" baseurl="true" style="height: 400px;" %}}
		</div>

		<div class="item">
      {{% img class="img-responsive center-block" src="media/content_ambilight4.png" alt="Ambilight4" baseurl="true" style="height: 400px;" %}}
		</div>
	</div>
	<a class="left carousel-control" data-slide="prev" href="#myCarousel" role="button"><span class="sr-only">Previous</span> </a>
  <a class="right carousel-control" data-slide="next" href="#myCarousel" role="button"> <span class="sr-only">Next</span> </a>
</div>

## Demos

<p>
	<iframe frameborder="0" height="450" id="ytplayer" src="http://www.youtube.com/embed/QiZHNcrvsQw" type="text/html" width="100%"></iframe>
</p>

<p>
	<iframe frameborder="0" height="450" id="ytplayer" src="http://www.youtube.com/embed/eNhAsUhEIEE" type="text/html" width="100%"></iframe>
</p>

## Components

- 50 LEDS => 2 x [12mm Diffused Thin Digital RGB LED Pixels (Strand of 25) - WS2801]: [Link Ebay](http://www.ebay.es/itm/12mm-Round-5V-Digital-RGB-LED-Pixels-Strand-of-50-WS2801-Waterproof-IP65-/161453014817?pt=UK_Computing_Other_Computing_Networking&amp;hash=item2597597f21)
- Arduino uno: [Link Dx](http://www.dx.com/p/uno-r3-atmega328p-uno-r3-development-board-deep-blue-285620)
- Male + Female DC Power Converter Connector Adapters (Optional to connect leds): [Link Dx](http://www.dx.com/p/male-female-dc-power-converter-connector-adapters-w-terminal-blocks-for-cctv-camera-pair-105084#.VLwoWC7F9TA)
- 5V 2A Power Adapter Charger: [Link Dx](http://www.dx.com/p/5v-2a-power-adapter-charger-for-security-camera-scanner-black-5-5-x-2-1mm-eu-plug-159396#.VLwo2C7F9TA)

Total price approximately: 100€

## Connection schema

{{% img class="img-responsive center-block" src="media/content_ambilight_wiring-diagram.png" alt="Ambilight5" baseurl="true" style="height: 400px;" %}}

## Software

- [Xbmc](http://kodi.tv/download)
- [Boblight Xbmc](http://kodi.wiki/view/Add-on:XBMC_Boblight)
- [Boblight Service](https://code.google.com/p/boblight)
- [Arduino code](https://learn.adafruit.com/adalight-diy-ambient-tv-lighting/download-and-install)
- [Boblight config maker](http://www.tweaking4all.com/home-theatre/xbmc/boblight-config-maker)
