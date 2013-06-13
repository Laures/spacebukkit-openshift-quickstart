#Install and Run SpaceBukkit on OpenShift
This git repository helps you get up and running quickly with a SpaceBukkit installation on OpenShift.

##Preperations

If you don’t already have an OpenShift account, head on over to the website and signup.
It is completely free and Red Hat gives every user three free Gears on which to run your applications. 

This client requires a command shell with a working `git` command and the OpenShift Client tools. These tools, known as `rhc` are built and packaged using the Ruby programming language. They allow you to manage your gears and applications from the commandline. The installation of these tools is explained [here](https://www.openshift.com/developers/rhc-client-tools-install).

##Creating your Gear

For SpaceBukkit you will require a php gear with installed MySQL. You can easily set this up with rhc by doing:

    rhc app create %appname% php-5.3
    rhc cartridge add mysql-5.1 -a %appname%

rhc will have created your app now and cloned the git repository into a subfolder named `%appname%`.

##Adding the Quickstart

The last thing you need to do is add the code of this repository to yours.

    cd %appname%
    git remote add upstream -m master git@github.com:Laures/spacebukkit-openshift-quickstart.git
    git pull -s recursive -X theirs upstream master
    git push

Congratulation. With this push openshift will start your Minecraft server automaticly and deploy the SpaceBukkit admin panel.

##Accessing SpaceBukkit

You can access the Admin Panel by visiting the URL of your gear (`%appname%-%namespace%.rhcloud.com`). The default Superusers uses:

User: `root`
Password: `root`

**YOU SHOULD CHANGE THESE CREDENTIALS IMEDIATELY**

##Connecting to your Minecraft Server

Unfortunately OpenShift gears do not support public ports. You are required to create an SSH tunnel to your server first. Note that you will need to configure an SSH key for every player in your OpenShift settings!
The tunnel can be created with `rhc` easily.

    rhc port-forward -a %appname%

Alternatively you can configure ssh port-forwarding using tools like [putty](https://howto.ccs.neu.edu/howto/windows/ssh-port-tunneling-with-putty/) or the ssh command on [linux](http://www.revsys.com/writings/quicktips/ssh-tunnel.html) and [mac](http://www.engr.wisc.edu/computing/best/rdesktop-mac.html)

Congratulations, you can connect to your server using `localhost:15000`. Have Fun.

**There is a feature request for at least one public port [here](https://www.openshift.com/content/at-least-one-port-for-external-use-excluding-8080-please)! PLEASE GO AND VOTE FOR IT**
