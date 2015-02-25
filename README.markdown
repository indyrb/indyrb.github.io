## Indy.rb

The source code for the site is in this source branch. The master branch is generated
and updated when you run 'rake deploy'. The master branch comes from a git repo initialized in the _deploy directory and the source from the git repo on the root directory of the project.

[This site](http://blog.zerosharp.com/clone-your-octopress-to-blog-from-two-places/) is the
source of much of this info and goes into more detail.

To get started, first you need to clone the source branch:

    git clone -b source git@github.com:indyrb/indyrb.github.io.git indyrb

then install:

    cd indyrb
    bundle install

Now you will clone the _deploy branch (the current generated site):

    git clone git@github.com:indyrb/indyrb.github.io.git _deploy

Then you should be set!

Before trying to deploy an update, be sure to pull the latest from both source and master:

    cd indyrb
    git pull origin source

Then you can deploy:

    rake generate
    rake deploy

and commit the changes to source:

    git add .
    git commit -am "`date`"
    git push origin source

Some commands from [This helpful site](http://blog.revolunet.com/blog/2013/04/15/octopress-cheatsheet/)

    # create a new post
    rake new_post['Title of the post']

    # create a new page
    rake new_page['Title of the page']

    # preview your work on localhost:4000
    rake preview

    # publish it
    cd _deploy
    git pull origin master

    cd ..
    git pull origin source

    rake generate && rake deploy

    # commit and backup(automatic message)
    git add .
    git commit -am "`date`" && git push origin source

The docs linked to below go into more detail and the Rakefile in source is a helpful read as far as knowing what a task is doing.


## Octopress 3.0

Note: Octopress 3.0 is in development at https://github.com/octopress/octopress

## What is Octopress?

Octopress is [Jekyll](https://github.com/mojombo/jekyll) blogging at its finest.

1. **Octopress sports a clean responsive theme** written in semantic HTML5, focused on readability and friendliness toward mobile devices.
2. **Code blogging is easy and beautiful.** Embed code (with [Solarized](http://ethanschoonover.com/solarized) styling) in your posts from gists, jsFiddle or from your filesystem.
3. **Third party integration is simple** with built-in support for Pinboard, Delicious, GitHub Repositories, Disqus Comments and Google Analytics.
4. **It's easy to use.** A collection of rake tasks simplifies development and makes deploying a cinch.
5. **Ships with great plug-ins** some original and others from the Jekyll community &mdash; tested and improved.

**Note**: Octopress requires a minimum Ruby version of `1.9.3-p0`.

## Documentation

Check out [Octopress.org](http://octopress.org/docs) for guides and documentation.
It should all apply to our current stable version (found in the `master`
branch). If this is not the case, [please submit a
fix to our docs repo](https://github.com/octopress/docs).

## Contributing

[![Build Status](https://travis-ci.org/imathis/octopress.png?branch=master)](https://travis-ci.org/imathis/octopress)

We love to see people contributing to Octopress, whether it's a bug report, feature suggestion or a pull request. At the moment, we try to keep the core slick and lean, focusing on basic blogging needs, so some of your suggestions might not find their way into Octopress. For those ideas, we started a [list of 3rd party plug-ins](https://github.com/imathis/octopress/wiki/3rd-party-plugins), where you can link your own Octopress plug-in repositories. For the future, we're thinking about ways to easier add them into our main releases.


## License
(The MIT License)

Copyright © 2009-2013 Brandon Mathis

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the ‘Software’), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED ‘AS IS’, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
