## Creating the client\_secrets.json and oauth2service.json files for GAM
To use GAM, you need to create your own client\_secrets.json and oauth2service.json files. These give you your own personal quota of API requests.

See these [YouTube videos](https://goo.gl/slo06E) for a demonstration of the process of creating the credentials and authorizing the required API scopes.

## Steps

1. Log into Google Apps. The account does not need to be in your Google Apps domain or have any special rights.
1. Create a Google API Project 
    1. point your web browser to [console.developers.google.com](http://console.developers.google.com)
        * these instructions are for the newest version of the Developer's console.  In some domains, it may still be the "beta" version
    1. click on `Select a project` and choose `Create a project` 
![gam-31](https://cloud.githubusercontent.com/assets/1683475/11098097/51366f22-8868-11e5-929a-601fa481fcc4.png)
    1. enter a project name.  Make the name distinctive and easily identifiable as a GAM project.  The name must be between 4 and 30 characters 
![gam02](https://cloud.githubusercontent.com/assets/1683475/11096331/07cda872-885f-11e5-9061-f7db2e18183b.png)
    1. if required, select an email preference and check the box to agree to the terms 
    1. click the `Create` button
    1. within a few second, your project will be created and the web page will switch to that project
1. Authorize specific APIs to work with GAM
    1. in the center of the screen, click on `Enable and manage APIs` 
![gam-33](https://cloud.githubusercontent.com/assets/1683475/11098098/5136c472-8868-11e5-9f11-31af28aafb16.png)
    1. near the top of the next window, click on `Enabled APIs` 
![gam04](https://cloud.githubusercontent.com/assets/1683475/11096332/07cf5492-885f-11e5-9793-3fc0651a0e31.png)
    1. some APIs are enabled for all projects by default.  GAM does not use any of them, so disable them
        1. at the far right of each listed API, click the `Disable` button 
![gam05](https://cloud.githubusercontent.com/assets/1683475/11096333/07d4dcc8-885f-11e5-974e-80e374e98fc2.png)
        1. in the pop-up dialog, click `Disable` to confirm 
![gam06](https://cloud.githubusercontent.com/assets/1683475/11096311/07a59c42-885f-11e5-802a-08beea16ffa3.png)
        1. wait for the API to be disabled
        1. repeat for all listed APIs
    1. near the top of the page, click on `Google APIs` 
![gam07](https://cloud.githubusercontent.com/assets/1683475/11096309/07a487f8-885f-11e5-99ef-487cdfdeb496.png)
    1. enable the APIs listed below
        1. in the search box, start typing the the first few letters of the name of an API, then click on that API
        1. in the next screen, click on `Enable API` 
![gam08](https://cloud.githubusercontent.com/assets/1683475/11096310/07a599a4-885f-11e5-9896-23364582e79a.png)
        1. when the screen confirms that the API is enabled, click the arrow to return to the list of all Google APIs
        1. repeat for each API listed below 
    1. near the top of the window, click on `Enabled APIs` again and verify that you have enabled all of the required APIs  
![gam09](https://cloud.githubusercontent.com/assets/1683475/11096313/07a72ae4-885f-11e5-8041-861e48f60af0.png)
    1. Required APIs:
        * Admin SDK
        * Apps Activity API
        * Calendar API
        * Drive API
        * Enterprise License Manager API
        * Gmail API
        * Google Classroom API (Google for Education domains only)
        * Groups Settings API
1. Create the Credentials files
    1. create client_secrets.json
        1. in the left side menu, click on `Credentials`
        1. in the center of the screen, click on `Add credentials` and choose OAuth 2.0 client ID  
![gam12](https://cloud.githubusercontent.com/assets/1683475/11096315/07b0ce00-885f-11e5-86dc-b84d3c2e94c5.png)
        1. you will be prompted to enter a product name on the consent screen.  Click the `Configure consent screen` button 
![gam-35](https://cloud.githubusercontent.com/assets/1683475/11098100/51467d40-8868-11e5-8511-62086b45ac1c.png)
        1. enter a _Product name_.  It can be the same project name that you used previously  
![gam11](https://cloud.githubusercontent.com/assets/1683475/11096312/07a61654-885f-11e5-9697-cb581fe094fe.png)
        1. at the bottom of the screen, click `Save` 
        1. on the next screen, choose `Application type Other`, enter a name, and click `Create`.  
![gam-36](https://cloud.githubusercontent.com/assets/1683475/11098096/5134ff2a-8868-11e5-9f20-1c36b8720bf1.png) 
        1. in the next window, enter a name for the client.  You can use the same name as the project.  
![gam-37](https://cloud.githubusercontent.com/assets/1683475/11098095/5133dc44-8868-11e5-9025-deb568d793db.png)
        1. click the `Save` button.
        1. in the pop-up confirmation window, click `OK`.  You do not need to record the client ID or client secret
        1. on the next screen, click the name of the project 
![gam13](https://cloud.githubusercontent.com/assets/1683475/11096316/07b12562-885f-11e5-9d9a-d6c7721f1b2d.png)
        1. on the next screen, near the top of the page click on `Download JSON`
        1. save the file to the same folder as GAM.exe or GAM.py and rename the file to *`client_secrets.json`*  
![gam15](https://cloud.githubusercontent.com/assets/1683475/11096317/07b2dac4-885f-11e5-9283-bd7cc7141aff.png)
        1. at the top of the screen, click the arrow button to return to the `Credentials` screen
    1. create oauth2service.json
        1. click `Add credentials` and select `Service account` 
![gam17](https://cloud.githubusercontent.com/assets/1683475/11096318/07b2f450-885f-11e5-9597-c71cdcf13ecf.png)
        1. select the `JSON` key type and click `Create` 
![gam18](https://cloud.githubusercontent.com/assets/1683475/11096319/07b390a4-885f-11e5-859a-b96e8b4376dc.png)
        1. a file download will start automatically.  Save the file to the same folder as GAM.exe or GAM.py and rename the file to *`oauth2service.json`* 
![gam19](https://cloud.githubusercontent.com/assets/1683475/11096321/07bd277c-885f-11e5-9aeb-07df368265e2.png)
        1. in the pop-up dialog, click `Close`
1. Run GAM to authorize the configuration
    1. open a command line window and navigate to the folder that contains gam.exe or gam.py
    1. run the command `gam info domain`
    1. the configuration options will be displayed.  All API scopes will be selected by default. Choose the last option in the list (`Continue`): type its option number and press `Enter`.  
![gam20](https://cloud.githubusercontent.com/assets/1683475/11096320/07ba411a-885f-11e5-9b68-2956e3b44475.png)
    1. a browser window will open to display the confirmation screen.  
        1. if the computer that you are running GAM on does not have a web browser, you can use a browser on another computer to complete this step.  On the other computer, enter the goo.gl short URL that is displayed in the command line window  
![gam22](https://cloud.githubusercontent.com/assets/1683475/11096324/07c046f0-885f-11e5-9ece-2cc76b4bb59d.png)
    1. scroll to the bottom of the list of permissions and click `Allow` 
![gam21](https://cloud.githubusercontent.com/assets/1683475/11096323/07be2bc2-885f-11e5-9822-35a6cd35b8e9.png)
    1. the web page will report that the authentication flow has completed.
    1. in the command line window, the GAM command will complete, and you will see information about the Google Apps domain
1. Authorize the API scopes for use with GAM in the Admin Console
    1. Authorize scopes for OAuth2
        1. in the Developer’s console [console.developers.google.com](http://console.developers.google.com), in the left side menu click on `Credentials`
        1. select to the project you just created
        1. in the `OAuth 2 client IDs` section, click and drag to select the `Client ID` and copy it (Control/Command-C).  The Client ID is a long string of numbers and/or letters. 
![gam-40](https://cloud.githubusercontent.com/assets/1683475/11100314/130210ae-8876-11e5-9659-a902e4d929cf.png)
        1. in another browser window or tab, log into Google Apps using a domain super-admin account
        1. go to the [Gogle Apps Admin Console](http://admin.google.com)
        1. click the `Security` icon  
![gam23](https://cloud.githubusercontent.com/assets/1683475/11096322/07bd8492-885f-11e5-9365-55a2dead8455.png)
        1. in the Security console, click on `Show more`, then `Advanced settings`, then `Manage API client access`
        1. near the top of the screen, paste the Client ID into the field labeled `Client Name`
        1. select the entire list of _API scopes - OAuth2_ below, copy it (Control/Command-C) and paste it into the field labeled `One or More API Scopes` on the Admin Console screen
        1. click the `Authorize` button 
![gam26](https://cloud.githubusercontent.com/assets/1683475/11096329/07c82474-885f-11e5-9741-90121987b508.png)
        1. in the list of projects and scopes, the Client ID will appear in the left column and the list of API scopes will appear in the right column 
![gam27](https://cloud.githubusercontent.com/assets/1683475/11096328/07c8fe30-885f-11e5-8db3-62cdd06bd626.png)
    1. Authorize scopes for the service account
        1. in the Developer's Console, return to the screen with the project's credentials listed
        1. in the Service Account section, click on the service account
![gam-41](https://cloud.githubusercontent.com/assets/1683475/11100312/12fcd54e-8876-11e5-8252-6d721f9eb28e.png)
        1. in the next screen, click and drag to select the Service Account's client ID and copy it (Control/Command-C).  The client ID is a long string of long string of numbers and/or letters (but may not the same client ID as the OAuth client ID)
![gam-42](https://cloud.githubusercontent.com/assets/1683475/11100313/12ff4c02-8876-11e5-8a30-124985678a3d.png)
        1. switch to the Admin Console and paste the client ID into the field labeld `Client Name`
        1. select the entire list of _API scopes - Service Account_ below, copy it (Control/Command-C) and paste it into the field labeled `One or More API Scopes` on the Admin Console screen
        1. click the `Authorize` button 

GAM is now ready for use.


API scopes - OAuth2:

````
https://www.googleapis.com/auth/calendar, 
https://mail.google.com/, 
https://www.googleapis.com/auth/activity, 
https://www.googleapis.com/auth/drive, 
https://www.googleapis.com/auth/plus.login, 
https://www.googleapis.com/auth/plus.me, 
https://www.googleapis.com/auth/siteverification, 
https://www.googleapis.com/auth/cloudprint, 
https://www.googleapis.com/auth/classroom.rosters, 
https://www.googleapis.com/auth/classroom.courses, 
https://www.googleapis.com/auth/classroom.profile.emails, 
https://www.googleapis.com/auth/classroom.profile.photos, 
https://www.googleapis.com/auth/admin.datatransfer, 
https://www.googleapis.com/auth/admin.directory.customer, 
https://www.googleapis.com/auth/admin.directory.domain
````

API scopes - Service Account:

````
https://mail.google.com/,
https://www.googleapis.com/auth/activity,
https://www.googleapis.com/auth/calendar,
https://www.googleapis.com/auth/drive
````


From time to time, Google changes one or more of the tools used in this process.  Some of the steps may change, or what you see on the screen may differ from what is shown here.  Please post a comment in the discussion forum if you find an outdated or incorrect instruction (or just fix it - anyone can edit the wiki).