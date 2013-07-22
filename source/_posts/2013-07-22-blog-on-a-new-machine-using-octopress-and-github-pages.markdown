---
layout: post
title: "Blog on a new machine: using octopress and github pages"
date: 2013-07-22 22:51
comments: true
categories: [octopress]
---
I have already create a github pages sometime before, using octopress,
hosted on github.
Today when I want to write a blog, I found I can not find the local
copy of the blog git repository to start. And I can't find an instruction on how
to reuse an existing octopress git repository to continue blogging on
the [official octopress website](http://octopress.org). After some
googling, here is how.
##Clone your existing blog repository
    git clone url_to_your_repository
The default branch after your checking out should be "master" branch.
Since octopress stores the "posts/blogs" under branch "source", and
place the generated static website under "master", I have to check out
the "source" branch from the remote repository to continue blogging.
This can be done by:
    git checkout source
##Install dependencies
    bundle install
this will get you all the required gems.
##Setup octopress to work with github pages
    rake setup_github_pages
##Setup locale
Since I may use Chinese to blog, I have to setup the locale. Or there
will be errors like "invalid byte sequence in xxxx(ASCII-8bit?)". 
On Mac OS X
    export LC_ALL=zh_CN.UTF-8 
On Windows
    set LC_ALL=zh_CN.UTF-8 
##Test if it works
First generate the static website from source.
    rake generate
Then preview the website at local.
    rake preview
This action will start a embeded webserver (WebBrick) listen at
[http://localhost:4000](http://localhost:4000).
The good thing is it will watch the file change and auto re-generate the
website if an change is detected. To view the latest website, all you
need to do is refresh the URL in your browser.
##Deploy it to github pages
    rake deploy
##Push your new blog to source
`rake deploy` only push the generated website to "master" branch of the
remote octopress repository. It will not automatically add your new post to
your local/remote repository. To save the new blog, you will need to add
it to git, and then push it to remote "source".
    git add .
    git ci -am "add new post"
    git push 

Go and check it!
