---
layout: post
title:  "Compiling non-related things in a Makefile"
date:   2016-11-10 19:25:53 -0800
---

[Bostock wrote a post a while back about documenting a build process
using `make`.](https://bost.ocks.org/mike/make/) I applied it today to document a build process to [create
a `sqlite` file from a bunch of CSV]({{ site.github.url }}/2016/11/10/shell-script-create-sqlite.html).

The `makefile` looks like this:

{% highlight make %}
all: ./sql.db ./summary-stats.json

./sql.db: ./dataset-a.csv
  bash create-sqlite-from-csv.sh ./dataset-a.csv ./sql.db
  touch ./dist/data/sql.db

./summary-stats.json: ./dataset-a.csv
  node summarize.js ./dataset-a.csv
  touch ./summary-stats
{% endhighlight %}

`all` is helpful here because now I can put all of these rules in one file,
even if they are not necessarily related.
