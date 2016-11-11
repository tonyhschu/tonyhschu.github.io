---
layout: post
title:  "A bash script to make a sqlite database from a CSV"
date:   2016-11-10 19:25:53 -0800
---

Also today I learned a ton about shell scripts because I wanted to have a
repeatable process for making a `sqlite` database.

TL:DR;

{% highlight bash %}
if [ -z "$1" ];
  then
    echo "No input csv specified"
    exit 1
fi

if [ -z "$2" ];
  then
    echo "No output location specified"
    exit 1
fi

if [ ! -f $1 ];
  then
    echo "Error: input csv ($1) does not exist"
    exit 1
fi

TABLENAME=$(basename $1 | cut -d. -f1 | sed 's/[-.]//g')
# `basename` is a command to get the base name from a path
# `cut` splits the string `-d` sets the delimiter `-f` gets the component
# `sed` does string manipulation, the stuff between '' is a regular expression

echo "Table Name will be: " $TABLENAME
echo "Starting sqlite..."

sqlite3<< EOF
.echo on
.mode csv

.import $1 $TABLENAME

.schema

.save $2

.exit
EOF

echo "Done"
exit 0
{% endhighlight %}

To run the shell script:

`$ bash create-sqlite-from-csv source.csv destination.db`
