---
layout: post
title: 'Search Autocomplete Stimulus'
date: 2021-02-20 10:11:58 +0000
categories: stimulus
permalink: /search-autocomplete-stimulus
---

# {{ page.title }}

## Before you start

Make sure you <span class="text-red-700">have Stimulus installed</span>. Check the package.json file or run `yarn why stimulus`. If Stimulus is not yet installed, follow the documentation.

Rails users can watch a GoRails episode. When using webpack, it's as easy as running `bin/rails webpacker:install:stimulus`.

## 1. Install package

Add [stimulus autocomplete](https://github.com/afcapel/stimulus-autocomplete) to your project
{% highlight bash %}
yarn add stimulus-autocomplete
{% endhighlight %}

A simple paragraph with an ID attribute.
{: .bg-red-100 .text.red-700 .px-2}

## 2. Add basic HTML layout

{% highlight html %}
<div data-controller="autocomplete" data-autocomplete-url-value="/birds/search">
  <input type="text" data-autocomplete-target="input"/>
  <input type="hidden" name="bird_id" data-autocomplete-target="hidden"/>
  <ul class="list-group" data-autocomplete-target="results"></ul>
</div>
{% endhighlight %}

## 3. Create a partial to render results

{% highlight css %}
.circle {
border-radius: 50%;
height: 50px;
width: 50px;
}
{% endhighlight %}

{% highlight ruby %}
def abc
puts "hello"
value = { }
appelsap = 23 + 'abc' + "#{interpolation}"
end
{% endhighlight %}

{% highlight javascript %}

import "index.css"

// Import all javascript files from src/\_components
const componentsContext = require.context("bridgetownComponents", true, /.js\$/)
componentsContext.keys().forEach(componentsContext)

console.info("Bridgetown is loaded!")
{% endhighlight %}
