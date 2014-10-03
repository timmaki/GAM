<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](http://doctoc.herokuapp.com/)*

- [Introduction](#introduction)
- [Steps](#steps)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Introduction

In order to use the new Group Settings API. Google requires you to get a Client ID and Secret. You will be prompted to enter these when setting up GAM authentication on GAM version 2.0 and greater.

# Steps

1. You can access the API Console at:

[https://code.google.com/apis/console](https://code.google.com/apis/console)

you'll need to be logged in to your Google Account.

2. Click Create Project to get started.
<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/Create-Project.png'>

3. Click "OFF" next to Groups Settings API to toggle it ON.<br>
<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2012-12-12_1331.png'>

4. Check "I agree to these terms" and click Accept (you'll do this twice)<br>
<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2012-12-12_1331_001.png'>

5. Click the "API Access" link to the left.<br>
<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2011-11-10_1553_001.png'>

6. Click "Create an OAuth 2.0 Client ID".<br>
<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2011-11-10_1554.png'>

7. Give a name for your Client ID. "GAM" is fine. Hit Next.<br>
<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2011-11-10_1554_001.png'>

8. Select "Installed Application" and "Other" then hit "Create Client ID".<br>
<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2012-12-12_1333.png'>

9. Finally, you'll have your Client ID and secret that can be plugged in to GAM. You can revoke your current OAuth token in order to be prompted again by running "gam oauth revoke" then running another GAM command like "gam info domain". Don't use the values listed in the image below. They are samples only and won't work!<br>
<br><br><img src='https://www.googledrive.com/host/0B8mlDZR33yTdcm12SGNnd3MzeDA/2011-11-10_1555.png'>