# Creating the client\_secrets.json and oauth2service.json files for GAM
To use GAM, you need to create your own client\_secrets.json and oauth2service.json files. These give you your own personal quota of API requests.

See these [YouTube videos](https://goo.gl/slo06E) for a demonstration of the process: https://goo.gl/slo06E

# Steps

1. You can access the API Console at:
[https://console.developers.google.com](https://console.developers.google.com)
you'll need to be logged in to a Google Account. The account does not need to be in your Google Apps domain or have any special rights.  
1. At the top left, click "Select a project" and then "Create a project..." to get started.
![nimbus-image-1435848805271](https://cloud.githubusercontent.com/assets/4623536/8480856/0cca9682-20ae-11e5-8359-03392dcf732c.png)  
1. Give your project a name like "GAM for MyOrg", agree to the terms and click Create.  
![nimbus-image-1435848937421](https://cloud.githubusercontent.com/assets/4623536/8480855/0cca3cf0-20ae-11e5-86f7-498c34c65919.png)  
1. To the left, under "APIs & auth" click "APIs"  
![nimbus-image-1435849229438](https://cloud.githubusercontent.com/assets/4623536/8480858/0ccd087c-20ae-11e5-94dd-5145b2464216.png)  
1. Search for and Enable the following APIs:
  * Admin SDK
  * Calendar API
  * Classroom API
  * Drive API
  * Enterprise License Manager API
  * Gmail API
  * Groups Settings API
![nimbus-image-1435849333678](https://cloud.githubusercontent.com/assets/4623536/8480857/0ccb438e-20ae-11e5-8cd9-a58d6460632f.png)  
1. To the left, under "APIs & auth", click "Consent screen".  
![nimbus-image-1435849384782](https://cloud.githubusercontent.com/assets/4623536/8480853/0cc9b24e-20ae-11e5-8bb5-42eb1d65f717.png)  
1. For "Product Name", enter something like "GAM for MyOrg". All other fields are optional and can be left alone. Click Save.  
![nimbus-image-1435849457377](https://cloud.githubusercontent.com/assets/4623536/8480854/0cc9b7f8-20ae-11e5-9439-c00fb016c6e6.png)  
1. To the left, under "APIs & auth", click "Credentials".  
![nimbus-image-1435849514389](https://cloud.githubusercontent.com/assets/4623536/8480851/0cc2f7e2-20ae-11e5-8b3e-70de1d963ddd.png)  
1. Click "Create new Client ID".  
![nimbus-image-1435849560906](https://cloud.githubusercontent.com/assets/4623536/8480847/0cc0dc6e-20ae-11e5-90b5-07a440279124.png)  
1. Choose "Installed application", "Other" and then click "Create Client ID".  
![nimbus-image-1435849621190](https://cloud.githubusercontent.com/assets/4623536/8480850/0cc21854-20ae-11e5-8c77-3b077f03013c.png)  
1. Click "Download JSON".  
![nimbus-image-1435849670307](https://cloud.githubusercontent.com/assets/4623536/8480849/0cc21eda-20ae-11e5-8c3f-4b783da98132.png)  
1. Name the file "client_secrets.json (Note the S at the end of secrets) and save it to the same folder as your GAM installations gam.py or gam.exe.  
![nimbus-image-1435849777799](https://cloud.githubusercontent.com/assets/4623536/8480852/0cc37064-20ae-11e5-8266-d4fc68a4c779.png)
1. For a 2nd time, click "Create new Client ID".
![nimbus-image-1435849560906](https://cloud.githubusercontent.com/assets/4623536/8480847/0cc0dc6e-20ae-11e5-90b5-07a440279124.png)  
1. This time, choose "Service Account", "JSON Key" and "Create Client ID".  
![nimbus-image-1435849866247](https://cloud.githubusercontent.com/assets/4623536/8480848/0cc1b67a-20ae-11e5-8365-aadd319217b8.png)  
1. You will be prompted to save another file. Name the file "oauth2service.json" and save it to the same folder as gam.exe or gam.py.  
![nimbus-image-1435850026256](https://cloud.githubusercontent.com/assets/4623536/8480846/0cb85eb8-20ae-11e5-9dac-0b11d8703b0f.png)  