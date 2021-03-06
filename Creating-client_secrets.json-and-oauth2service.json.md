<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](http://doctoc.herokuapp.com/)*

- [Creating Your Own OAuth Console clients\_secrets.json](#creating-your-own-oauth-console-clients\_secretsjson)
- [Steps](#steps)
- [Creating Your Own OAuth2service.json](# Creating Your Own OAuth2service.json)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Creating Your Own OAuth Console clients\_secrets.json
In the past, all GAM installations shared the same client\_secrets.json file included with the GAM download. This file identifies the GAM project to Google but it does not provide any special access rights to your Google Apps domain (that's what the oauth2.txt file is for).

With GAM versions 3.02 and higher, you need to create your own client\_secrets.json file. This gives you your own personal quota of API requests to be used.

# Steps

1. You can access the API Console at
<a href='https://cloud.google.com/console' target='_blank'>https://cloud.google.com/console</a>
you'll need to be logged in to your Google Account. The account does not need to be in your Google Apps domain or have any special rights.

1. Click the big red "Create Project" button to get started.

1. Give your project a name and id as you prefer.<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1223.png'>

1. You may be prompted to verify via SMS. Complete SMS verification before continuing.

1. Click the "API & auth" link to the left.<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1227.png'>

1. Enable the Admin SDK by clicking the OFF button so that it turns to on. If you're prompted with terms of service, accept them.<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1228.png'>

1. Also enable Calendar API, Drive API, Drive SDK, Enterprise License Manager API and Group Settings API accepting terms of service whenever prompted. The services that were on by default (BigQuery API, etc) can be left alone or turned off, GAM does not use them.<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1231.png'>

1. Click "Consent screen to the left, enter a PRODUCT NAME and SAVE your changes.<br><br><img src='https://googledrive.com/host/0B16ur9NKHJwBd2o4ZDdudG5lWlk/consent_screen.png'>

1. Click "Credentials to the left.<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1231_001.png'>

1. Click the "CREATE NEW CLIENT ID" red button.<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1231_002.png'>

1. Choose "Installed Application" for Application Type.<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1232_001.png'>

1. Choose "Other" for Installed Application Type.<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1233.png'>

1. Under "Client ID for Native Application", click the red "Download JSON" button. Make sure you are clicking the download button under "Client ID for Native Application"!<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1234.png'>

1. Name your file "client_secrets.json" and put it in the exact same path as gam.py or gam.exe.

1. You can confirm which Project your GAM authorization is using by running:<br><br>gam oauth info<br><br><b>380063494358.apps.googleusercontent.com</b> is the Client ID for the client_secrets.json that came with old versions of the GAM download. If you see it, you're not using your own project, run "gam oauth revoke" to delete the existing oauth2.txt authorization and then "gam info domain" to redo the authorization with your own project.

# Creating Your Own OAuth2service.json

1. Starting from the end of the previous step after creating your client_secrets.json file, Below the section for the Installed applications, click on Create another client ID…<br><br><img src='https://googledrive.com/host/0B9ltla5VOI4-bWZHWXljbHVwNDA/gam13.png'>

1. On the next screen select Application type: Service account
1. Click Create Client ID <br><br><img src='https://googledrive.com/host/0B9ltla5VOI4-bWZHWXljbHVwNDA/gam14.png'>
1. Click Download private key then save this file as oauth2service.p12 and save it in the same folder as your GAM installation, same place that you saved your client_secrets.json file then close the dialog window. <br><br><img src='https://googledrive.com/host/0B9ltla5VOI4-bWZHWXljbHVwNDA/gam16.png'>
1. Navigate to the section of the page for the Service Account, and then click on Download JSON, save the file to the same folder as your GAM installation and rename it to oauth2service.json
1. In the section for the Service Account, copy your Client ID to the clipboard <br><br><img src='https://googledrive.com/host/0B9ltla5VOI4-bWZHWXljbHVwNDA/gam17.png'>
1. In a new browser window, go to the Google Apps Admin dashboard (admin.google.com) and navigate to the Security Icon, click Show More then Advanced settings, and under the Authentication section click on Manage API client access.  <br><br><img src='https://googledrive.com/host/0B9ltla5VOI4-bWZHWXljbHVwNDA/gam18.png'>
1. Click in the Client Name field at the top left and paste in the OAuth2 Client ID that you copied to the clipboard previously <br><br><img src='https://googledrive.com/host/0B9ltla5VOI4-bWZHWXljbHVwNDA/gam19.png'>
1. Next paste the following text into the One or More API Scopes field and click Authorize:
`https://www.googleapis.com/auth/calendar,https://www.googleapis.com/auth/drive`<br><br><img src='https://googledrive.com/host/0B9ltla5VOI4-bWZHWXljbHVwNDA/gam20.png'>
1. You should now be setup with your OAuth2service.json and be able to access the Drive and Calendar Commands.

