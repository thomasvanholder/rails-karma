---
layout: post
title: 'Migrate Environment Variables (ENV) to Rails Credentials'
date: 2021-02-20 10:11:58 +0000
categories: stimulus lightgallery
permalink: /migrate-environment-variables-ENV-to-rails-credentials
navigation: ['Why Should You Move From ENV to Credentials?', 'How it Works', 'Migrate From ENV to Rails Credentials', 'How to Use Credentials in Multiple File Formats', 'How to Share Keys With a Team', 'Conclusion']
---

# {{ page.title }}
{: .text-left }

{{ page.date | date: "%b %d, %Y" }}
{: .italic .text-sm}

Rails credentials are the new gold standard. ENV files are an insecure ancestor. In this article, you’ll learn why and how to migrate, how to use API keys in Ruby, YML and js.erb, and how to share a single key once with your team.

> How to Migrate Environment Variables (ENV) to Rails Credentials

DHH tweeted about its arrival nearly three years ago, but new technology often takes time to catch up. A wake-up call is when you find yourself too frequently juggling API keys between developers in your team. It might be time to take a second look at how to implement credentials in a rails app.

<div class="flex justify-center">
<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Rails 5.2.0 final is out the door! Just in time for <a href="https://twitter.com/railsconf?ref_src=twsrc%5Etfw">@railsconf</a> ❤️. Please enjoy Active Storage, Redis Cache Store, HTTP/2 Early Hints, CSP, Credentials, and more! <a href="https://t.co/z4VWJTclhc">https://t.co/z4VWJTclhc</a></p>&mdash; DHH (@dhh) <a href="https://twitter.com/dhh/status/983452583368019968?ref_src=twsrc%5Etfw">April 9, 2018</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
</div>

## Why Should You Move From ENV to Credentials?

The further a project gets in its development cycle, the more services are integrated. Every external service has its API key. It usually doesn’t take too long before developers start hunting teammates for the latest API key. How annoying!

Or, just imagine when an API key gets refreshed. Every developer individually has to update it into local dotenv files. That seems anti-automation and anti-programmatic — and it is.

Stop throwing API keys through Slack or email and avoid a security breach of your keys. Luckily, rails credentials offer an easy and welcoming successor. Uploading your keys to Github.

Uploading to Github!? 😱 <br>
Yes, uploading to Github! A small annotation is that the API keys are fully encrypted.

The big win is that there is only a single key to share with your team. It never changes! Any new API keys added by your fellow developers as rails credentials are pulled from Github as you pull the latest main (prev. master).

You can find the key in the **config/master.key** folder.

## How it Works

Running `bin/rails credentials:edit` in rails creates two files needed in the config folder:

- **credentials.yml.enc** stores all your API keys. In case you were wondering, the .enc extension signifies encryption.
- **master.key** is the key use to decrypt the encrypted.file (1.) Make sure to check the inclusion of the **master.key** in your **.gitignore.yml** file.

**Credentials.yml.enc** is safe and secure sent along with your repository to Github. The master key, however, is never sent along — guard it like your life depends on it!

## Migrate From ENV to Rails Credentials

Open the credentials file in your terminal.<br>
`EDITOR='code --wait' bin/rails credentials:edit`

Depending on the editor you currently use, replace code (VS Code). For example:

- vim or vi= Vim
- atom = Atom
- subl or stt = Sublime

The credentials file automatically opens in the editor and waits to for you to update and close the file again. Migrate the ENV keys you are using in the .env file to the credentials.yml file.

Turn your legacy .ENV file:

{% highlight env %}
STRIPE_PUBLISHABLE_KEY=pk_test_VG8LlUN82DcZS3cAOJVy0WyIR9Jwz0YZkq302MKc00t
STRIPE_SECRET_KEY=sk_test_VG8LlUN82DcZS3cAOJVy0WyIR9Jwz0YZkq302MKc00tgAAYF
STRIPE_WEBHOOK_SECRET_KEY=whsec_cZpB0VG8cZpB0VG8cZpB0VG8UrgA2gcZpB0VG8cZpB
CLOUDINARY_URL=cloudinary://15031853100444:XOr3XQ-DcZ4dBoan80@DcZ4Boan800U
GOOGLE_API_KEY=S3cAOJVy0WyS3cAOJVy0WyIR9AOJVy0WyIR92e
{% endhighlight %}

Into a credentials.yml:
{% highlight yml %}
stripe:
publishable_key: pk_test_VG8LlUN82DcZS3cAOJVy0WyIR9Jwz0YZkq302MKc00tgAAYF
secret_key: sk_test_VG8LlUN82DcZS3cAOJVy0WyIR9Jwz0YZkq302MKc00tgAAYF
web_hook_secret_key: whsec_cZpB0VG8cZpB0VG8cZpB0VG8UrgA2gcZpB0VG8cZpB

google_api_key: S3cAOJVy0WyS3cAOJVy0WyIR9AOJVy0WyIR92e

cloudinary:
cloud*name: abcdefg
api_key: 12345678910
api_secret: abc315-VG8Ll8VG8Ll8L
{% endhighlight %}
\_note: Cloudinary API key is split up as per documentation.*

You are now all set. View credentials can run in the terminal.<br>
Run `bin/rails credentials:show`.

It’s time now to say goodbye to that old .ENV file and delete it.

## How to Use Credentials in Multiple File Formats

### Ruby

{% highlight ruby %}
# nested key
Rails.application.credentials.stripe[:publishable_key]

# single key
Rails.application.credentials.google_api_key
{% endhighlight %}

### YML

{% highlight yml %}
cloudinary:
service: Cloudinary
api*key: <%= Rails.application.credentials.dig(:cloudinary, :api_key) %>
api_secret: <%= Rails.application.credentials.dig(:cloudinary, :api_secret) %>
{% endhighlight %}
\_Note: for Cloudinary an additional [**config/cloudinary.yml**](https://gist.github.com/thomasvanholder/6ee92715274ad993f080db15ed3dd177) file is needed*

### JavaScript

{% highlight javascript %}
// ruby code only possible with js.erb format
const abc = "<%= Rails.application.credentials.google_api_key %>"
{% endhighlight %}

### HTML

{% highlight erb %}

<!-- interpolate in script tag -->
<script src="https://maps.googleapis.com/maps/api/js?key=<%= Rails.application.credentials.google_api_key %>"</script>

{% endhighlight %}

## How to Share Keys With a Team

- Share the key in **master.key** with fellow developers to enable decryption.
- Each team member creates a **master.key** file locally in the config folder and pastes it in the shared key.

## Conclusion

Coding is more fun without the hassle of chasing the correct API keys. Your app is up-to-date with security best practices. Share a master key once and be free of tedious copy-pasting.

Thanks for reading!
