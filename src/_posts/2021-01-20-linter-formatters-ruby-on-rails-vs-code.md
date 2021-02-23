---
layout: post
title: 'Set Up Linters and Formatters for VS Code'
date: 2021-02-20 10:11:58 +0000
categories: vscode tools
permalink: /rubocop-stylelint-standard-markdownlint-vs-code
---

# {{ page.title }}
{:  .text-left }

With the right tools, any developer can enjoy deeply satisfying coding sessions. Mastering flow is empowering. The opposite leads to frustration and annoyance. Luckily, linters and formatters can help do the heavy lifting when it comes to coding best practices.

In the guide below, VS Code users and Ruby on Rails developers can find a detailed setup to build well-formatted and styled projects in no time!

- JavaScript — StandardJS (w Prettier)
- CSS and SCSS — Stylelint
- Ruby — Rubocop and Rubocop Rails
- Markdown — Markdownlint

## First, what is the difference between a linter and a formatter?

A linter checks code for best practices and code quality. It checks for both programmatic as well as stylistic errors. It’s like an advanced spell checker (e.g. Grammarly) for programming languages. A formatter shines in applying a consistent format everywhere (like tabs and spaces). Linters can be used as formatters, but they might not always be the best at that. It depends. For JavaScript files, using Standard as the linter and Prettier as the formatter is an excellent combo. For Ruby, Rubocop has both great formatting as well as linting capabilities.

A linter can be executed by a terminal command. On top of that, it can be integrated into an editor (e.g. VS Code). You can unleash advanced formatting and styling skills without ever leaving your development env. This article will help you to set up both. No more endless searching around to install the right package or to find the right formatting rules. Below is an installation guide from A to Z.

## 1. JavaScript Standard Style

[Standard](https://standardjs.com/) is a popular opinionated JavaScript formatter. Forget about creating complex setup files or a list of exceptions. Follow the best practices and spend more time coding instead of formatting! Standard is thoughtful with no configuration (like .eslint) to help automatically format JS code.

### 1.1 Install StandardJS:

- Yarn user? → `yarn add standard`
- NPM user? → `npm install standard`

### 1.2 Formatting

- Run `standard` in your terminal to view style offenses
- Run `standard --fix` to automatically fix all the found offenses.

### 1.3 Integrate into VS Code

![standard-vscode.png](images/standard-vscode.png)

Open the __settings.json__ file and disable the default JavaScript default built-in validation.

Note: Mac users can open the __setting.json__ file with <br>
 `Cmd + Shift + P` and selecting “__Preferences: Open Settings (JSON)__”.

{% highlight json %}
"javascript.validate.enable": false
{% endhighlight %}

You can now simply let StandardJS take care of formatting a JavaScript file with <br>
`Cmd + Shift + P` and selecting “__JavaScript Standard Style: Fix all auto-fixable problems__”.

### 1.4 ES7 for Javascript Standard style

Some developers like to use experimental JavaScript features (ES7 syntax). Standard might show a couple of style offenses that can be solved by adding babel-eslint as a dependency. For example:

_Parsing error. Unexpected token =._
{: .bg-red-100 .text-red-700 .max-w-max .px-2 }

### 1.5 Add babel-eslint as a dependency:

- Yarn user? → `yarn add babel-eslint --dev`
- NPM user? → `npm install eslint babel-eslint --save-dev`

### 1.6 Formatting

- Run `standard --parser babel-eslint` to lint all files.
- Run `standard --parser babel-eslint --fix` to automatically fix all the found offenses.

In order to get rid of the same error in VS Code, install ESLint and set "eslint.enable": true in the settings.json file.

### 1.7 Prettier and Standard in VS Code
![prettier-standard.png](images/prettier-standard.png)

If you are using Prettier as your formatter, you can install the Prettier-Standard package. Prettier takes care of the visual formatting. Standard serves as a linter to help guide you on best practices while writing JavaScript.

## 2. Rubocop and Rubocop Rails

Rubocop implements most of the [Ruby style guide](https://rubystyle.guide/) out of the box. [Check the configuration options](https://github.com/rubocop-hq/rubocop/blob/master/config/default.yml) and enable or disable certain rules by overwriting in .__rubocop.yml__. If you’d like Rubocop to flag Rails best practices and coding conventions, you can add that in as well. [Check the Rails best practices](https://docs.rubocop.org/rubocop-rails/cops_rails.html).

### 2.1 Add to the gem file:

{% highlight ruby %}
group :development, :test do
  gem 'rubocop', require: false
  gem 'rubocop-rails', require: false
end
{% endhighlight %}

### 2.2 Install

Run `bundle install` in your terminal. Add rubo-rails to the top of the __.rubocop.yml__ file. Note: The .rubocop.yml file is located at the level of your repository. If it’s not there, create one yourself [example](https://gist.github.com/jhass/a5ae80d87f18e53e7b56).

{% highlight yml %}
require:

- rubocop-rails
{% endhighlight %}

### 2.3 Formatting

Run `rubocop --auto-correct-all` or the shorter `rubocop -a` to auto-correct all (safe) offenses.

Some offenses can’t be auto-corrected, as they would change the semantics of the code too much. In that case, Rubocop will list the offenses and you can go and review them manually.

## 3. Stylelint

A [modern CSS linter](https://stylelint.io/) that helps you enforce consistent conventions and avoid errors in stylesheets. Typos, errors, and proactive feedback display as you are editing CSS and SCSS files. [Check the formatting rules here](https://stylelint.io/user-guide/rules/list).

### 3.1 Install Stylelint:

- Yarn user? → `yarn add stylelint stylelint-config-standard --dev`
- NPM user? → `npm install stylelint stylelint-config-standard --save-dev`

### 3.2 Create __.stylelintrc.json__

in top lovel of repository.
{% highlight json %}
{
  "extends": "stylelint-config-standard"
}
{% endhighlight %}

### 3.3 Formatting

- To style .css files, run `stylelint "**/\*.css"`.
- To style .scss files, run `stylelint "**/\*.scss"`.

### 3.4 Integrate into VS Code

![stylelint.png](images/stylelint.png)


Avoid flagging the same issues twice. Make it work nicely together with Tailwind. Add this into the settings.json file of VS Code:
{% highlight json %}
"css.validate": false,
"less.validate": false,
"scss.validate": false
{% endhighlight %}

Manually fix the flagged errors or let Stylelint auto-fix all offenses:<br>
`Cmd + Shift + P` while selecting “__stylelint: Fix all auto-fixable Problems__”.

## 4. Markdownlint

Markdown is one of the most common languages to help developers turn plain text into styled documents. For a short guide on how to use markdown, check this[cheat sheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet).

### 4.1 Install Markdownlint:

- Yarn user? → `yarn add markdownlint --dev`
- NPM user? → `npm install markdownlint --save-dev`

### 4.2 Formatting

- Run `markdownlint README.md` to style check the README file.
- Run `markdownlint -f README.md` to fix the found offenses in a specific file.
- Run `markdownlint \*_/_.md --ignore node_modules` to lint all markdown files if multiple are present in the repository (excluding markdown files from external libraries).

### 4.3 Integrate into VS Code

![markdownlint](images/markdownlint.png)

Once installed, markdown rules are auto-compiled when a markdown (.md) file is opened in VS Code (e.g. README.md). You can manually make the changes to remove the style conflicts. For a complete overview of the linter’s rules: check the [Markdowlint repo](https://github.com/DavidAnson/markdownlint/blob/main/doc/Rules.md) on GitHub.

![markdown_errors](images/markdown_errors.png)

Upon opening a markdown file in VS Code, a small search icon appears on the top right. After clicking the icon, a new tab opens with a side-by-side preview of your markdown code. The changes are reflected in real-time as you edit.
![live_preview_markdown](images/live_preview_markdown.gif)

