---
layout: post
title: 'Build a Carousel with Stimulus'
date: 2021-02-20 10:11:58 +0000
categories: stimulus carousel
permalink: /build-a-carousel-stimulus
navigation: ['Before you start', '1. Install the package', '2. Add the Stimulus Carousel library', '3. Import stylesheets', '4. Add basic HTML layout', '5. Add CSS and content', '6. Add pagination and buttons', 'Adding More Functionality', 'Conclusion' ]
---

# {{ page.title }}
{: .whitespace-nowrap .text-left }

Learn how to set up a modern carousel with Ruby on Rails and [Stimulus Components](https://github.com/stimulus-components). This is a powerful and easy solution to build a fancy carousel into your project without writing any custom JavaScript. Check the [swiperjs demo page](https://swiperjs.com/demos) to get an idea of what you can build after reading this article.

![carousel.gif](images/carousel.gif)
{: .flex .justify-center }

## Before You Start

Make sure you have Stimulus installed. Check the package.json file or run `yarn why stimulus`. If Stimulus is not yet installed, follow the [documentation](https://stimulus.hotwire.dev/handbook/installing).

## 1. Install the package

Add [stimulus carousel](https://stimulus-components.netlify.app/docs/components/stimulus-carousel/) to your project
{% highlight bash %}
yarn add stimulus-lightbox
{% endhighlight %}

## 2. Add the Stimulus Carousel library

{% highlight javascript %}
import { Application } from "stimulus"
import Carousel from "stimulus-carousel"

const application = Application.start()
application.register("carousel", Carousel)
{% endhighlight %}

## 3. Import stylesheets

{% highlight javascript %}
// In your application.js (for example)
import 'swiper/swiper-bundle.min.css'

// Or in your application.scss file
@import "~swiper/swiper-bundle"
{% endhighlight %}

Choose one of the two. If you get a “file import not found” error, try <br>_@import “swiper/swiper-bundle”_.

## 4. Add basic HTML layout

{% highlight erb %}
<!-- Slider main container -->
<div data-controller="carousel" class="swiper-container">
  <!-- Additional required wrapper -->
  <div class="swiper-wrapper">
    <!-- Slides -->
    <div class="swiper-slide">Slide 1</div>
    <div class="swiper-slide">Slide 2</div>
    <div class="swiper-slide">Slide 3</div>
  </div>
</div>
{% endhighlight %}

Note the added __data-controller__ attribute on line 2. Stimulus uses the identifier (“carousel”) to link the HTML page to JS controller (it’s creating a new carousel controller instance). The carousel’s scope is between the opening div and the closing div.

## 5. Add CSS and content

The content of your slides (text, pictures, background) comes in the __swiper-slide div__. Or you can apply differentiated background styling.

{% highlight css %}
<style>
  .swiper-slide {
    height: 250px;
    display: flex;
    align-items:center;
    justify-content: center;
  }

  .pink {
    background-color: lightpink;
  }

  .green {
    background-color: lightgreen;
  }

  .blue {
    background-color: lightblue;
  }
</style>
{% endhighlight %}

## 6. Add pagination and buttons

{% highlight erb %}
<div data-controller="carousel" class="my-5 swiper-container w-25"
    data-carousel-options-value='{
    "pagination": { "el": ".swiper-pagination",
                    "dynamicBullets": "true" },
    "navigation": { "nextEl": ".swiper-button-next",
                    "prevEl": ".swiper-button-prev"}}'>
  ...
  <!-- Pagination (... or 1/10 or progress bar) -->
  <div class="swiper-pagination"></div>

  <!-- Navigation buttons (< >) -->
  <div class="swiper-button-prev"></div>
  <div class="swiper-button-next"></div>
</div>
{% endhighlight %}

- Swiper buttons allow users to tap navigation chevrons (__< >__).
- Swiper pagination displays the page like slide 1/10, … or a progress bar.
- __Data-carousel-options-value__ is a way to pass any functionality of the [chosen features](https://swiperjs.com/demos) as data attributes in the HTML.

If you like to avoid writing any data-carousel options in the HTML, you can choose to[ extend the functionality](https://stimulus-components.netlify.app/docs/components/stimulus-carousel/#-extending-controller) of the library and add your carousel options as default.

That’s it, your slider is ready!

![carousel.gif](images/carousel.gif)
{: .flex .justify-center }

## Adding More Functionality

![swiper-extra.gif](images/swiper.png)

It’s as simple as:

- Searching for the desired functionality from swiper.
- Inspecting the source code or viewing it on Stackblitz.
- Adding the options in the data-carousel-options-value attribute.

Note: Make sure to wrap every hash key in quotes and beware of redundant commas, as those might break the code.

## Conclusion

Coding is fun with the right tools at your fingertips. Stimulus Components is an excellent library to build a carousel. It offers exciting features without the need to write any JavaScript yourself!

Thanks for reading!
