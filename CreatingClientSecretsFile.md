<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](http://doctoc.herokuapp.com/)*

- [Creating Your Own OAuth Console clients\_secrets.json](#creating-your-own-oauth-console-clients\_secretsjson)
- [Steps](#steps)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Creating Your Own OAuth Console clients\_secrets.json
In the past, all GAM installations shared the same client\_secrets.json file included with the GAM download. This file identifies the GAM project to Google but it does not provide any special access rights to your Google Apps domain (that's what the oauth2.txt file is for).

With GAM versions 3.02 and higher, you need to create your own client\_secrets.json file. This gives you your own personal quota of API requests to be used.

# Steps

  1. You can access the API Console at<br><br><a href='https://cloud.google.com/console'>https://cloud.google.com/console</a><br><br>you'll need to be logged in to your Google Account. The account does not need to be in your Google Apps domain or have any special rights.<br><br>
<ol><li>Click the big red "Create Project" button to get started.<br><br>
</li><li>Give your project a name and id as you prefer.<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1223.png'><br><br>
</li><li>You may be prompted to verify via SMS. Complete SMS verification before continuing.<br><br>
</li><li>Click the "API & auth" link to the left.<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1227.png'><br><br>
</li><li>Enable the Admin SDK by clicking the OFF button so that it turns to on. If you're prompted with terms of service, accept them.<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1228.png'><br><br>
</li><li>Also enable Calendar API, Drive API, Drive SDK, Enterprise License Manager API and Group Settings API accepting terms of service whenever prompted. The services that were on by default (BigQuery API, etc) can be left alone or turned off, GAM does not use them.<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1231.png'><br><br>
</li><li>Click 'Consent screen' under 'APIs & auth' on the left.<br><br><img src='https://www.dropbox.com/s/ewxmcxx8aqvoce6/Screen%20Shot%202014-10-07%20at%204.03.30%20PM.png'><br><br>
</li><li>If the values on this screen are empty, select an email address and type in a product name, then click Save. If there are already values, you can move to the next step.<br><br><img src='https://www.dropbox.com/s/pokjg8xcr9dxqts/Screen%20Shot%202014-10-07%20at%204.03.44%20PM.png'><br><br>
</li><li>Click "Credentials" to the left.<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1231_001.png'><br><br>
</li><li>Click the "CREATE NEW CLIENT ID" red button.<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1231_002.png'>
</li><li>Choose "Installed Application" for Application Type.<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1232_001.png'><br><br>
</li><li>Choose "Other" for Installed Application Type.<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1233.png'><br><br>
</li><li>Under "Client ID for Native Application", click the red "Download JSON" button. Make sure you are not clicking the wrong button!<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1234.png'><br><br>
</li><li>Name your file "client_secrets.json" and put it in the exact same path as gam.py or gam.exe.<br>
</li><li>You can confirm which Project your GAM authorization is using by running:<br><br>gam oauth info<br><br><b>380063494358.apps.googleusercontent.com</b> is the Client ID for the client_secrets.json that comes with the GAM download. If you see it, you're not using your own project, run "gam oauth revoke" to delete the existing oauth2.txt authorization and then "gam info domain" to redo the authorization with our own project.