---
title: "일상 이야기"
layout: archive
permalink: categories/life_story
author_profile: true
types: posts
---

{% assign posts = site.categories['life_story']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}
