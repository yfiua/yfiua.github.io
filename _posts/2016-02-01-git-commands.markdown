---
layout: post
title:  "Some Useful Git Commands"
date:   2016-02-01 21:10:00 +0100
comments: true
categories: tech
---

1.  Credential caching

    Cache git credential (for 15 mins by default), so you don't have to type in your username and password every time.

        git config --global credential.helper cache
    
    You can provide options via the credential.helper configuration variable (this example increases the cache time to 1 hour).

        git config --global credential.helper 'cache --timeout=3600'

2.  Git 

    Suggested by Jérôme Kunegis: "Don't go home when `svn st` or `git` doesn't return an empty string". To get rid of the verbose `git status` command, simply add this piece of code to your `.bashrc` file, and use `git` instead of `git status`, since the original `git` almost gives you nothing.

        git() {
          if [ $# -eq 0 ] ; then
            git log --oneline origin/master..HEAD && git status -s
          else
            command git "$@"
          fi
        }

3.  Unicode displaying

    Use this command to let your git display Unicode characters correctly.

        git config --global core.quotepath false

