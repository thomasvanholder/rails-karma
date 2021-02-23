---
layout: page
title: Posts
permalink: /posts/
---

<ul class="mt-10 space-y-5 text-center ">
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}"  class="font-serif text-2xl font-semibold text-gray-800" >{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
