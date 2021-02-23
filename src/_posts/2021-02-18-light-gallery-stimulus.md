---
layout: post
title: 'Build a Lightgallery with Stimulus'
date: 2021-02-20 10:11:58 +0000
categories: stimulus lightgallery
permalink: /build-a-lightgallery-with-stimulus
---

In this article, you will learn how to set up a light gallery with Stimulus, a modest JavaScript framework for the HTML you already have. Stimulus is a powerful alternative to SPA’s and enables developers to bring web applications to life.

> Stimulus. A modest JavaScript framework for the HTML you already have.

Stimulus Components is an open-source project that hosts a collection of customizable components for typical JavaScript behavior. One component helps you to create a feature-rich light gallery into your project without writing any custom JavaScript at all. See lightgallery.js to get an idea of what you can build after reading this article.

Stimulus is back-end and framework agnostic. Use it with your preferred back-end framework of choice. In this tutorial, Ruby on Rails is the chosen back-end framework.
What we will build

A light gallery for a pillow store.
Image for post
Image for post
Photos by Artem Podrez from Pexels
Before You Start

Make sure you have Stimulus installed. Check the package.json file or run yarn why stimulus. If Stimulus is not yet installed, follow the documentation.

Rails users can watch a GoRails episode. When using webpack, it's as easy as running rails webpacker:install:stimulus.
Create Your Lightgallery
1. Install the package

Run yarn add stimulus-lightbox in the terminal.
2. Add the Stimulus Lightbox library
3. Import stylesheets
4. Add basic HTML layout

The lightgallery.js library looks for a data-scr attribute. The rails image tage does not provide that by default. Manually add in a data-src attribute in the HTML.
5. Add basic styling to the images
6. Add captions

Make the light-gallery descriptive by adding a small, informative text at the bottom of every image.
7. Add additional options

Enable additional features on the lightgallery. A full list of the options here.

    i.e .visual navigation options
    i.e infinite loop

If you like to avoid writing any data-lightbox-options in the HTML, you can choose to extend the functionality library and add your lightgallery options as default.

That’s it, your lightgallery is ready!
Image for post
Image for post
Conclusion

Stimulus proves it value by sprinkling JavaScript on the page, without the need the go full-blown SPA. Leverage pre-build components and suddenly developers can easily bring interactivity the HTML-dominant web applications.

Thanks for reading!
