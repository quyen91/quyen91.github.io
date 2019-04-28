---
# You don't need to edit this file, it's empty on purpose.
# Edit theme's home layout instead if you wanna make some changes
# See: https://jekyllrb.com/docs/themes/#overriding-theme-defaults
layout: home
---
<!--
<script type='text/javascript'>
  window.onload = evt => {
    var colors = {
      rails: '#F2B400',
      github: '#9966CC'
    }
    console.log(colors['rails'])
    var items = ['#F2B400', '#9966CC', '#A4C639', '#89CFF0', '#B0BF1A', '#C9FFE5']
    document.querySelectorAll('.img-thumb').forEach(function(element) {
      var item = items[Math.floor(Math.random()*items.length)];
      element.style.background = item
    });
  };
</script> -->

<!-- <div class="top-post">
  <ul>
    {% for post in site.posts %}
      <li>
        <span class="entry-date"><time datetime="{{ post.date | date_to_xmlschema }}" itemprop="datePublished">{{ post.date | date_to_string }} --- </time></span>
        <a class='post-title' href="{{ post.url }}">{{ post.title }}</a>
      </li>
    {% endfor %}
  </ul>
</div> -->
## ===> Last time I create issues
{:.remind-title}
{% assign today = site.time | date: '%s' %}
{% assign start = site.posts.first.date | date: '%s' %}
{% assign secondsSince = today | minus: start %}
{% assign hoursSince = secondsSince | divided_by: 60 | divided_by: 60     %}
{% assign daysSince = hoursSince | divided_by: 24  %}

{{daysSince}} days ago
{:.remind-time}


## ===> Latest issues
{:.home-page-title}
{% for post in site.posts limit:3 %}
  - [{{ post.title }}]({{ post.url }})
{% endfor %}


## ===> Issues
{:.home-page-title}

{% for category in site.categories %}
### {{ category[0] }}
{% for post in category[1] %}
  - [{{ post.title }}]({{ post.url }})
{% endfor %}
{% endfor %}
