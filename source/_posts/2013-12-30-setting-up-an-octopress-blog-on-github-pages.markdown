---
layout: post
title: "Setting up an octopress blog on github pages"
date: 2013-12-30 15:01:12 -0300
comments: true
categories: [Octopress, Blogging, Github]
---
Suppose you are already hosting your personal site in github pages with your user name, so when you go to http://yourusername.github.io, or http://yourcustomdomain.com if you had set up a custom domain, the page that gets renderer is your home page with your portfolio, social links and contact form. 

However you want to have your own personal blog hosted in github pages too but this time pointing to http://yourcustomdomain/blog so let's configure octopress in order to have that.

If you don't know about octopress, octopress is a blog framework that let's you create blog posts as a static page instead of a full dynamic page like wordpress, it is simpler because it doesn't need any database or special server, and you can host your blog on gh-pages as it is a static web page

More info: 
http://octopress.org/

Let's get our hands dirty
-------------------------

First let's clone octopress framework

```
$ git clone git://github.com/imathis/octopress.git octopress
```

Now we want to point to our own github repository, so create your repository project repository on github and then

```
$ git remote rm origin
$ git remote add origin your_repository
```
Where it says your_repository it should be the project repository you just created.
After this we want to download all the gems that octopress uses, thankfully it comes with bundler

```
$ bundle install
```

Then we have to tell octopress to create all the needed folders

```
$ rake install
```

This is a good point to commit all our changes to our repository

```
$ git add -A .
$ git commit -m "Initial setup"
```

Now we need to configure octopress to use github pages

```
$ rake setup_github_pages  
```

Copy and paste your github repository on the promt when asked for it.

We are almost there, so we have to configure octopress to be published on /blog in order to do that we have to change the root directory

```
$ rake set_root_dir[/blog]
```

And then we have to change the url in the the _config.yml file, note that if you have a custom domain like for example jonvillage.com you have to put that there, if you don't want a custom domain and want to use your github url it would be just yourusername.github.io/blog

Also we need to change the permalink to display your posts in the correct url

```
url: http://yoururl/blog

permalink: /:year/:month/:day/:title/
```

The _config.yml file lets you configure the blog title, subtitle and more.

Now we need to generate all the pages and commit everything to your repository master

```
$ rake generate 
$ git add -A . 
$ git commit -m "Successfuly configured blog"
```

The finishing touch

```
rake deploy
```

Now go to http://yoururl/blog and you can see it

I hope you liked it and could deploy it, if you have any further question just ask and I will answer as soon as I can
