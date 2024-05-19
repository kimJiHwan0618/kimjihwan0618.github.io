---
title: "Java"
layout: archive
permalink: tags/java
author_profile: true
sidebar_main: true
entries_layout: grid
classes: wide
---

{% assign posts = site.tags.java %} {% for post in posts %} {% include archive-single.html type=page.entries_layout
%} {% endfor %}
