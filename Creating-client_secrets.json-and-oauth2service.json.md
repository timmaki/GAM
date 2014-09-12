# Creating Your Own OAuth Console clients\_secrets.json
In the past, all GAM installations shared the same client\_secrets.json file included with the GAM download. This file identifies the GAM project to Google but it does not provide any special access rights to your Google Apps domain (that's what the oauth2.txt file is for).

With GAM versions 3.02 and higher, you need to create your own client\_secrets.json file. This gives you your own personal quota of API requests to be used.

# Steps

<ol><li>You can access the API Console at
<a href='https://cloud.google.com/console' target='_blank'>https://cloud.google.com/console</a>
you'll need to be logged in to your Google Account. The account does not need to be in your Google Apps domain or have any special rights.</li>

<li>Click the big red "Create Project" button to get started.</li>

<li>Give your project a name and id as you prefer.
<img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1223.png'></li>

<li>You may be prompted to verify via SMS. Complete SMS verification before continuing.</li>

<li>Click the "API & auth" link to the left.
<img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1227.png'></li>

<li>Enable the Admin SDK by clicking the OFF button so that it turns to on. If you're prompted with terms of service, accept them.
<img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1228.png'></li>

<li>Also enable Calendar API, Drive API, Drive SDK, Enterprise License Manager API and Group Settings API accepting terms of service whenever prompted. The services that were on by default (BigQuery API, etc) can be left alone or turned off, GAM does not use them.
<img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1231.png'></li>

<li>Click "Credentials to the left.
<img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1231_001.png'></li>

<li>Click the "CREATE NEW CLIENT ID" red button.
<img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1231_002.png'></li>

<li>Choose "Installed Application" for Application Type.
<img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1232_001.png'></li>

<li>Choose "Other" for Installed Application Type.

<img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1233.png'></li>

<li>Under "Client ID for Native Application", click the red "Download JSON" button. Make sure you are not clicking the wrong button!

<img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2014-01-31_1234.png'></li>

<li>Name your file "client_secrets.json" and put it in the exact same path as gam.py or gam.exe.</li>

<li>You can confirm which Project your GAM authorization is using by running:

gam oauth info

<b>380063494358.apps.googleusercontent.com</b> is the Client ID for the client_secrets.json that comes with the GAM download. If you see it, you're not using your own project, run "gam oauth revoke" to delete the existing oauth2.txt authorization and then "gam info domain" to redo the authorization with your own project.