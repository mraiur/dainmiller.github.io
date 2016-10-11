---
published: true
title: Login Issues in Linux
layout: post
tags: [linux, ubuntu, bugs]
categories: [linux]
summary: The nuke-it option is not secure, but it's certainly easier. 😍
---
I know this isn't an ideal fix, but my gosh this is an annoying issue.

What happens when you virtualize Ubuntu 12-14, is that it sets the password and user account as "parallels". 

Then, upon first login, it asks you to reset that password. In the internal OS process of resetting that password, in virtualization and only in some instances for some people, it hiccups and fails to correctly set the password PGP key in the OS itself. 

What this means is you're allowed to login to certain things, because your login did get stored but at a deeper level it wasn't persisted, so certain **otherrrrr** things will fail. 

For instance, if you try to create user accounts or do other admin actions that prompt Ubuntu password popup, those will all fail if your login wasn't persisted correctly.

**To fix this I chose the nuke it option:**

Hit cmd or windw btn

Type password, hit down arrow, hit enter on _Passwords and Keys_

Click login, click green plus button on top left of window.

Click password keyring and continue

Name it whatever

Set password to empty on both and hit submit.

All done, issue fixed. 
