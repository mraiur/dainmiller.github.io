---
published: true
title: Fix Login & Keyring Issues in Ubuntu
layout: post
---
I know this isn't an ideal fix, but my gosh this is an annoying issue.

What happens when you virtualize Ubuntu 12-14, is that it sets the password and user account as "parallels". 

Then, upon first login, it asks you to reset that password. In the internal OS process of resetting that password, in virtualization and only in some instances for some people, it hiccups and fails to correctly set the password PGP key in the OS itself. 

What this means is you're allowed to login to certain things, because your login did get stored but at a deeper level it wasn't persisted, so certain **otherrrrr** things will fail. 

For instance, if you try to create user accounts or do other admin actions that prompt Ubuntu password popup, those will all fail if your login wasn't persisted correctly.

To fix this I chose the nuke it option:

1. Hit cmd or windw btn

2. Type password, hit down arrow, hit enter on _Passwords and Keys_

3. Click login, click green plus button on top left of window.

4. Click password keyring and continue

5. Name it whatever

6. Set password to empty on both and hit submit.

All done, issue fixed. 