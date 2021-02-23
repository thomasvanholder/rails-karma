---
layout: post
title: 'Build a Lightgallery with Stimulus'
date: 2021-02-20 10:11:58 +0000
categories: stimulus lightgallery
permalink: /build-a-lightgallery-with-stimulus
---

# {{ page.title }}

In this article, you will learn how to set up a light gallery with Stimulus, a modest JavaScript framework for the HTML you already have. Stimulus is a powerful alternative to SPA’s and enables developers to bring web applications to life.

> Stimulus. A modest JavaScript framework for the HTML you already have.

[Stimulus Components](https://github.com/stimulus-components) is an open-source project that hosts a collection of customizable components for typical JavaScript behavior. One component helps you to create a feature-rich light gallery into your project without writing any custom JavaScript at all. See [lightgallery.js](https://sachinchoolur.github.io/lightgallery.js/) to get an idea of what you can build after reading this article.

Stimulus is back-end and framework agnostic. Use it with your preferred back-end framework of choice. In this tutorial, Ruby on Rails is the chosen back-end framework.

![autocomplete.gif](images/lightgallery.gif)
Demo: a light gallery for a pillow store. _Photos by Artem Podrez from Pexels_

## Before you start

Make sure you have Stimulus installed. Check the package.json file or run `yarn why stimulus`. If Stimulus is not yet installed, follow the [documentation](https://stimulus.hotwire.dev/handbook/installing).

## 1. Install the package
Add [stimulus lightbox](https://stimulus-components.netlify.app/docs/components/stimulus-lightbox/) to your project
{% highlight bash %}
yarn add stimulus-lightbox
{% endhighlight %}

## 2. Add the Stimulus Lightbox library

{% highlight javascript %}
import { Application } from "stimulus"
import Lightbox from "stimulus-lightbox"

const application = Application.start()
application.register("lightbox", Lightbox)
{% endhighlight %}
Add to the **index.js** file

## 3. Import stylesheets

{% highlight javascript %}
// In your application.js (for example)
import "lightgallery.js/dist/css/lightgallery.min.css"

// Or in your application.scss file
@import "lightgallery.js/src/sass/lightgallery"
{% endhighlight %}

## 4. Add basic HTML layout

The lightgallery.js library looks for a data-scr attribute. The rails image tage does not provide that by default. Manually add in a data-src attribute in the HTML.

{% highlight erb %}
<div data-controller="lightbox" class="images">
 <%= image_tag "pillow1",  data: { src: "../assets/pillow1.jpg" } %>
 <%= image_tag "pillow2",  data: { src: "../assets/pillow2.jpg" } %>
 <%= image_tag "pillow3",  data: { src: "../assets/pillow3.jpg" } %>
 <%= image_tag "pillow4",  data: { src: "../assets/pillow4.jpg" } %>
</div>
{% endhighlight %}

## 5. Add basic styling to the images

{% highlight css %}
<style>
 .images {
	display: flex;
	justify-content: center;
	margin-top: 25px;
 }

 img {
	height: 200px;
	width: 200px;
	margin: 10px;
	cursor: pointer;
 }
</style>
{% endhighlight %}

## 6. Add captions

Make the light-gallery descriptive by adding a small, informative text at the bottom of every image.

{% highlight erb %}
<div data-controller="lightbox" class="images">
 <%= image_tag "pillow1", data: { src: "../assets/pillow1.jpg",
								  sub_html: "A companion for other pillows." } %>
 <%= image_tag "pillow2", data: { src: "../assets/pillow2.jpg",
								  sub_html: "Always on duty." } %>
 <%= image_tag "pillow3", data: { src: "../assets/pillow3.jpg",
								  sub_html: "Easy to hold with 2 hands."} %>
 <%= image_tag "pillow4", data: { src: "../assets/pillow4.jpg",
								  sub_html: "Or twist when you feel like."} %>
</div
{% endhighlight %}


## 7. Add additional options

Enable additional features on the lightgallery. A full list of the options [here](https://sachinchoolur.github.io/lightgallery.js/docs/api.html#lg-thumbnail).

- i.e .visual navigation options
- i.e infinite loop

{% highlight erb %}
<div data-controller="lightbox"
     class="images"
     data-lightbox-options-value='{"controls": true, "loop":true}'>
	...
</div>
{% endhighlight %}


If you like to avoid writing any data-lightbox-options in the HTML, you can choose to extend the functionality library and add your lightgallery options as default.

That’s it, your lightgallery is ready!
![autocomplete.gif](images/lightgallery.gif)

## Conclusion

Stimulus proves it value by sprinkling JavaScript on the page, without the need the go full-blown SPA. Leverage pre-build components and suddenly developers can easily bring interactivity the HTML-dominant web applications.

Thanks for reading!
