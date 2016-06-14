---
title: "Meteodino monitoring temperature system"
slug: "arduino-meteodino-temperature"
date: "2014-12-31"
tags:
  - "meteodino"
  - "arduino"
  - "temperature"
  - "humidity"
author: "GUILLERMO"
---

A monitoring system for temperature and humidity. The system is composed by a gadget with sensors and a server to store the data. This project combines [Ruby on rails](http://en.wikipedia.org/wiki/Ruby_on_Rails), [AngularJS](http://en.wikipedia.org/wiki/AngularJS), [Coffescript](http://coffeescript.org) and [Arduino](http://en.wikipedia.org/wiki/Arduino).

<div class="carousel slide" id="myCarousel">
	<ol class="carousel-indicators">
		<li class="active" data-slide-to="0" data-target="#myCarousel"></li>
		<li data-slide-to="1" data-target="#myCarousel"></li>
	</ol>

	<div class="carousel-inner">
		<div class="item active">
      {{% img class="img-responsive center-block" src="media/content_meteodino_1.jpg" alt="Meteodino1" baseurl="true" style="height: 400px;" %}}			
		</div>

		<div class="item">
      {{% img class="img-responsive center-block" src="media/content_meteodino_2.png" alt="Meteodino2" baseurl="true" style="height: 400px;" %}}			
		</div>
	</div>
	<a class="left carousel-control" data-slide="prev" href="#myCarousel" role="button"><span class="sr-only">Previous</span> </a> <a class="right carousel-control" data-slide="next" href="#myCarousel" role="button"> <span class="sr-only">Next</span> </a>
</div>

## Description

## Server

- API REST.
- Frontend with [AngularJS](http://en.wikipedia.org/wiki/AngularJS).

## Temperature gadget => Arduino

- Arduino Uno: [Link Dx](http://www.dx.com/p/uno-r3-atmega328p-uno-r3-development-board-deep-blue-285620#.VMk3V17F9TA)
- Arduino Ethernet Shield: [Link Dx](http://www.dx.com/p/ethernet-shield-v1-1-for-arduino-66908#.VMk3Tl7F9TA)
- Temperature sensor (DHT-11): [Link Dx](http://www.dx.com/p/arduino-digital-temperature-humidity-sensor-module-121350#.VMk3UV7F9TA) (Shit, very imprecise)
- Temperature sensor (DHT-22): [Link Dx](http://www.dx.com/p/arduino-dht11-digital-temperature-humidity-sensor-138531)
- LCD 16x2: [Link Dx](http://www.dx.com/p/16-x-2-character-lcd-display-module-with-blue-backlight-121356#.VMk3c17F9TA)

## Temperature gadget => Raspberry pi (coming soon)

- Raspberry pi
- Temperature sensor (DHT-11): [Link Dx](http://www.dx.com/p/arduino-digital-temperature-humidity-sensor-module-121350#.VMk3UV7F9TA) (Shit, very imprecise)
- Temperature sensor (DHT-22): [Link Dx](http://www.dx.com/p/arduino-dht11-digital-temperature-humidity-sensor-138531)
- LCD 16x2: [Link Dx](http://www.dx.com/p/16-x-2-character-lcd-display-module-with-blue-backlight-121356#.VMk3c17F9TA)

Demo at: [meteodino.guerreroibarra.com](http://meteodino.guerreroibarra.com)

## Remarks

The web page is developed with [Ruby on Rails](http://en.wikipedia.org/wiki/Ruby_on_Rails) and [Bootstrap](http://getbootstrap.com). The web uses some interesting gems, we will explain some:

- [Active Admin](http://activeadmin.info) generates a complete backoffice for manage the web site.
- [Did you mean](https://github.com/yuki24/did_you_mean)
- [Annotate](https://github.com/ctran/annotate_models) add a comment summarizing the current schema to the top or bottom of each of your models.
- [Rails erd](https://github.com/voormedia/rails-erd) generates a class diagram.
- [Rubocop](https://github.com/bbatsov/rubocop) is a Ruby static code analyzer. Out of the box it will enforce many of the guidelines outlined in the community Ruby Style Guide.

[GO TO REPOSITORY](https://bitbucket.org/devcows/meteodino)
