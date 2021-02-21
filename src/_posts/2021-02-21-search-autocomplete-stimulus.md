---
layout: post
title: 'Search Autocomplete Stimulus'
date: 2021-02-20 10:11:58 +0000
categories: stimulus search
permalink: /search-autocomplete-stimulus
---

# {{ page.title }}

Learn how to set-up a search autocomplete. A user can see resuts after typing in the search field. The Stimulus Autocomplete library is a pre-bulid Stimulus controller that provides an easy solution to auto-completion.

## What we will build
![Alt Text](images/search-autocomplete.gif)

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

## 2. Import library

{% highlight javascript %}
import { Application } from 'stimulus'
import { Autocomplete } from 'stimulus-autocomplete'

const application = Application.start()
application.register('autocomplete', Autocomplete)
{% endhighlight %}
Add to the **index.js** file

## 3. Add basic HTML layout

{% highlight erb %}
<div class="max-w-xs mx-auto bg-white">

  <div data-controller="autocomplete" data-autocomplete-url-value="/autocomplete">
    <input type="text" class="w-full" data-autocomplete-target="input" placeholder='Type to search...'/>
    <ul data-autocomplete-target="results"></ul>
  </div>

</div>
{% endhighlight %}
Let's add a wrapper around to narrow the input field and search results.

- **data-controller="autocomplete"** scopes the imported controller to the div
- **data-autocomplete-url-value** sets the route to get the seach results from
- **data-autocomplete-target="input"** listens for a keyboard change and reads the input field
- **data-autocomplete-target="results"** is the wrapper to inject the result list items in

## 4. Create route

{% highlight ruby %}
get '/autocomplete', to: 'products#autocomplete'
{% endhighlight %}
Fetch the HTML search results that should be displayed at the user types

## 5. Create controller method

{% highlight ruby %}
def autocomplete
@search_results = ['apple', 'apple juice', 'apple compote']
render layout: false
end
{% endhighlight %}
Layout false ensures that only plain HTML is returned. The header and metadata are not included. This is exactly what we want as the search results should display text only.

## 6. Create results view

{% highlight erb %}
<% @search_results.each do |result| %>

  <li role="option" ><%= result %></li>
<% end %>
{% endhighlight %}
Display the search results in a HTML view that matches the created route<br>_products/_autocomplete.html.erb_
