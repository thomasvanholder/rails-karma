---
layout: page
title: Posts
permalink: /posts/
---
![font-import.png](/images/carousel.gif)


<div class="grid grid-cols-1 gap-12 md:grid-cols-2 xl:grid-cols-3">
  {% for post in site.posts %}
  {{ "carousel.gif" | asset_url | img_tag: 'featured img' }}

    <div class="m-auto overflow-hidden rounded-lg shadow-lg cursor-pointer h-90 w-60 md:w-80">
      <a href="{{ post.url }}" class="block w-full h-full">
        <img alt="blog photo" src={{ title_content }} class="object-cover w-full max-h-40"/>
        <div class="w-full p-4 bg-white dark:bg-gray-800">
            <p class="font-medium text-indigo-500 text-md">
                Article
            </p>
            <p class="mb-2 text-xl font-medium text-gray-800 dark:text-white">
                {{ post.title }}
            </p>
        </div>
      </a>
    </div>
  {% endfor %}
 </div>

