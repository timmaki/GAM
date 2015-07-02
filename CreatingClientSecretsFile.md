# Creating Your Own OAuth Console client\_secrets.json
To use GAM, you need to create your own client\_secrets.json and oauth2service.json filse. These give you your own personal quota of API requests.

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
1. 