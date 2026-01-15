## Playwright Series

{% for post in site.posts %}
{% if post.title contains "Playwright" %}
- [{{ post.title }}]({{ post.url }}) — {{ post.date | date: "%b %d, %Y" }}
{% endif %}
{% endfor %}
