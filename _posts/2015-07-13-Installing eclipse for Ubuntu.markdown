---
layout: post
title:  "Installing eclipse for Ubuntu"
date:   2015-07-13 06:49:49
categories: eclipse, ubuntu, chmod, file
banner_image: ""
featured: false
comments: true
---

This is about installing eclipse for Ubuntu 9.x new desktop version. You can run any eclipse you want to this way! I have taken this content from here for easier and faster reference. I have also added my own stuff to it, which I found would make eclipse start up properly. So read on.

On ubuntu, remember this always:

Please download the x86_64 version of eclipse-<version-name> and NOT the 32 bit version. That won’t work!

These instructions assume you’ve downloaded and extracted the above mentioned Eclipse tarball:

    bash
    sudo mv eclipse /opt/eclipse cd /opt sudo chown -R root:root eclipse
    sudo mv eclipse /opt/eclipse cd /opt sudo chown -R root:root eclipse
    sudo chmod -R +r eclipse
    sudo chmod +x `sudo find eclipse -type d`


Then create an eclipse executable in your path


    bash
    sudo touch /usr/bin/eclipse
    sudo chmod 777 /usr/bin/eclipse
    
    sudoedit /usr/bin/eclipse
    

With these contents:


    bash
    #!/bin/sh
    export ECLIPSE_HOME=/opt/eclipse
    $ECLIPSE_HOME/eclipse $*
    

**NOTE:**

If you use, sudo chmod 755, it wont allow you to edit the /usr/bin/eclipse file in some systems, hence I have changed it to chmod 777 instead. you can change back to 755 after editing the file!

Also see that ECLIPSE_HOME is set to /opt/eclipse (WITHOUT QUOTES)
Now you can execute Eclipse from anywhere in your bash shell by just typing ‘eclipse’.