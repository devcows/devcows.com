---
title: "Create a blog with Hugo and deploy it to GitHub with Semaphore"
slug: "create-a-website-or-blog-with-hugo-and-gitHub-pages"
date: "2016-05-26"
tags:
  - "hugo"
  - "github"
---

### Introduction

Static site generators are becoming increasingly popular and many bloggers and website owners have already migrated to them. Not having a language-specific runtime like Python or PHP allows to basically run your website anywhere you want. Moreover, it also reduces the attack surface since there is not a lot to hack in the server side as there is only static files (HTML, Javascript, CSS).

In this tutorial we are going to use Hugo -a popular static site generator written in Go- to create our blog. We are going to keep track of sources in GitHub, leveraging their [Pages](https://pages.github.com/) feature to host and serve our blog for free. Finally, we will use Semaphore to automate the build and deployment processes, so that we only worry about editing our content in Markdown.

This figure describes the final workflow after going through the tutorial.

* Figure with workflow. Content change -> push to GH master -> Travis build w/ Hugo -> push to gh-pages


### Goals

By the end of this tutorial, you will learn:

* How to create websites and blogs with Hugo,
* How to host static website on GitHub Pages,
* How to continuously deploy your website using Semaphore.

### Prerequisites

For this tutorial, you will need:

* A basic knowledge of continuous integration systems and Git,
* A [GitHub](https://github.com/) repo to which we will push our content, and
* A [Semaphore](https://semaphoreci.com/) account where you will build and trigger the deployment of your blog.


## What is Hugo?

Hugo is a static site generator like Jekyll. Hugo does not dynamically generate a page every time a request comes in. Instead, before deploying your site, Hugo builds your website with your content and generates the public files that will be served by the web server (i.e. HTML, CSS, Javascript) based on the source content you have written in a human-friendly language like Markdown. Therefore, websites built with Hugo have no dependencies on language-specific runtimes like Ruby, JVM, or Python and neither with databases.

## Why Hugo?

Typically, when you think about creating a website or a blog, the first thing that comes to your mind is Wordpress. Wordpress is the undeniable leader representing one fourth of all sites in the Internet. But being that popular also has its drawbacks as it is also the target of a large number of attacks and your site can be compromised if you don't keep it up to date constantly. Moreover, finding a free and decent hosting for your Wordpress site can also be a arduous task.

In the last years, very interesting tools have emerged and allow you to easily create static websites from friendly formats like [Markdown](https://daringfireball.net/projects/markdown/) or [reStructuredText](http://docutils.sourceforge.net/rst.html). One of the pioneers was [Jekyll](https://jekyllrb.com/), and others like [Middleman](https://middlemanapp.com/) and [Hugo](http://gohugo.io/) followed. We have chosen Hugo for this tutorial due to its blazing fast build times and, why not, because I love Go.

## Using Hugo

Installing Hugo is quite easy. If you are on OS X and use [Homebrew](http://brew.sh/), you just need to run `brew update && brew install hugo` and you are good to go. For other OS or if you are having some issues installing it please check the [official documentation](https://gohugo.io/overview/installing/) for the installation information.

To make sure you have installed Hugo correctly, run `hugo version` and you should get a similar output like this.

```
$ hugo version
Hugo Static Site Generator v0.15 BuildDate: 2015-11-26T07:29:07+01:00
```


## Initialize your repository

Let's go to GitHub and create a public repo to host your blog. I have called my repo simply `blog`. If you name it differently, remember to replace it in the following occurrences.

You can now go ahead and clone it wherever your workspace is.

```
$ git clone git@github.com:<your_github_username>/blog.git
Cloning into 'blog'...
warning: You appear to have cloned an empty repository.
Checking connectivity... done.
$ cd blog
```


## Using Hugo to scaffold the blog

Hugo comes with helper commands that allows you to easily scaffold your site. So let's tell Hugo to create a base site in the current directory. We add the `--force` flag because the directory is not empty - we may have a license or readme file as well as the Git directory.

```
hugo new site . --force
```

The resulting directory tree will be as follows.

```
$ tree .
.
├── archetypes
├── config.toml
├── content
├── data
├── layouts
└── static

5 directories, 1 file
```

In this blog example we are only going to make use of the `content` directory. But you can refer to [Hugo's official documentation](https://gohugo.io/overview/introduction/) for more advanced setups.

## Add some content

Now let's create the first post of our blog. We will use the `hugo new` command to create posts inside the `content` directory.

```
$ hugo new post/my-first-post.md
/Users/adrianmo/blog/content/post/my-first-post.md created
```

The above command created a Markdown file with the following metadata.

```
$ cat /Users/adrianmo/blog/content/post/my-first-post.md
+++
date = "2016-06-07T13:10:11+02:00"
draft = true
title = "my first post"

+++
```

As you can see, Hugo marked the post as a draft. By default drafts are not built, so let's add some content and change some metadata to this blog post.

```markdown
+++
date = "2016-06-07"
draft = false
title = "My first post with Hugo"
tags = [
    "hugo",
    "blog",
]
+++

This is the very first post of my brand new **Hugo** blog.

> You can use Markdown to add some style to your posts.

```

## Add a theme

If you were to build your blog at this point, you would not see anything since there is no theme configured yet and Hugo does not provide a default one.

Hugo uses the theme to render your blog. You can adapt any website template to work with Hugo, but for the purpose of simplicity we are going to use one of the themes available at https://themes.gohugo.io/.

First of all, create a `theme` directory and change directory to it.

```
mkdir themes && cd themes
```

Now, we are going to clone the `aglaus` theme. But you can clone any other theme.

```
git clone https://github.com/dim0627/hugo_theme_aglaus.git aglaus
```

Let's go back to the project's root directory.

```
cd ..
```

And edit the `config.toml` file to tell Hugo what theme we want to use. Let's add a `theme` field with the name of the template directory.

```
baseurl = "http://replace-this-with-your-hugo-site.com/"
languageCode = "en-us"
title = "My New Hugo Site"
theme = "aglaus"
```

## Build and preview your blog

Now that we have added our first post and configured a theme, it's time to build and preview our job. Hugo comes with a development server that rebuilds and reloads automatically while we are updating the content. Let's run it.

```
hugo serve
```

```
0 draft content
0 future content
1 pages created
2 paginator pages created
0 categories created
0 tags created
in 20 ms
Watching for changes in /Users/adrianmo/blog/{data,content,layouts,static,themes}
Serving pages from memory
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

You can know open your web browser and go to http://localhost:1313 to see your new blog.

- Figure

Excellent! You can now stop the server by hitting *Ctrl + C* and let's see how Hugo builds your site.

If you just run `hugo`, it will gather all your source files and build them into a directory called `public`. This `public` directory contains everything needed by the web server.

```
$ hugo
0 draft content
0 future content
1 pages created
2 paginator pages created
0 tags created
0 categories created
in 24 ms
```

This is what Semaphore will do later to do to deploy our blog.

## Push it to GitHub



## Set up TravisCI

The magic comes here. To avoid having to manually build and deploy the website every time we make a change, we will configure TravisCI to do it for you whenever there is a push to the `master` branch.

Go to `http://travis-ci.org` and log in using your GitHub credentials. It will detect all your public repos automatically. Select your `bookshelf` repo. Travis will not do anything yet since it cannot find the `.travis.yml` file in your project's root directory. This file tells Travis what to do whenever it detects changes in your code.

So, let's start by creating a `.travis.yml` file and adding the following content.

```
language: go

go:
  - 1.6
```

With this we are telling Travis that our project language is Go. That will make it easier to install Hugo.

```
install:
  - go get -v github.com/spf13/hugo
```

On the `install` section we install the dependencies. In this case, it's only going to be Hugo.

```
before_script:
  - mkdir themes && cd themes
  - git clone https://github.com/dim0627/hugo_theme_robust.git
```

Now, we need to pull our theme into the `themes` directory. Just like we did on the quickstart guide.

```
script:
  - hugo
  - test -d public
```

The `script` section is the one that will build the website and verify that a `public` directory is generated. If the build process fails, Travis is going to stop here and not go any further, alerting us that it failed.

```
deploy:
  provider: script
  skip_cleanup: true
  script: bash ./deploy.sh
  on:
    branch: master
```

The `deploy` section will run a script whenever there is a push to the master branch.

So the full script looks like this:

```
language: go

go:
  - 1.6

env:
  global:
    - ENCRYPTION_LABEL: 6004e94fbaa2
    - COMMIT_AUTHOR_EMAIL: hello@devcows.com

install:
  - go get -v github.com/spf13/hugo
  - pip install Pygments --user

before_script:
  - mkdir themes && cd themes
  - git clone https://github.com/dim0627/hugo_theme_robust.git

script:
  - hugo
  - test -d public

deploy:
  provider: script
  skip_cleanup: true
  script: bash ./deploy.sh
  on:
    branch: master
```

## Make a change and push it



## Configure a CNAME
