---
layout: post
title:  "Connect to globally available Nextcloud/ownCloud via LAN"
date:   2017-10-25 22:22:22 +0200
categories: script
tags:   nextcloud owncloud ubuntu
---
Having your Nextcloud/ownCloud instance available over the internet is a great thing. You can synchronize and access your files from all around the globe.

Using the desktop client to sync folders misses one feature though: If your server is available locally, you don't want your data to go the extra miles through the web.
This script is a workaround that did the job flawlessly for me. It automatically changes the IP address of the domain your server is available over the web.

In this file strings you should replace are surrounded by "<>"" (e.g. <IP>).

{% highlight bash %}
#! /bin/bash
ssid=$(iwgetid -r)

text="<local IP address of the server>    <domain of the server>"
placeholder="#justaplaceholder#"

infile="/etc/hosts"
tmpfile="/tmp/hosts"


if [ "$ssid" == "<SSID of your local WIFI>" ]
        then
                sed "s/$placeholder/$text/g" "$infile" > "$tmpfile"
        else
                sed "s/$text/$placeholder/g" "$infile" > "$tmpfile"
fi

mv "$tmpfile" "$infile"

{% endhighlight %}

Place this file in /etc/network/if-up.d and /etc/network/if-down.d to be executed when connecting or disconnecting to a network.
Tested with Ubuntu 16.04, it should work similarly on other Linux distributions though.
