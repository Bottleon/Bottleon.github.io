---
layout: single
title: "ORM에 관하여"
permalink: categories/orm
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories['orm'] %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}
