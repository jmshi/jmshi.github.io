---
title: WordPress to Github Pages Migration
date: 2018-02-20T00:00:00+00:00
author: jmshi
layout: post
permalink: /migration/
image:
summary: 
categories: log
---

Migration project, which was planned long ago, finally started on Feb 20, 2018. The reason to switch is too obvious to even think about it. The basic process consists of

1. Export my [old WordPress site](http://jimingshi.us) into markdown documents and download necessary images and videos: achieved by using [Jekyll exporter](https://wordpress.org/plugins/jekyll-exporter/)

2. Create a local website with Jekyll: I need to sorted out the layout in ./_data/menu.yml (the so-called data-driven method) since my old site has a slightly complicated menu. 

3. Create a repo based on the local site, and synced with github.

4. Tweak the local site and push to remote when it's done. 

It took me a while to decide how to export WordPress site. I even tried pelican to import wordpress xml export but found unsatisfying result. Eventually, I picked Jekyll exporter, and together with locally installed Jekyll, they did a great job to recover most of my pages and posts. 

A few other things I have added:

1. Some preliminary layout and css format were borrowed and modified from [Steve's No-Good-Very-Bad theme](https://github.com/svmiller/steve-ngvb-jekyll-template). 

2. Add google analytics to track the traffic and Twitter cards to show image previews of a post in a tweet. 

To-Do:

1. tweak more of the outfit of the site

2. add comments functionality

3. implement categories and tags

4. fix the links in those imported pages/posts from old site
