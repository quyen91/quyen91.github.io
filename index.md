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

<script type='text/javascript'>
  function caculateTime() {
    var today_in_number = new Date().getTime() / 1000
    var last_time = document.getElementsByClassName('remind-latest-post')[0].textContent
    distance = (parseInt(today_in_number) - parseInt(last_time))/60/60/24
    var distanceDiv = document.getElementsByClassName('remind-time')[0]
    distanceDiv.innerText = `${Math.round(distance)} days ago`
}
  window.onload = evt => {
    caculateTime()
  };
</script>


<div class="header-right" markdown='1'> 

## Active

{:.remind-latest-post.q-hidden}
{{ site.posts.first.date | date: '%s' }}


{:.remind-title}

{:.remind-time}
0 days ago


## Latest issues
{:.home-page-title}
<div class="latest-item" markdown="1">
{% for post in site.posts limit:3 %}
  - [{{ post.title }}]({{ post.url }})
{% endfor %}
</div>

</div>

## Issues
{:.home-page-title}

{% for category in site.categories %}
### {{ category[0] }}
{% for post in category[1] %}
  - [{{ post.title }}]({{ post.url }})
{% endfor %}
{% endfor %}
