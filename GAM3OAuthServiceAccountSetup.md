<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](http://doctoc.herokuapp.com/)*

- [Introduction](#introduction)
- [Steps](#steps)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Introduction

In order to use some of the new GAM 3.0 Calendar, Drive and (coming soon Google+) commands, Google requires you to setup a service account. You can then authorize this service account to act on behalf of your Google Apps account and all users. This is the OAuth 2.0 equivalent of Two-Legged OAuth 1.0a.

# Steps

1. You can access the API Console at:

[https://code.google.com/apis/console](https://code.google.com/apis/console)

you'll need to be logged in to your Google Account.

2. Click Create Project to get started.
<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/Create-Project.png'>

3. Click "OFF" next to Calendar API, Drive API and Drive SDK to toggle them ON.<br>
<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2012-12-12_1331.png'>

5. Click the "API Access" link to the left.<br>
<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2011-11-10_1553_001.png'>

6. Click "Create an OAuth 2.0 Client ID".<br>
<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2011-11-10_1554.png'>

7. Give a name for your Client ID. "GAM" is fine. Hit Next.<br>
<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2011-11-10_1554_001.png'>

8. Select "Service Account" then hit "Create Client ID".<br>
<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/oauth-service-account.png'>

9. Now download the private key. The downloaded file will have a long name of random characters but before or after downloading it, you should rename it to "oauth2service.p12" and save the file to the same location as gam.exe or gam.py. This key is extremely important! Keep it secure as it provides full access to your service account and whatever APIs you've granted the service account access to.<br>
<br>
10. Also take note of the Client ID and Email address for your Service Account. You'll need these in the steps below.<br>
<br>
11. Log in to your Google Apps Control Panel and navigate to:<br>
<br>
<ul><li>New Admin console: Security > Advanced settings > Authentication > Manage third party OAuth Client access<br>
</li><li>Classic Admin console: Advanced Tools > Manage third party OAuth Client access (under the Authentication section)</li></ul>

12. For Client Name, enter the Client ID you entered above.<br>
<br>
13. For One or More API Scopes, enter:<br>
<br>
<pre><code>https://www.googleapis.com/auth/calendar,https://www.googleapis.com/auth/drive<br>
</code></pre>

these scopes give the Service Account full access to Calendar and Drive data for all users in your Google Apps account. Hit Authorize. The Client ID should now be listed below along with the API scopes you authorized.<br>
<br>
14. Now that the Service Account is created and authorized to access your domain data, we can switch back to GAM. Try running:<br>
<br>
<pre><code>gam user &lt;non admin user email&gt; show calendars<br>
</code></pre>

you will immediately be prompted for the email address of your service account. Copy and Paste the email address from above into GAM. You'll only need to do this once. Once the email address is entered, you'll be able to perform Calendar and Drive GAM operations that require service account authentication!