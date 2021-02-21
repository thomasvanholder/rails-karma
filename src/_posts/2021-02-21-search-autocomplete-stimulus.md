---
layout: post
title: 'Search Autocomplete Stimulus'
date: 2021-02-20 10:11:58 +0000
categories: stimulus search
permalink: /search-autocomplete-stimulus
---

# {{ page.title }}

## Introduction

Learn how to set-up a search autocomplete with Stimulus. A user can see query results after typing in the input field. The [Stimulus Autocomplete library](https://github.com/afcapel/stimulus-autocomplete) is a pre-build Stimulus controller that provides an easy solution to auto-completion.

![autocomplete.gif](images/search-autocomplete.gif)

## Before you start

Make sure you have Stimulus installed. Check the package.json file or run `yarn why stimulus`. If Stimulus is not yet installed, follow the [documentation](https://stimulus.hotwire.dev/handbook/installing).

## 1. Install package

Add [stimulus autocomplete](https://github.com/afcapel/stimulus-autocomplete) to your project
{% highlight bash %}
yarn add stimulus-autocomplete
{% endhighlight %}

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
    <input type="text" class="w-full" data-autocomplete-target="input"
            placeholder='Type to search...'/>
    <ul data-autocomplete-target="results"></ul>
  </div>

</div>
{% endhighlight %}
Let's add a wrapper around to narrow the input field and search results.

- **data-controller="autocomplete"** scopes the imported controller to the div
- **data-autocomplete-url-value** sets the route to get the search results from
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
Layout false ensures that only plain HTML is returned. The header and metadata are not included. Precisely what is needed as the search results should display text only.

## 6. Create results view

{% highlight erb %}
<% @search_results.each do |result| %>

  <li role="option" ><%= result %></li>
<% end %>
{% endhighlight %}
Display the search results in a HTML view that matches the created route<br>_products/_autocomplete.html.erb_

## Conclusion

Stimulus proves it value by sprinkling JavaScript on the page, without the need for much custom JavaScript. Leverage pre-build components and suddenly developers can easily bring interactivity to HTML-dominant web applications.
