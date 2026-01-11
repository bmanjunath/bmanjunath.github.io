---
layout: home
title: Automation with Manjunath
---

Welcome to **Automation with Manjunath** — your go-to blog to learn **Playwright automation from zero to pro**.  

Here, you’ll find step-by-step tutorials, beginner guides, and real-world examples to get started with automation testing quickly.

---

## Latest Posts

{% for post in site.posts %}
- [{{ post.title }}]({{ post.url }}) — {{ post.date | date: "%b %d, %Y" }}
{% endfor %}
