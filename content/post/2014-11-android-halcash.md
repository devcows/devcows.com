---
title: "Hal-cash finder (Android)"
slug: "hal-cash-finder-android"
date: "2014-11-29"
tags:  
  - "android"
  - "google maps"
author: "GUILLERMO"
image: "media/hal-cash.png"
---

Hal-cash finder searches terminal banks compatibles with [Hal-cash](http://www.halcash.com/es) method using Hal-cash API and render in Google Maps.

<div class="carousel slide" id="myCarousel">
	<ol class="carousel-indicators">
		<li class="active" data-slide-to="0" data-target="#myCarousel"></li>
		<li data-slide-to="1" data-target="#myCarousel"></li>
		<li data-slide-to="2" data-target="#myCarousel"></li>
		<li data-slide-to="3" data-target="#myCarousel"></li>
		<li data-slide-to="4" data-target="#myCarousel"></li>
		<li data-slide-to="5" data-target="#myCarousel"></li>
	</ol>

	<div class="carousel-inner">
		<div class="item active">
			<img class="img-responsive center-block" src="/ckeditor_assets/pictures/15/content_picture_1.png" style="height: 400px;">
		</div>

		<div class="item">
			<img class="img-responsive center-block" src="/ckeditor_assets/pictures/12/content_picture_2.png" style="height: 400px;">
		</div>

		<div class="item">
			<img class="img-responsive center-block" src="/ckeditor_assets/pictures/14/content_picture_3.png" style="height: 400px;">
		</div>

		<div class="item">
			<img class="img-responsive center-block" src="/ckeditor_assets/pictures/13/content_picture_4.png" style="height: 400px;">
		</div>

		<div class="item">
			<img class="img-responsive center-block" src="/ckeditor_assets/pictures/11/content_picture_5.png" style="height: 400px;">
		</div>

		<div class="item">
			<img class="img-responsive center-block" src="/ckeditor_assets/pictures/10/content_picture_6.png" style="height: 400px;">
		</div>
	</div>
	<a class="left carousel-control" data-slide="prev" href="#myCarousel" role="button"><span class="sr-only">Previous</span> </a> <a class="right carousel-control" data-slide="next" href="#myCarousel" role="button"> <span class="sr-only">Next</span> </a>
</div>

## Description

Hal-cash finder is an application that searches terminal banks compatibles with Hal-cash method nearest your position.

With this application, you can do:
- **With your position**: the application searches terminal banks automatically nearest your position.
- **With an address**: you can put an address and the application finds terminal banks nearest.
- **With finger**: you can hold down the map and the application searches nearest terminal banks.

[GOOGLE PLAY](https://play.google.com/store/apps/details?id=com.devcows.hal_cash_finder&amp;hl=es)


<iframe frameborder="0" height="450" id="ytplayer" src="http://www.youtube.com/embed/ULmzavHzv80" type="text/html" width="100%"></iframe>

## Remarks

This application uses libraries and implements different design patterns, for example:

- [Robospice](https://github.com/stephanenicolas/robospice): This library implements asynchronous network request. Parses the JSON response to java classes.  

- Design patterns: [Observer](https://en.wikipedia.org/wiki/Observer_pattern) and [Singleton](http://en.wikipedia.org/wiki/Singleton_pattern)
