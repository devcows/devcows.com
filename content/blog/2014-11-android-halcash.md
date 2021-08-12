---
title: "Hal-cash finder (Android)"
slug: "hal-cash-finder-android"
date: "2014-11-29"
tags:  
  - "android"
  - "google maps"
authors: [Guillermo Guerrero]
banner: "media/hal-cash.png"
---

Hal-cash finder searches terminal banks compatibles with [Hal-cash](http://www.halcash.com/es) method using Hal-cash API and render in Google Maps. This application is a hello world using Google Maps.


## Description

Hal-cash finder is an application that searches terminal banks compatibles with Hal-cash method nearest your position.

With this application, you can do:
- **With your position**: the application searches terminal banks automatically nearest your position.
- **With an address**: you can put an address and the application finds terminal banks nearest.
- **With finger**: you can hold down the map and the application searches nearest terminal banks.

[GOOGLE PLAY](https://play.google.com/store/apps/details?id=com.devcows.hal_cash_finder&amp;hl=es)


## Images

Main screen:
{{% img class="img-responsive center-block" src="media/hal-cash1.png" alt="" baseurl="true" style="height: 200px;" %}}

Lateral menu:
{{% img class="img-responsive center-block" src="media/hal-cash2.png" alt="" baseurl="true" style="height: 200px;" %}}

Searching ATMs:
{{% img class="img-responsive center-block" src="media/hal-cash3.png" alt="" baseurl="true" style="height: 200px;" %}}

Searching ATMs:
{{% img class="img-responsive center-block" src="media/hal-cash4.png" alt="" baseurl="true" style="height: 200px;" %}}

ATMs options:
{{% img class="img-responsive center-block" src="media/hal-cash5.png" alt="" baseurl="true" style="height: 200px;" %}}		

Auto complete search box:
{{% img class="img-responsive center-block" src="media/hal-cash6.png" alt="" baseurl="true" style="height: 200px;" %}}


## Demo

<iframe frameborder="0" height="450" id="ytplayer" src="http://www.youtube.com/embed/ULmzavHzv80" type="text/html" width="100%"></iframe>


## Remarks

This application uses libraries and implements different design patterns, for example:

- [Robospice](https://github.com/stephanenicolas/robospice): This library implements asynchronous network request. Parses the JSON response to java classes.  

- Design patterns: [Observer](https://en.wikipedia.org/wiki/Observer_pattern) and [Singleton](http://en.wikipedia.org/wiki/Singleton_pattern)
