# Introduction

In order to use some of the new GAM 3.0 Calendar, Drive and (coming soon Google+) commands, Google requires you to setup a service account. You can then authorize this service account to act on behalf of your Google Apps account and all users. This is the OAuth 2.0 equivalent of the (deprecated) Two-Legged OAuth 1.0a.

# Steps

1. You can access the Google Cloud Console at:

[https://cloud.google.com/console](https://cloud.google.com/console)

you'll need to be logged in to a Google Account.

2. Click Create Project.

<br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2013-11-22_1224.png'>


3. Give your project a name and ID.<br>
<br>
<br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2013-11-22_1224_001.png'>


4. Click "APIs & auth" to the left.<br>
<br>
<br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2013-11-22_1228.png'>


5. Click the green "ON" button for any service that have been pre-enabled in order to turn them off.<br>
<br>
<br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2013-11-22_1231.png'>


6. Click the gray "OFF" button for Calendar API, Drive API, Drive SDK, Google+ API and Google+ Domains API to toggle them "ON". Accept any terms of service that may appear. Confirm each service is listed at the top and is on.<br>
<br>
<br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2013-11-22_1233.png'>


7. Click the "Credentials" link to the left.<br>
<br>
<br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1231_001.png'>


8. Click the red "Create New Client ID" button.<br>
<br>
<br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-04-02_0907_001.png'>


9. Give your app a name. Ensure "Service account" is selected and click the blue "Register" button.<br>
<br>
<br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-04-02_0908.png'>


10. Save the downloaded file with a name of "oauth2service.p12" in the same folder/directory as gam.exe or gam.py.<br>
<br>
<br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-04-02_0908_001.png'>

11. <b>Underneath the Service Account area</b>, click the "Download JSON" button and save the file with a name of "oauth2service.json" in the same folder/directory as gam.exe or gam.py.<br>
<br>
<br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-04-02_0909.png'>


12. Now from the GAM, try running your GAM command that requires a Service Account. An example command would be:<br>
<br>
<b>gam all users show calendars</b>


13. GAM will print out an error. The error shows the Client Name of your OAuth Service Account as well as the scopes that are needed for the given command. Follow GAM's instructions to grant your Service Account access to your Google Apps domain in the Control Panel.