---
layout: defaults/page
permalink: index.html
narrow: true
---

{% include components/intro.md %}

[More about Tengfei Tu.]({{ site.baseurl}}{% link _pages/about.md %})

<hr/>

<div class="card mb-2">
    <img class="card-img-top" src="{{ site.baseurl }}/theme/img/Spring-Lion.jpg"/>
    <div class="card-body bg-light">
        <div class="card-text">A picture from Penn State University.</div>
    </div>
</div>

### Recent Posts

{% for post in site.posts limit:3 %}
{% include components/post-card.html %}
{% endfor %}

{% include bars/copyright.html %}
