<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](http://doctoc.herokuapp.com/)*

- [How GAM Authenticates to Google](#how-gam-authenticates-to-google)
- [Avoiding the Prompt for domain, admin user and password](#avoiding-the-prompt-for-domain-admin-user-and-password)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

_**Comments have been turned off for these help pages, please post your questions and comments to the [Mailing List](http://groups.google.com/group/google-apps-manager)**_

# How GAM Authenticates to Google
When you run GAM for the first time, or if you haven't run GAM for roughly 24 hours, you'll be prompted for your Google Apps domain, admin user and password. After successfully confirming the credentials, Google's servers issue GAM a token that can be used to authenticate commands that modify or read information from Google's servers regarding your Google Apps account. The token is good for 24 hours after which it expires and you are asked for your credentials again. GAM stores the token in a file called **token.txt** and will always check to see if it has a valid token in this file before prompting for credentials. If you're worried about security, always delete the token.txt file completely off your computer when you're done running GAM commands, you should also never run GAM on a computer that isn't physically secured.

# Avoiding the Prompt for domain, admin user and password
If you'd like to skip the credentials prompts completely, you can create a file in the same directory as GAM named **auth.txt**. auth.txt should have the format of:
<pre>
domain.com<br>
adminuser<br>
password<br>
</pre>
where domain.com is your Google Apps domain, adminuser is your admin username (not full email) and password is that user's password. If GAM finds auth.txt it will use it to create a token file instead of prompting you to enter these details meaning GAM will always just work (assuming the credentials are valid).