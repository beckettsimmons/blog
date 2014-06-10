**********************************
This Blog with Tinkerer and Github
**********************************

So I though it would be nice to write down how I use Tinkerer and Github to write this here blog.

Setup
=====
First things first. I started by creating a new repo on Github and cloned it to my local machine::

    git clone https://github.com/beckettsimmons/blog.git

Next I :strong:`cd` to my blogs directory and setup tinkerer. Which assumes that you actually got it installed correctly...    ::

    tinker --setup

Then as instructed I edit my *conf.py* file with the necessary details.
This includes the *withgithub* extension. So I have to edit that line in my *conf.py* to look like this::

    # Add other Sphinx extensions here
    extensions = ['tinkerer.ext.blog', 'tinkerer.ext.disqus', 'withgithub']

Next I need to add the *_exts* folder to my blog's root and drop `withgithuwithb.py <https://github.com/vladris/tinkerer-contrib/blob/master/withgithub/withgithub.py>`_ inside.

Lastly, I setup the **gh-pages** branch that I will commit blog builds to which will be publish to Github::

    git checkout --orphan gh-pages
    git rm -rf .

Daily Use
#########

This is how typically add a post, page, or modify my blog. Firstly, I just make sure that my git directory on **master** branch is clean and ready to use. Then I can start to use Tinkerer to, say, make a new post::

    tinker --post "myCoolPost"

Yes, for whatever reasons I dislike spaces in any names... That then creates a new .rst file in a location similar to */2014/05/10/myCoolPost.rst*. I just copy and post my post into that file. 

I then commit my newest post on my **master** branch. ::

     git commit -m "Added a cool post"

Now, this is the part where I hack it. First I build my Tinkerer blog on **master**, then stash my changes, checkout gh-pages and forcefully apply the stash.  ::

    tinker --build
    git stash save myCoolPost
    git checkout gh-pages
    git checkout stash@{0} -- . #overwrite directory with stash

After that I just simply add the new files, commit, then push. The new post is now up on a git page!

#TODO: Proof Read this blog.

