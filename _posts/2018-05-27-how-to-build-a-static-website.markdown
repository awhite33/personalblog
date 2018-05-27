---
layout: post
title:  "How to Build a Static Website"
date:   2018-05-27 21:01:22 +1000
categories: tutorials
---

With so many easy website creators out there (Wordpress, Squarespace, Wix etc), why would anyone want to build their own website? The short answer: for greater control over the site, for a lower price, and to learn how the web works.

In this tutorial I will go through the process of building a static [Jekyll](https://jekyllrb.com/) site, from installing all the necessary tools to editing pages and ways to get it online.

#### Setting up your environment
I have always been a Windows OS fan, but have been jealous of the power (and prestige) of the unix shell. Luckily, Microsoft have now brought out [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10) where you can access the full power of your favourite linux distro from within Windows. I chose [Ubuntu](https://www.microsoft.com/en-au/store/p/ubuntu/9nblggh4msv6), and will be using the shell commands for the rest of the tutorial.

#### Installing Jekyll & Prerequisites
Jekyll has [several requirements](https://jekyllrb.com/docs/installation/) that we will be installing first.

We will need [Ruby](https://www.ruby-lang.org/en/downloads/), which you can check if it is installed by running:

```shell
ruby -v
# ruby 2.3.1p112 (2016-04-26) [x86_64-linux-gnu]
```

If you don't get a version number then install Ruby through:
```shell
sudo apt-get install ruby-full
```

Repeat the same process for:
- RubyGems
```shell
gem -v
# 2.5.2.1
# If not installed then
sudo apt-get install gem
```
- GCC/G++
```shell
gcc -v
# gcc version 5.4.0 20160609
# If not installed then
sudo apt-get install gcc
```

- Make
```shell
make -v
# GNU Make 4.1
# If not installed then
sudo apt-get install make
```

And now we're ready to install Jekyll!
```shell
gem install bundler jekyll
```

#### Creating your Jekyll Site
Now that everything is ready to go, creating a Jekyll site is easy. First navigate into the parent directory of where your site data will be. Then run
```shell
# Insert whatever <site-name> you like
jekyll new <my-site-name>
```
The code will run for a few moments as it creates all the necessary files. Then
when it is complete you can build and serve your new website by running
```shell
bundle exec jekyll serve
```
Visit your locally-hosted website by going to http://127.0.0.1:4000/ in your browser. How easy was that!

#### Making it Yours
One of the brilliant things about Jekyll is the many different themes that can be easily installed. By default, Jekyll ships with the *Minima* theme. The first thing we will do is update the configuration file `_config.yml` file with your settings. In popular templates such as *Minima*, `_config.yml` is well commented. This makes it easy to go through updating the appropriate fields in your favourite code editor (I use [Atom](https://atom.io/)) with your:
```yaml
title: Your awesome title
email: your-email@example.com
description:
  Write an awesome description for your new site here. You can edit this
  line in _config.yml. It will appear in your document head meta (for
  # Google search results) and in your feed.xml site description.
baseurl: "" # the subpath of your site, e.g. /blog
url: "" # the base hostname & protocol for your site, e.g. http://example.com
twitter_username: jekyllrb
github_username:  jekyll
```

You will need to re-serve the site (`bundle exec jekyll serve`) to see changes in the `_config.yml` file. Then voila: a customised site! We're making progress!

The next thing we'll do is update our *About* page, so that people can find out more about our us and our site. But before we do, it is probably a good time to learn a bit more about how Jekyll works...

#### Jekyll 101
As I mentioned before, Jekyll is a static site generator. This means that it takes a combination of template files and content files and combines them into a single cohesive site. If we were to make a static site without Jekyll (or another generator), any time we wanted to make a change to a page we would have to edit the HTML code directly in each of the pages that would be affected - imagine how tedious this would be for sites with hundreds or thousands of pages!

Instead, Jekyll uses HTML pages with dynamic elements ([liquid templates](https://shopify.github.io/liquid/)) to keep pages consistent and easily updateable across your site. Creating content only requires creating/editing markdown pages and making sure that they are named and located correctly.

[Markdown](https://daringfireball.net/projects/markdown/) is a simple text markup language that can be read in plain text or rendered as HTML. For example, this **bolded** word in markup is written as `**bolded**` and the heading above was written as `#### Jekyll 101`.

After exploring how markdown works we are ready to personalise our About page. Feel free to change it however you like, as long as it still contains the header material:

```yaml
---
layout: page  # Tells Jekyll to use 'page.html' as the template
title: About  # The displayed title of your page
permalink: /about/  # The link to this page, relative to site root
---
```
Once you've saved the page, you can rebuild your site and see the difference In case you need a refresher:

```shell
bundle exec jekyll serve
```

Now that you're familiar with writing in markdown, you are on track on easily create content for your entire site.

#### Creating a Post
Posts in Jekyll are different to Pages. The About file we edited was a `page`, which means that it appears in the navigation bar and has a folder of its own. What we are going to create now is a blog `post`, which will form the core of most content-focused websites.

You can get an idea of what a post file contains by looking at the example post already in the `_posts` directory. It has a specific naming convention of `YYYY-MM-DD-name-of-post.markdown`, as well as some extra fields in the header:

```yaml
---
layout: post  # Again, which HTML layout Jekyll will use
title:  "Welcome to Jekyll!"  # Title of the post
date:   2018-05-26 21:23:38 +1000 # Timestamp of the post
categories: jekyll update # What the post is about
---
```

The easiest way to create a new post is to:
1. Duplicate an existing post in the `_posts` directory
2. Rename the file (keeping the convention above)
3. Adjust the header with the correct info
4. Delete the content and start writing!

#### Getting it Online
Now that you've made a website, updated your About page and learnt to publish blog posts, it's time to put it online! One of the easiest (and free) ways to do this is with [GitHub Pages](https://pages.github.com/) which also supports Jekyll. There are an emormous range of hosting providers available. I'm currently (May 2018) using [Google Firebase](https://firebase.google.com/) because of its low (currently free) cost and my keenness for the Google ecosystem.

Get keen for a future tutorial where I will go through the steps of purchasing a domain and hosting your site online!
