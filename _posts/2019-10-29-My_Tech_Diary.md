---
layout: post
title: "My Tech Diary"
date: 2019-10-28 16:00:06
image: '/assets/img/'
description: 'thoughts and daily useful tips'
tags:
- Thoughts
- Tips
categories:
- Dairy 
twitter_text: 'thoughts and daily useful tips'
---

## Git

I know the git has version rollback function, but I didn't care too much before, because I think I've already uploaded my file to github, if I just want the previous version back why not just download the file back from GitHub? And I always think that git pull can do this for me, but I was wrong, if I modified the file and ran  with git pull, it doesn't work. 

Well, it is time to pay for my lazyness, I finally met this stupid situation, I messed it up and all I wanted is to get my previous file version back. `Git reset` saves me.

You can use `git log` to view the commit history, Head indicates your current version, and use `git reset --hard commit_id` to get back to the past. Or you can use `git reflog` to view the command history and to jump to the future.

## 杂记





