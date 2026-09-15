+++
title = "UI Showcase"
date = 2026-04-22
description = "A showcase of how different elements look like in zola-yolk theme."

[taxonomies]
tags = ["ui", "zola"]

[extra]
series = "Showcases"
series_part = 2
+++

A simple showcase of how different elements look like in the theme.

## Homepage

Demo : [/](/)
{% dmode() %}
{% border() %}
{{ img(src="/images/screenshots/home-dark.webp", alt="dark theme screenshot of home page", eager=true) }}
{% end %}
{% end %}

{% lmode() %}
{% border() %}
{{ img(src="/images/screenshots/home-light.webp", alt="light theme screenshot of home page", eager=true) }}
{% end %}
{% end %}

## Post page

Demo : [/posts/introduction/](/posts/introduction/)
{% dmode() %}
{% border() %}
{{ img(src="/images/screenshots/intro-dark.webp", alt="dark theme screenshot of a post page") }}
{% end %}
{% end %}

{% lmode() %}
{% border() %}
{{ img(src="/images/screenshots/intro-light.webp", alt="light theme screenshot of a post page") }}
{% end %}
{% end %}

## Posts listing

Demo : [/posts/](/posts/)
{% dmode() %}
{% border() %}
{{ img(src="/images/screenshots/posts-dark.webp", alt="dark theme screenshot of the posts listing") }}
{% end %}
{% end %}

{% lmode() %}
{% border() %}
{{ img(src="/images/screenshots/posts-light.webp", alt="light theme screenshot of the posts listing") }}
{% end %}
{% end %}

## Tags listing

Demo : [/tags/](/tags/)
{% dmode() %}
{% border() %}
{{ img(src="/images/screenshots/tags-dark.webp", alt="dark theme screenshot of the tags listing") }}
{% end %}
{% end %}

{% lmode() %}
{% border() %}
{{ img(src="/images/screenshots/tags-light.webp", alt="light theme screenshot of the tags listing") }}
{% end %}
{% end %}

