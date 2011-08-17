--- 
layout: post
title: CakePHP now available at Github
categories: articles
---
<em><strong>Update:</strong> The Github repository I created now has an untouched clone of the CakePHP 1.2 SVN branch as the master. I then created a branch of this called 'pimped', which contains my own custom code. This means that you can choose to use the official Cake core, or my pimped copy. I'll try to write a little more about my pimped branch in a future post.</em>

For the last few months, I've been developing an application which I hope to release to the unsuspecting public very soon. So I wanted to get it on my server and tested remotely, which I promptly did by checking out a copy from my SVN repository. I also did the same for the Cake core, by checking out <a href="https://svn.cakephp.org/repo/branches/1.2.x.x/cake">https://svn.cakephp.org/repo/branches/1.2.x.x/cake</a>.

Great, all worked fine... until I spotted loads of errors in the app. I then remembered that I made some local changes to the Cake core. I know, I know, it's a cardinal sin. But I really needed these changes for this app, and it was doing nobody any harm, as they stayed on my local machine. But now, I also needed them on my remote copy on the server, but want to be able to 'svn up' the cake core, whenever there are updates.

So I figured the best way would actually be to use a different SCM just for this purpose. I'd played with <a href="http://git.or.cz/">Git</a> a little, and have been really impressed at <a href="http://github.com">Github</a>. So I created a public repo at Github, and proceeded to create a clone of the Cake SVN repo, which I then pushed to the public repo at Github. I then applied my custom changes, and now we have a mirror of the CakePHP 1.2 branch at <a href="https://github.com/joelmoss/cakephp/tree">https://github.com/joelmoss/cakephp/tree</a>.

I can now clone the new git repo on my remote server, and I have a copy of CakePHP with all my custom changes, which I can update as and when I need to. This is all assuming of course, that I regulalry update the repo from the Cake SVN repo.

So things have actually turned out quite well. Please feel free to push and pull to/from the new <a href="http://github.com/joelmoss/cakephp/tree/master">git repo</a>, and let me know your thoughts.
