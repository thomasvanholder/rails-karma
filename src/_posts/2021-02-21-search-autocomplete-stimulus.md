---
layout: post
title: 'Search Autocomplete Stimulus'
date: 2021-02-20 10:11:58 +0000
categories: stimulus
permalink: /search-autocomplete-stimulus
---

### Before You Start

Make sure you <span class="text-red-700">have Stimulus installed</span>. Check the package.json file or run ```yarn why stimulus```. If Stimulus is not yet installed, follow the documentation.

Rails users can watch a GoRails episode. When using webpack, it's as easy as running ```bin/rails webpacker:install:stimulus```.


### 1. Install package

Add [stimulus autocomplete](https://github.com/afcapel/stimulus-autocomplete) to your project
```batch
yarn add stimulus-autocomplete
```

A simple paragraph with an ID attribute.
{: .bg-red-100 .text.red-700}


### 2. Add basic HTML layout
```html
<div data-controller="autocomplete" data-autocomplete-url-value="/birds/search">
  <input type="text" data-autocomplete-target="input"/>
  <input type="hidden" name="bird_id" data-autocomplete-target="hidden"/>
  <ul class="list-group" data-autocomplete-target="results"></ul>
</div>
```

### 3. Create a partial to render results
```html
<li class="list-group-item" role="option" data-autocomplete-value="1">Blackbird</li>
<li class="list-group-item" role="option" data-autocomplete-value="2">Bluebird</li>
<li class="list-group-item" role="option" data-autocomplete-value="3">Mockingbird</li>
```

