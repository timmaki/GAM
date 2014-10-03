- [Introduction](#introduction)
- [1) Enabling the APIs](#1-enabling-the-apis)
- [2) Download GAM](#2-download-gam)
  - [Windows Users](#windows-users)
  - [Mac and Linux Users](#mac-and-linux-users)
- [3) Extract GAM](#3-extract-gam)
  - [Windows Users](#windows-users-1)
  - [Mac and Linux Users](#mac-and-linux-users-1)
- [4) Generating your own client\_secrets.json file](#4-generating-your-own-client\_secretsjson-file)
- [5) Running GAM for the First Time](#5-running-gam-for-the-first-time)
  - [Windows Users](#windows-users-2)
  - [Mac and Linux Users](#mac-and-linux-users-2)
- [6) More simple GAM commands](#6-more-simple-gam-commands)

# Introduction

Dito GAM is a command line tool that allows administrators to manage many aspects of their Google Apps Account. This page provides simple instructions for downloading, installing and starting to use GAM.

GAM requires Google Apps Business, Education, Partner or Government Edition.  Google Apps Free Edition has limited API support and not all GAM commands work.

# 1) Enabling the APIs
GAM talks to Google's Servers via Google APIs (Application Programming Interface). By default, APIs for working with Google Apps are disabled. You'll need to follow Google's instructions for [Enabling Administrative API Access](http://support.google.com/a/bin/answer.py?hl=en&answer=60757). API access must be enabled for GAM to function properly.

# 2) Download GAM
## Windows Users
Head to the [Releases page](https://github.com/jay0lee/GAM/releases) and download the latest Windows version of GAM, do not download the Python Source version (unless you know what you're doing).

## Mac and Linux Users
Head to the [Releases page](https://github.com/jay0lee/GAM/releases) and download the latest Python source version of GAM, do not download the Windows version.

# 3) Extract GAM
## Windows Users
Use the archive extraction tool of your choice to extract the files from the GAM .zip you downloaded. Windows XP and higher have a built in tool that works just fine. When specifying where to extract GAM, I suggest extracting directly to C:\ so that the files will reside in C:\GAM. Once completed, you should have a folder with gam.exe and a few text files in it.

## Mac and Linux Users
Use the archive extraction tool of your choice to extract the files from the GAM .zip you downloaded. I suggest first creating a sub-folder in your home directory (something like ~/gam/) and then extracting the GAM archive there.

# 4) Generating your own client\_secrets.json file
Google enforces quotas on the number of API operations a program can run. The client\_secrets.json file is used to register your GAM program with Google and provide you with your own API quota. Instructions for generating and downloading client\_secrets.json are [on this page](CreatingClientSecretsFile). Please note that despite the name, client\_secrets.json does not provide authorized access to Google Apps, it only identifies your GAM install to Google for quota management. It is perfectly safe to use one client\_secrets.json file with multiple Google Apps domains.

# 5) Running GAM for the First Time
## Windows Users
Open a command prompt on your computer. You can do this by going to Start -> Programs -> Accessories -> Command Prompt or by opening the Run... dialog on the start menu and typing CMD then enter. Now change to the directory where you extracted GAM. The command to change directories looks like:
```html

cd \gam
```
this works if you extracted GAM to c:\gam. If you extracted it elsewhere, specify that location instead. Now type:
```html

gam info domain
```
After seeing some information about Dito (press Enter), you'll be asked to specify which "scopes" you'd like the OAuth token to support. For now, select the last option to continue, all scopes will be selected. Next GAM will open up a web page in order for you to grant access to retrieve data and make changes to your Google Apps account. Make sure you are logged in to a Google Apps Administrator account before granting access. Once you've granted access, switch back to the command prompt window, GAM should already be working to display information about your Google Apps domain.

Congrats, you're up and running with GAM.

## Mac and Linux Users
Open up a terminal window on your computer. On Linux, this is generally under Accessories -> Terminal. On Mac, it's under Applications -> Utilities -> Terminal. Now change to the directory where you extracted GAM. Try:
```html

cd ~/gam
```
this will work if you extracted the gam files to a subfolder named gam in your home directory. If you extracted them elsewhere, replace ~/gam with the full path to them. Now run:
```html

python gam.py info domain
```
If you get an error about python not being a valid program, make sure you have the Python interpreter installed on your machine. All Macs and most Linux installs should include Python but if not, you may need to research how to install it on your OS/Distribution. If everything works, you'll be asked to specify which "scopes" you'd like the OAuth token to support. For now, just select the last option to continue, all scopes will be selected.

Next GAM will open up a web page in order for you to grant GAM access to retrieve data and make changes to your Google Apps account. Make sure you are logged in to a Google Apps Administrator account before granting access. Once you've granted access, switch back to the command prompt window and hit enter. If no errors are printed, you should see details about your Google Apps domain if everything is working.

If you're running GAM on a machine that doesn't have a browser installed (for example, a headless Linux box), you won't be able to open a browser on the machine running GAM in order to authorize. In this case, you should first create a file called ` nobrowser.txt ` in the same location as gam.py. Then, after running ` gam info domain `, GAM will simply display a link which you can copy and open from a computer running a browser in order to manually authorize.

Instead of needing to type "python gam.py for every command, we can use the alias command to shorten it to just "gam":
```html

alias gam="python ~/gam/gam.py"
```
Now when we can just type commands like:
```html

gam info domain
```
you'll need to type the alias command each time you open a Terminal to run GAM or add it to your .bashrc file.

Congratulations, you now have a working GAM install.

# 6) More simple GAM commands

Try the following GAM commands to get a feel for how the program works. I suggest creating a test user account for experimenting, or if you don't have a test account, use your account, we'll call our test user crashtestdummy in the examples below.

If you haven't already, we can just create our crashtestdummy account with GAM:
```html

gam create user crashtestdummy firstname Crash lastname "Test Dummy" password "BuckleUp"
```

We can give crashtestdummy an alias so that emails to idontwearseatbelts go to him:
```html

gam create alias idontwearseatbelts user crashtestdummy
```

We can create a group for crash test dummy's friends:
```html

gam create group test-dummies-united name "Test Dummies United" description "Support Group Against Plastic Abuse"
```

Crash test dummy likes Gmail but sometimes he prefers to use IMAP with his favorite email client, Thunderbird, let's enable IMAP for him:
```html

gam user crashtestdummy imap on
```

these are just a few examples, more are available under the topics to the right. Have fun!