---
layout: post
title:  "Typography: a small widow prevention function"
date:   2016-11-16 22:20:00 -0800
---

Just a small function to insert a non-breaking space into a string. And this is what it prevents:

![widow example](http://www.shauninman.com/assets/images/widowed.gif "This is what it prevents")

{% highlight javascript %}
function widont(heading) {
  let i = heading.lastIndexOf(' ')
  if (i < 0) { return heading }

  let beginning = heading.substr(0, i)
  let end = heading.substr(i + 1, heading.length - i + 1)
  return beginning + '\u00a0' + end
}
{% endhighlight %}
