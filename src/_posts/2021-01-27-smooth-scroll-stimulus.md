---
layout: post
title: "Smooth Scroll Stimulus"
date: 2021-02-27 10:11:58 +0000
categories: stimulus scroll
permalink: /smooth-scroll-stimulus
navigation:
  [
    'Before You Start',
    '1. Install the package',
    '2. Add Stimulus Scroll-To library',
    '3. Add sidebar',
    '4. Add content',
  ]
---

# {{ page.title }}

{: .text-left }

Learn how to set up a smooth scrolling with Ruby on Rails and [Stimulus Components](https://github.com/stimulus-components). This is a simple and clean way to enable users to slide to a different section of a page.

![smooth-scroll.gif](images/smooth-scroll.gif)
{: .flex .justify-center }
The article are snippets from the [Ruby on Rails wiki page](https://en.wikipedia.org/wiki/Ruby_on_Rails).
{: .text-sm}

## Before You Start

Make sure you have Stimulus installed. Check the package.json file or run `yarn why stimulus`. If Stimulus is not yet installed, follow the [documentation](https://stimulus.hotwire.dev/handbook/installing).

## 1. Install the package

Add [Stimulus ScrollTo](https://stimulus-components.netlify.app/docs/components/stimulus-scroll-to/) to your project
{% highlight bash %}
yarn add stimulus-scroll-to
{% endhighlight %}

## 2. Add Stimulus Scroll-To library

{% highlight javascript %}
import { Application } from "stimulus"
import ScrollTo from "stimulus-scroll-to"

const application = Application.start()
application.register("scroll-to", ScrollTo)
{% endhighlight %}

## 3. Add sidebar

![sidebar.gif](images/sidebar.png)
{: .h-auto .w-1/2 }

{% highlight erb %}
<div class="flex">
  <div class="w-1/5">
    <small class="pb-3 text-sm italic">click an link in the sidebar 👇</small>
    <ul class="sticky flex flex-col w-full h-auto p-2 space-y-4 bg-white border-4 border-gray-500 rounded-lg top-16">
      <li><%= link_to "Introduction", "#introduction", data: { controller: "scroll-to" } %></li>
      <li><%= link_to "Technical overview", "#technical_overview", data: { controller: "scroll-to" }%></li>
      <li><%= link_to "Philosophy & Design", "#philosophy_design", data: { controller: "scroll-to" }%></li>
      <li><%= link_to "Framework Structure", "#framework_structure", data: { controller: "scroll-to" }%></li>
      <li><%= link_to "Trademarks", "#trademarks", data: { controller: "scroll-to" }%></li>
    </ul>
  </div>

  <div class="w-4/5">
  </div>
</div>
{% endhighlight %}

- **data-controller="scroll-to"** scopes the imported controller to every link individually

The hashtag(#) in the link_to will look on the same page for a matching id:

#introduction -> id="introduction"
{: .bg-purple-100 .text-purple-700 .px-2 .max-w-max}

## 4. Add content

{% highlight erb %}
<div class="w-4/5">
  <article>
    <ul>
      <li>
        <p id="introduction">Introduction</p>
        <p>PARAGRAPH HERE</p>
      </li>
      <li>
        <p id="technical_overview">Technical Overview</p>
        <p>PARAGRAPH HERE</p>
      </li>
      ...
    </ul>
  </article>
</div>
{% endhighlight %}

Note that the code snippet above is a simplied, without Tailwind classes, in order to keep clean view.

That’s it, Smooth Scrolling is now functional!

Thanks for reading!
