---
title: "Face Recognition"
layout: archive
permalink: categories/face_recognition
author_profile: true
types: posts
---

{% assign posts = site.categories['face_recognition']%}
{% for post in posts %}
  {% include archive-single.html type=page.entries_layout %}
{% endfor %}