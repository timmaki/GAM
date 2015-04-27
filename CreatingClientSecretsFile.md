# Creating Your Own OAuth Console client\_secrets.json
In the past, all GAM installations shared the same client\_secrets.json file included with the GAM download. This file identifies the GAM project to Google but it does not provide any special access rights to your Google Apps domain (that's what the oauth2.txt file is for).

Also have created steps below to create the OAuth2services.json file as well which enables commands for Drive and Calendar

With GAM versions 3.02 and higher, you need to create your own client\_secrets.json file. This gives you your own personal quota of API requests to be used.

# Steps

  1. You can access the API Console at<br><br><a href='https://cloud.google.com/console'>https://cloud.google.com/console</a><br><br>you'll need to be logged in to your Google Account. The account does not need to be in your Google Apps domain or have any special rights.<br><br>
<ol><li>Click the big red "Create Project" button to get started.<br><br>
</li><li>Give your project a name and id as you prefer.<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1223.png'><br><br>
</li><li>You may be prompted to verify via SMS. Complete SMS verification before continuing.<br><br>
</li><li>Click the "API & auth" link to the left.<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1227.png'><br><br>
</li><li>Enable the Admin SDK by clicking the OFF button so that it turns to on. If you're prompted with terms of service, accept them.<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1228.png'><br><br>
</li><li>Also enable Apps Activity API, Calendar API, Drive API, Drive SDK, Enterprise License Manager API, Gmail API, Groups Settings API and Site Verification API, accepting terms of service whenever prompted. The services that were on by default (BigQuery API, etc) can be left alone or turned off, GAM does not use them.<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1231.png'><br><br>
</li><li><b>Click</b> 'Consent screen' under 'APIs & auth' on the left.<br><br><img src='https://dl.dropboxusercontent.com/u/5024956/Screen%20Shot%202014-10-07%20at%204.03.30%20PM.png' height='300'><br><br>
</li><li>If the values on this screen are empty, <b>select</b> an email address and type in a product name, then click <b>Save</b>. If there are already values, you can move to the next step.<br><br><img src='https://dl.dropboxusercontent.com/u/5024956/Screen%20Shot%202014-10-07%20at%204.03.44%20PM.png'><br><br>
</li><li>Click "Credentials" to the left.<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1231_001.png'><br><br>
</li><li>Click the "CREATE NEW CLIENT ID" red button.<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1231_002.png'>
</li><li>Choose "Installed Application" for Application Type.<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1232_001.png'><br><br>
</li><li>Choose "Other" for Installed Application Type.<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1233.png'><br><br>
</li><li>Under "Client ID for Native Application", click the red "Download JSON" button. Make sure you are not clicking the wrong button!<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1234.png'><br><br>
</li><li>Name your file "client_secrets.json" and put it in the exact same path as gam.py or gam.exe.<br>
</li><li>You can confirm which Project your GAM authorization is using by running:<br><br>gam oauth info<br><br><b>380063494358.apps.googleusercontent.com</b> is the Client ID for the client_secrets.json that comes with the GAM download. If you see it, you're not using your own project, run "gam oauth revoke" to delete the existing oauth2.txt authorization and then "gam info domain" to redo the authorization with our own project.

# Creating Your Own OAuth2service.json

1. Starting from the end of the previous step after creating your client_secrets.json file, Below the section for the Installed applications, click on Create another client ID…<br><br><img src='https://googledrive.com/host/0B9ltla5VOI4-bWZHWXljbHVwNDA/gam13.png'>

1. On the next screen select Application type: Service account
1. Click Create Client ID <br><br><img src='https://googledrive.com/host/0B9ltla5VOI4-bWZHWXljbHVwNDA/gam14.png'>
1. Navigate to the section of the page for the Service Account, and then click on Download JSON, save the file to the same folder as your GAM installation and rename it to oauth2service.json
1. In the section for the Service Account, copy your Client ID to the clipboard <br><br><img src='https://googledrive.com/host/0B9ltla5VOI4-bWZHWXljbHVwNDA/gam17.png'>
1. In a new browser window, go to the Google Apps Admin dashboard (admin.google.com) and navigate to the Security Icon, click Show More then Advanced settings, and under the Authentication section click on Manage API client access.  <br><br><img src='https://googledrive.com/host/0B9ltla5VOI4-bWZHWXljbHVwNDA/gam18.png'>
1. Click in the Client Name field at the top left and paste in the OAuth2 Client ID that you copied to the clipboard previously <br><br><img src='https://googledrive.com/host/0B9ltla5VOI4-bWZHWXljbHVwNDA/gam19.png'>
1. Next paste the following text into the One or More API Scopes field and click Authorize:
`https://www.googleapis.com/auth/calendar,https://www.googleapis.com/auth/drive,https://www.googleapis.com/auth/activity,https://mail.google.com/,https://www.googleapis.com/auth/siteverification`<br><br><img src='https://googledrive.com/host/0B9ltla5VOI4-bWZHWXljbHVwNDA/gam20.png'>
1. You should now be set up with your `OAuth2service.json` and be able to access the Drive and Calendar Commands.