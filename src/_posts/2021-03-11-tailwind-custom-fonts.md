---
layout: post
title: 'Tailwind Custom Fonts'
date: 2021-02-27 10:11:58 +0000
categories: tailwind
permalink: /tailwind-custom-fonts
navigation: ['1a. Import Google Fonts', '1b. Import local fonts', '2. Overwrite or Extend', '3. Apply styles']
featured_img: /images/font-import.png
---

# {{ page.title }}

Tailwind CSS offers developers powerful capabilities to build visually appealing websites in a very short time frame. The [default Tailwind classes](https://tailwindcss.com/docs/font-family) include 3 different fonts. Font-sans is the default font that will be applied even when you don't explicitley set the font-sans class. If you want to add more fonts to custom your website, Tailwind got your back too!

To use the different font you could either use an `@import` from Google fonts or when you can import the fonts locally into your project. For example, when Google Fonts does not have the specific font you are looking for.

- `font-sans` Rapidly build modern websites without ever leaving your HTML.
  {: .font-sans}

- `font-serif` Rapidly build modern websites without ever leaving your HTML.
  {: .font-serif}

- `font-mono` Rapidly build modern websites without ever leaving your HTML.
  {: .font-mono}

## 1a. Import Google Fonts

Visit [Google Fonts](https://fonts.google.com/) and search the specific font you like. Select the style variants from thin (100) to bold (900). Copy the import statement in between the style tags.

![font-import.png](images/font-import.png)gst
{: .w-96}

Import the font above css file where you import tailwind classes
{% highlight css %}
/* body font */
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@100;300;400;500;700;900&display=swap');

@tailwind base;
@tailwind components;
@tailwind utilities;
{% endhighlight %}

## 1b. Import local fonts

## Rails asset pipeline

First, make sure the font folder is loaded into the application. In the `application.rb` file add:

{% highlight ruby %}
# load custom fonts in the asset pipeline

config.assets.paths << Rails.root.join("app", "assets", "fonts")
{% endhighlight %}

{% highlight css %}
@layer base {
  @font-face {
    font-family: 'Barcelony';
    src: font-url('barcelony/Barcelony.ttf') format('truetype');
  }
}
{% endhighlight %}

[Stackoverflow](https://stackoverflow.com/questions/12849840/integrating-font-face-files-into-rails-asset-pipeline/12849881#12849881)

## 2. Overwrite or extend

You can either overwrite the [default Tailwind fonts](https://tailwindcss.com/docs/font-family).
Or you can extend and add your own.

Using extend will add the newly specified font families without overriding Tailwind's entire font stack.

If your app is already built, it makes sense to overwrite the font so you save yourself the need to re-visit every paragraph element on your website to add the custom class.

In your tailwind.config.js file add the chosen font-family.

{% highlight javascript %}
module.exports = {
  purge: {...},
  theme: {
    extend: {...},
    fontFamily: {
      sans: ['Roboto', 'sans-serif'],
      heading: ['Oswald', 'sans-serif']
    }
  }
  variants: {
    extend: {}
  },
  plugins: [
    require('@tailwindcss/typography'),
    require('@tailwindcss/forms'),
    require('@tailwindcss/aspect-ratio'),
  ]
}
{% endhighlight %}

Font-sans is now using Roboto. As Font-sans is the default, it's not necessary to explicit include that class on an element. Additionaly a new font-heading class is added which will manually be added to title elements.

Font-heading is the newly added Oswald font. To apply the font we can add to the base layer or include the class manually in the HTML where needed.

## 3. Apply styles

Apply a style globally.

tailwind.css
{% highlight css %}
@layer base {
  h1 {
    @apply text-green-500;
  }
}
{% endhighlight %}
Awesome Title
{: .text-green-500}

Any <h1> tag will now by default have the color of green.
Be aware of order specificity. If you have a color set in the HTML on the h1 tag itself, the newly set color will overwrite the global defined class.

{% highlight html %}

 <h1 class="text-red-500">NEW YEARS SALE</h1>
{% endhighlight %}
Awesome Title
{: .text-red-500}
The title will be red, not green.
