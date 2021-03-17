---
layout: post
title: 'Tailwind Custom Local and Google Fonts'
date: 2021-02-27 10:11:58 +0000
categories: tailwind
permalink: /tailwind-custom-local-fonts
navigation: ['1a. Import Google Fonts', '1b. Import local fonts', '2. Overwrite or Extend', '3. Apply styles']
featured_img: /images/font-import.png
---

# {{ page.title }}
{: .text-left}

Tailwind CSS offers developers powerful capabilities to build visually appealing websites in a very short time frame. To give your website a unique look and feel, you can choose to add new fonts to the Tailwind configuration.

The [default Tailwind classes](https://tailwindcss.com/docs/font-family) include 3 different fonts. Font-sans is the default font that will be applied even when you don't explicitley set the font-sans class. If you want to add more fonts to custom your website, Tailwind got your back too!

To use a different font you could either use an `@import` from Google fonts or when you can import the fonts locally into your project. For example, when Google Fonts does not have the specific font you are looking for.

- `font-sans` Rapidly build modern websites without ever leaving your HTML.
  {: .font-sans}

- `font-serif` Rapidly build modern websites without ever leaving your HTML.
  {: .font-serif}

- `font-mono` Rapidly build modern websites without ever leaving your HTML.
  {: .font-mono}

## 1a. Import Google Fonts

Visit [Google Fonts](https://fonts.google.com/) and search the specific font you like. Select the desired font weights from thin (100) upto bold (900). FCopy the import statement in between the style tags.

![font-import.png](images/font-import.png)
{: .w-96}

Import the new font in the css file where you import tailwind classes, i.e. styles.css. Note, it's important that your fonts are loaded at the top of the file.
{% highlight css %}
/* header font */
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700;800;900&display=swap');
/* body font */
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@100;300;400;500;700;900&display=swap');

@tailwind base;
@tailwind components;
@tailwind utilities;
{% endhighlight %}

## 1b. Import local fonts

To create something more unique, find an appealing font is not on Google Fonts, such as the handwritten [Barcelony](https://www.dafont.com/barcelony.font).

![barcelony.png](images/barcelony.png)
{: .w-96}
_image source: https://www.dafont.com/barcelony.font_
{: .text-gray-500 .font-light .text-sm}


Create a fonts folder in the assets pipeline (i.e. assets/fonts).
In the fonts folder add one of your custom font files, for example:
- `.ttf` for TryeType Fonts
- `.woff` for Web Open Format
- `.otf` for OpenType

With Rails the trick is to explicity load the newly created font folder into the application.<br>
In the `application.rb` file add:

{% highlight ruby %}
# load custom fonts in the asset pipeline
config.assets.paths << Rails.root.join("app", "assets", "fonts")
{% endhighlight %}

Make sure to restart the server.

Next, add the font to the bottom of the styles.css file.

{% highlight css %}
@layer base {
  @font-face {
    font-family: 'Barcelony';
    src: font-url('barcelony/Barcelony.ttf') format('truetype');
  }
}
{% endhighlight %}

- the __font-family__ value is what will be set into the Tailwind config file.
- _src_ is the path to where to local font can be found.

## 2. Overwrite or extend

You can either overwrite the [default Tailwind fonts](https://tailwindcss.com/docs/font-family).
Or you can extend and add your own. Using extend will add the newly specified font families without overriding Tailwind's entire font stack.

If your app is already built, it makes sense to overwrite the font so you save yourself the need to re-visit every paragraph element on your website to add the custom class.

In your tailwind.config.js file add the chosen font-family.

{% highlight javascript %}
module.exports = {
  purge: {...},
  theme: {
    extend: {...},
    fontFamily: {
      sans: ['Roboto', 'sans-serif'],
      heading: ['Poppins', 'sans-serif']
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

Font-sans is now using Roboto. As Font-sans is the default, it's not necessary to explicit include that class on an element. Additionaly a new font-heading class is added. As the font-heading class was non-existing, it will be created. You could also have chosen to add it within the extend curly bracets.

Font-heading is the newly added Poppins font for our heading/titles. To apply the Poppins font we can add to the base layer or include the class manually in the HTML where needed.

## 3. Apply styles

Apply styles globally.
In the file where you import the Tailwind classes add:

{% highlight css %}
@layer base {
  h1 {
    @apply font-heading;
  }
}
{% endhighlight %}

Any <h1> tag will now by default have the poppins font appliead. Be aware of order specificity. If you have add a font-class, i.e. font-mono, in the HTML on the h1 tag itself, font-mono will overwrite the global defined font-heading class.

Thanks for reading!
