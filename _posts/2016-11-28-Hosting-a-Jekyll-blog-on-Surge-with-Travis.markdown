---
layout: post
title:  "Hosting a Jekyll Blog on Surge.sh with Travis integration via GitHub."
date:   2016-11-28 13:03:17 -0600
categories: notes
---

Rather than post to a static page, I decided to use Jekyll for this blog and then went about the various steps to
make the process as painless as possible for adding new posts. The process of configuring everything wasn't too bad,
but there were a fair number of steps.

First I had to install Ruby 'cause I didn't have a decently new version on my laptop. I installed it with rvm.

Then I had to install gems for bundler and Jekyll, so I did that following the instructions on the Jekyll
web site. `gem install jekyll bundler`

Then I spun up a Jekyll blog, using their handy dandy instructions `jekyll new my-awesome-site`

Then, I cd'd into the new directory that created and went into `_config.yml` to change my configuration, into `_posts`
to edit posts, edited `about.md` to fix up the about page, added a `.travis.yml` file in the hopes that it would just
magically work, created a GitHub repo, connected my directory to it, committed and pushed everything, and crossed my
fingers.

Apparently, crossing one's fingers remains an insufficient method for ensuring something will work.

I forgot to go into Travis CI and configure it to watch the repo, so I did that, and tried again.

This time Travis tried to build but I'd forgotten to setup my Surge Secret and ID within Travis, so I went into Travis
and found the settings for my repo, added in the Surge variables it needed. 

And, IT WORKED, well Travis told me it worked
but it didn't actually push my stuff up, so I weeded through the Travis logs and saw I had a couple things off
in my `.travis.yml` file, I fixed those, committed and pushed the change and "BAM" now I've got instant Jekyll
build and push to Surge.sh via Travis-CI, whenever I push changes to GitHub. Snazzy.

If anyone else needs a blueprint for how to replicate the process:

* fork [my repo](https://github.com/P1xt/p1xt-redpanda)
* install ruby on your machine
* `gem install jekyll bundler`
* clone your fork of my repo on your local machine
* run `jekyll serve` to see the blog running locally on your machine
* edit _config.yml, .travis.yml, about.md, CNAME, README.md, and the contents of the posts directory
* signup for Travis-CI and configure Travis to run for your repo [instructions here](https://surge.sh/help/integrating-with-travis-ci)
* presto-chango, now you just put a new file in the posts directory and commit/push the change to git and surge gets
updated.


