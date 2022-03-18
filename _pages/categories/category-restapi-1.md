---
layout: single
title: "REST API"
permalink: categories/restapi
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories['restapi'] %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}
