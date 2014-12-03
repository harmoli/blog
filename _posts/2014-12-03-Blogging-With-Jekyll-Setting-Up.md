---
layout: post
title: Blogging with Jekyll on Github: Setting Up Custom Domains
tags: [Jekyll, GitHub pages, custom domains]
author: Harmony M Li
---
Over the past week, I have been attempting to set up my Jekyll blog to be
configured correctly.  While it is a bit meta to be blogging about how I got
my blog set up, there are a couple caveats in Jekyll worth mentioning for
anyone who is attempting to create or set up a Jekyll blog via Github pages.

For the most part, blogging with Jekyll on Github is very straight
forward.  This is even more true with resources like [Jekyll
Now](http://github.com/barryclark/jekyll-now) which allow first time
Jekyll-Github users to set up their blogs in under 10 minutes.  For more
advanced users, it boasts a detailed and clearly written README to help
navigate through the initial hurdle of setting up, allowing you to focus on
customization and content delivery.  However, things start to go haywire once
we attempt to configure Jekyll to work with subdomains or Github project
pages.

1. Configuring username.github.io for an apex domain
This is, perhaps, the most straight forward. Let's say you have an apex domain
like example.com.  

GitHub: Add a CNAME file to your GitHub username.github.io repository. 

DNS Provider: Add either a) an A record that points to the following IP
addresses:

* `192.30.252.153`
* `192.30.252.154`

or b) an ALIAS record that points to username.github.io.

2. Configuring username.github.io for a subdomain
Like the former configuration, you will need to first add a CNAME file to your
repository.  The contents will be the subdomain url.  For example,
'blog.example.com' or 'www.example.com'.  

NOTE:  If you configure username.github.io to have a CNAME for your apex domain
(example.com), the 'www' subdomain will also redirect properly to
username.github.io.

DNS Provider: Add a CNAME record that points to `username.github.io` 

3. Configuring project pages for an apex domain
Configuring project pages for an apex domain works similarly to configuring
username.github.io for an apex domain.  Remember that the `gh-pages` branch is
served as the webpage, whereas the rest of the branches are left untouched.  So
everything you do must be committed to the `gh-pages` branch.

4. Configuring project pages for a subdomain
Like configuring username.github.io for a subdomain, you will need to add a
CNAME record on your GitHub repository and on your DNS provider.  If you
previously had your `baseurl` property set to the repository name such as
`blog/`, make sure you change the `baseurl` to the new subdomain URL that you
plan to use.  Otherwise, your content will not serve correctly.

Useful links:
* [GitHub: Setting up a custom domain with GitHub Pages](https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages/)

* [GitHub: Tips for configuring an A record with your DNS provider](https://help.github.com/articles/tips-for-configuring-an-a-record-with-your-dns-provider/)

* [GitHub: Tips for configuring a CNAME record with your DNS provider](https://help.github.com/articles/tips-for-configuring-a-cname-record-with-your-dns-provider/)

* [GitHub: Troubleshooting custom domains](https://help.github.com/articles/my-custom-domain-isn-t-working/)

TIPS:
* DNS settings take a while to propagate, you can check to see if they are pointing at the desired IP addresses by using the `dig` command (`dig username.github.io`)

* Project pages are served from the `gh-pages` branches, so make sure all your project website pages are commited to the `gh-pages` branch

Happy blogging!
