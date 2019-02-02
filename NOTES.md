---
title: scratchpad
---

# Scratchpad

This is the url of the current page:
<a href="{{site.url}}{{page.url}}">{{site.url}}{{page.url}}</a>

The site url is : {{site.url}}

The page url is : {{page.url}}

The date and time is : {{site.date}} and {{site.time}} and {{page.date}}

https://github.com/pages-themes/cayman

The Man on the Mountaintop Susan Trott (Holy Man Series : trilogy) Adapted by Libby Spurrier https://www.audible.com/pd/The-Man-on-the-Mountaintop-Audiobook/B075Y4SWJ8

Narrated by Stanley Tucci, Toby Jones and a cast of others https://www.amazon.com/Susan-Trott/e/B000APH1NE/

## testing 1

Hopefully a toc wil show up.

{% for post in site.posts %}
  <a href="{{ post.url }}">
    <h2>{{ post.title }}</h2>
    <p>{{ post.date | date_to_string }}</p>
  </a>
{% endfor %}

## testing 2

Take 2

{% for post in site.pages %}
  <a href="{{ post.url }}">
    <h2>{{ post.title }}</h2>
  </a>
{% endfor %}
