
> 🚀 Welcome to **Automation with Manjunath**!  
> Learn **Playwright automation from zero to pro** with step-by-step tutorials, beginner guides, and real-world examples.

---

## Latest Posts

{% for post in site.posts %}
- [{{ post.title }}]({{ post.url }}) — {{ post.date | date: "%b %d, %Y" }}
{% endfor %}
