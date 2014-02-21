Mac Setup with Vagrant
==================

This will run you through the steps to configure your web development environment using the vagrant install process.

Step 1 - Create accounts if you haven't already
--------

First go to [GitHub.com](http://github.com) and [Heroku.com](http://Heroku.com) and create an account there


Step 2: Download and install the tools
-------

I suggest following these installers in this order, because the last installer will have you retart your machine.  When it prompts you to, click "Yes".

* [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
* [Sublime Text Editor](http://sublimetext.com/)
* [Vagrant](http://www.vagrantup.com/downloads.html) 
 
 
Step 3:  Get the dev environment
-----------

**If you have a Firehose Flash Drive**:  copy the vagrant folder onto your __Desktop__.

**If you do not have a Firehose Flash Drive**: download and unzip the following file: [firehose-vagrant](https://github.com/kenmazaika/firehose-vagrant/archive/master.zip) to your __Desktop__ and rename the folder `vagrant`.  This is where all your web development environment will live.

Download the firehose.box file, and save it in your `Desktop/vagrant` folder.
 
Step 4: Add the Box
--------
 
Open up the **Terminal Window**: Hold CTRL+Spacebar, in the Spotlight type 'Terminal' and hit the enter key.

A terminal window will come up, and then run the following two commands:

```
cd ~/Desktop/vagrant
```
 
then run this next command, it may take a few moments to complete:

```
vagrant box add firehose firehose.box
```


Step 5: Turn on your Web Dev Environment
-------

In the terminal you've been using, type this command, again this may take a few moments to complete:

```
vagrant up
```
 
Step 6: Log into your dev environment
-----------
 
Then in your terminal type this command.  This will convert your terminal window locally, into a terminal window in your web dev environment and the title of the tab that you're in should change to say "ssh".  That means the terminal window is inside your web development environment.

```
vagrant ssh
``` 
 


Step 7: Accounts
------------

#### Generate SSH Key

 Inside the web development terminal window, where it says SSH, run this. _important note: the command has backticks (`) not single-quotes ('), either copy and paste the command or if you type it use the key to the left of the 1 to type the backtick in the first line_:
 
```
eval `ssh-agent -s`
ssh-keygen -t rsa -C "Firehose Vagrant" -N '' -f ~/.ssh/id_rsa
ssh-add ~/.ssh/id_rsa
```
 
#### Configure Heroku with SSH Keys
 
This will prompt you for your heroku username and password.  Enter that here.

```
heroku login
heroku keys:add
```
 
#### Configure Github with SSH Keys
 
```
curl "https://raw2.github.com/kenmazaika/firehose-vagrant/master/github-key.rb" > ~/.firehose-github.rb && ruby ~/.firehose-github.rb
```

Then adjust these to have your name and email address inside the double quotes:

```
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

##Amazon AWS services##

_We need an amazon developer account for some image storage space on Amazons S3 service (this will cost you nothing)_

* Sign-up and create an account for [Amazon Web Services](http://aws.amazon.com/). Anything we'll do over the weekend will cost you nothing, so don't worry about your credit card being charged.

 
Step 8: Test
---------
 
 In the web development terminal window, where it says SSH, run this, _important note: after you run `rails s` it won't give you the prompt to continue to enter commands. This is by design, so move onto the next step even if it looks like it's just hanging_:

```
cd /vagrant/src/firehose-test-app
rails s
```


Open a web browser on your windows machine and go to: [http://127.0.0.1:3030](http://127.0.0.1:3030)

If you want to return to a window where you can enter commands in web development terminal window, go into it and hold CTRL+C.  This will stop your webpage from working, but allow you to enter new commands.


Additional Info
---------------

#### A Note about Restarting Your Machine

When you restart your machine and go to connect to your development environment you will probably get a "Connection Error".  If this happens, you'll need to make sure to startup up the dev environment (Step 5).  To do this:

Open up the **terminal window**.

A command prompt will come up, and then run the following two commands:

```
cd ~/Desktop/vagrant
```

Then enter this command, it may take a few moments to complete:

```
vagrant up
```

#### How to log into your web development environment

When you want to log into your web development environment in a new terminal tab or window, open up the tab.  Then you'll want to move into the web development locations:

```
cd ~/Desktop/vagrant
```

Then once you're there, you can change the terminal window from a regular one, to the web development one by typing the following:

```
vagrant ssh
```