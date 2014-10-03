(TODO: Add table of contents.)

_**Comments have been turned off for these help pages, please post your questions and comments to the [Mailing List](http://groups.google.com/group/google-apps-manager)**_

# Introduction

Google Apps Manager (GAM) is a command line tool that allows administrators to manage many aspects of their Google Apps Account. This page provides simple instructions for downloading, installing and starting to use GAM.

GAM requires Google Apps Business, Education, Partner or Government Edition.  Google Apps Free Edition has limited API support and not all GAM commands work.

# Step 1: Enabling the Provisioning API
GAM talks to Google's Servers via the Google Apps Provisioning API (Application Programming Interface). Google has more information on the Provisioning API [here](http://www.google.com/support/a/bin/answer.py?hl=en&answer=60757). By default, the Provisioning API is disabled. You can enable the Provisioning API by logging in to your domain as an Administrator and clicking the "Manage this Domain" link. Then, along the blue ribbon at the top of the page, click the link that says "Domain Settings" and finally the link that says "User Settings" just below the blue ribbon. Make sure the checkbox next to "Enable provisioning API" is checked and click "Save Changes" at the bottom of the page if it wasn't. That's it!

# Step 2: Download GAM
## Windows Users
Head to the [Downloads page](http://code.google.com/p/google-apps-manager/downloads/list) and download the latest Windows version of GAM, do not download the Python Source version (unless you really know what you're doing).

## Mac and Linux Users
Head to the [Downloads page](http://code.google.com/p/google-apps-manager/downloads/list) and download the latest Python source version of GAM, do not download the Windows version.

# Step 3: Extract GAM
## Windows Users
Use the archive extraction tool of your choice to extract the files from the GAM .zip you downloaded. Windows XP and higher have a built in tool that works just fine. When specifying where to extract GAM, I suggest extracting directly to C:\ so that the files will reside in C:\GAM. Once completed, you should have a folder with gam.exe and a few text files in it.

## Mac and Linux Users
Use the archive extraction tool of your choice to extract the files from the GAM .zip you downloaded. I suggest extracting the files to a sub-folder of your home directory.

# Step 4: Running GAM for the First Time
## Windows Users
Open a command prompt on your computer. You can do this by going to Start -> Programs -> Accessories -> Command Prompt or by opening the Run... dialog on the start menu and typing CMD then enter. Now change to the directory where you extracted GAM. The command to change directories looks like:
```html

cd \gam
```
this works if you extracted GAM to c:\gam. If you extracted it elsewhere, specify that location instead. Now type:
```html

gam info domain
```
you'll be prompted for your Primary Google Apps domain. This should be something like example.com. Then you'll be asked to enter your Client ID. If you don't know it and don't plan on using the Group Settings API, just press Enter here. If you need to learn how to get a Client ID and Secret, see [here](http://code.google.com/p/google-apps-manager/wiki/GettingAnOAuthConsoleKey). Next you'll be asked to specify which "scopes" you'd like the OAuth token to support. For now, type 5 and press enter to select all scopes, then press 8 and Enter to continue. Next GAM will open up a web page in order for you to grant GAM access to retrieve data and make changes to your Google Apps account. Make sure you are logged in to a Google Apps Administrator account before granting access. Once you've granted access, switch back to the command prompt window and hit enter.

If you are getting DLL errors when attempting to run GAM, please try installing the [MS Visual C++ 2008 Redistributable Package](http://www.microsoft.com/downloads/en/details.aspx?FamilyID=9b2da534-3e03-4391-8a4d-074b9f2bc1bf&displaylang=en).

If no errors are printed, GAM will print out details of your Google Apps domain. Congrats, you're up and running with GAM.

## Mac and Linux Users
Open up a terminal window on your computer. On Linux, this is generally under Accessories -> Terminal. On Mac, it's under Applications -> Utilities -> Terminal. Now change to the directory where you extracted GAM. Try:
```html

cd ~/gam
```
this will work if you extracted the gam files to a subfolder named gam in your home directory. If you extracted them elsewhere, replace ~/gam with the full path to them. Now run:
```html

python gam.py info domain
```
If you get an error about python not being a valid program, make sure you have the Python interpreter installed on your machine. All Macs and most Linux installs should include Python but if not, you may need to research how to install it on your OS/Distribution. If everything works, you will be prompted for your Google Apps domain. This should be something like example.com. Then you'll be asked to enter your Client ID. If you don't know it and don't plan on using the Group Settings API, just press Enter here. If you need to learn how to get a Client ID and Secret, see [here](http://code.google.com/p/google-apps-manager/wiki/GettingAnOAuthConsoleKey). Next you'll be asked to specify which "scopes" you'd like the OAuth token to support. For now, type 5 and press enter to select all scopes, then press 8 and Enter to continue. Next GAM will open up a web page in order for you to grant GAM access to retrieve data and make changes to your Google Apps account. If the web page fails to open, you can manually type the URL in a browser window on another machine. Make sure you are logged in to a Google Apps Administrator account before granting access. Once you've granted access, switch back to the command prompt window and hit enter. If no errors are printed, you should see details about your Google Apps domain if everything is working.

Instead of needing to type "python gam.py for every command, we can use the alias command to shorten it to just "gam":
```html

alias gam="python gam.py"
```
Now when we can just type commands like:
```html

gam info domain
```
you'll need to type the alias command each time you open a Terminal to run GAM. Congratulations, you now have a working GAM install.

# Step 5: More simple GAM commands

Try the following GAM commands to get a feel for how the program works. I suggest creating a test user account for experimenting on, or if you don't have a test account, use your account, we'll call our test user crashtestdummy in the examples below.

If you haven't already, we can just create our crashtestdummy account with GAM:
```html

gam create user crashtestdummy firstname Crash lastname "Test Dummy" password "BuckleUp"
```

We can give crashtestdummy a alias so that emails to idontwearseatbelts go to him:
```html

gam create alias idontwearseatbelts user crashtestdummy
```

We can create a group for crash test dummy's friends:
```html

gam create group test-dummies-united name "Test Dummies United" description "Support Group Against Plastic Abuse" permission member
```

Crash test dummy like's Gmail but sometimes he prefers to use IMAP with favorite email client, Thunderbird, let's enable IMAP for him:
```html

gam user crashtestdummy imap on
```

these are just a few examples, more are available under the topics to the left. Have fun!

# Step 6: Need a Google Apps Expert?
GAM is made possible and maintained by the work of Dito. Who is Dito?

Dito is solely focused on moving organizations to Google's cloud. After hundreds of successful deployments over the last 5 years, we have gained notoriety for our complete understanding of the platform, our change management & training ability, and our rock-star deployment engineers. We are known worldwide as the Google Apps Experts.
<br><a href='http://www.ditoweb.com?s=gam'><img src='http://ditoweb.com/images/website/header-logo.png' /></a>
<br>
Need a Google Apps Expert? Contact Dito at <a href='http://www.ditoweb.com?s=gam'>ditoweb.com</a>