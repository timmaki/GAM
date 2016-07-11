
## Creating the client\_secrets.json and oauth2service.json files for GAM
To use GAM, you need to create your own client\_secrets.json and oauth2service.json files. These give you your own personal quota of API requests.

## Steps

1. Enable API access for Google Apps. This step requires a domain super-admin account or an account with delegated Security rights
    1. in the domain's Admin Console, go to the `Security` section, then click on `API reference`
![gam-30](https://cloud.githubusercontent.com/assets/1683475/11548007/02d69214-991e-11e5-8595-3ea6083776ab.png)
    1. if API access is not already enabled:
            1. click to check the box for `Enable API access`
            1. click the `Save` button
1. Login to a Google account. The account does not need to be in your Google Apps domain or have any special rights.
1. Create a Google API Project 
    1. Go to <a href="https://console.developers.google.com/flows/enableapi?apiid=admin,appsactivity,calendar,classroom,drive,gmail,groupssettings,licensing,plus" target="_blank">**this link**</a> to start.  This link will begin the project creation process, and specifies the APIs that must be included in the project.<br />
![gam-101](https://cloud.githubusercontent.com/assets/1683475/14234019/b7cfce9e-f99d-11e5-8ee0-9022f71c0301.png)
    1. Verify that `Create a new project` is selected
    1. click the `Continue` button
    1. within a few second, your project will be created and the screen will display a confirmation message. On the confirmation screen, verify that all of the required APIs are included.  (Other APIs may also be enabled.  You may ignore them.)
    1. Required APIs:
        * Admin SDK
        * Apps Activity API
        * Calendar API
        * Drive API
        * Enterprise License Manager API
        * Gmail API
        * Google Classroom API (Google for Education domains only)
        * Groups Settings API
        * Google+ API
    1. Click on `Go to credentials`.<br />
![gam-103](https://cloud.githubusercontent.com/assets/1683475/14234014/b7c827d4-f99d-11e5-9fd9-75f9f08566a0.png)
1. Rename the project.
    1. by default, the new project will be named `My Project` or something similar.  The project should be renamed so that you will know that it is a GAM project.
    1. near the top right of the screen, click on the project selection menu. (The menu may be labeled `Go to project` or may be the name of a specific project.)<br />
![gam-104](https://cloud.githubusercontent.com/assets/1683475/14234015/b7cef2a8-f99d-11e5-8020-f56ca86ffa80.png)
    1. a list of all active projects will be displayed.  Find the line for the project just created.  At the far right of that line, click on the pencil icon to re-name the project.
![gam-105](https://cloud.githubusercontent.com/assets/1683475/14234017/b7cf53f6-f99d-11e5-8aff-3dcde1ae89eb.png)
    1. choose a name that is meaningful to you and identifies the project as a GAM project.
![gam-107](https://cloud.githubusercontent.com/assets/1683475/14234018/b7cf7700-f99d-11e5-8488-b357eaef8b00.png)
1. Create the Credentials files
    1. create client_secrets.json
        1. in the left side menu, click on `Credentials`
        1. in the top menu, click on `OAuth consent screen`
![gam-50](https://cloud.githubusercontent.com/assets/1683475/11798257/d2af222a-a28e-11e5-90dd-67e3dbbe3123.png)
        1. enter a _Product name_.  It can be the same project name that you used previously  
![gam-74](https://cloud.githubusercontent.com/assets/1683475/14229406/c501aa6a-f8f8-11e5-84ae-0f6aabfe056c.png)
        1. at the bottom of the screen, click `Save` 
        1. on the next screen, in the center of the screen, click on `Create credentials` and choose `OAuth client ID`<br />
![gam-75](https://cloud.githubusercontent.com/assets/1683475/14229405/c5013c2e-f8f8-11e5-84f5-3351968ec5e3.png)     
        1. on the next screen, change the `Application type` to `Other`, enter a name, and click `Create`.  
![gam-36](https://cloud.githubusercontent.com/assets/1683475/11098096/5134ff2a-8868-11e5-9f20-1c36b8720bf1.png) 
        1. click the `Save` button.
        1. in the pop-up confirmation window, click `OK`.  You do not need to record the client ID or client secret
        1. on the next screen, you will see a section labeled `OAuth 2.0 client IDs`.  The client you just created will be listed. The `Type` column will say `Other`.
![gam-52](https://cloud.githubusercontent.com/assets/1683475/11798262/d2bd882e-a28e-11e5-9c4d-6e258263c2c9.png)
        1. at the far right of the line, click the download button. 
        1. save the file to the same folder as GAM.exe or GAM.py and rename the file to *`client_secrets.json`*.  
![gam15](https://cloud.githubusercontent.com/assets/1683475/11096317/07b2dac4-885f-11e5-9283-bd7cc7141aff.png)
    1. create oauth2service.json
        1. near the top left of the screen, click on the `Create credentials` button and select `Service account key`<br />
![gam-78](https://cloud.githubusercontent.com/assets/1683475/14229302/1c89eb56-f8f6-11e5-82ba-fae6633212cd.png)
        1. under the label `Service account`, click the menu and select `New service account`.
![gam-81](https://cloud.githubusercontent.com/assets/1683475/14229303/1c9bef68-f8f6-11e5-8c58-9ec5f40aed00.png)
        1. enter a name for the service account.  It can be the same name as the project.
        1. select the `JSON` key type 
        1. click the `Create` button<br />
![gam-82a](https://cloud.githubusercontent.com/assets/1683475/14229633/ad94f22e-f8fd-11e5-9e9e-2c2724baa41a.png)
        1. a file download will start automatically.  Save the file to the same folder as GAM.exe or GAM.py and rename the file to *`oauth2service.json`*<br />
![gam19](https://cloud.githubusercontent.com/assets/1683475/11096321/07bd277c-885f-11e5-9aeb-07df368265e2.png)
        1. in the pop-up dialog, click `Close`
    1. There are now two sections in the screen - `OAuth 2.0 client IDs` and `Service account keys`.  At the far right of the `Service account keys` section, click on `Manage service accounts`.
![gam-83](https://cloud.githubusercontent.com/assets/1683475/14229293/1c131454-f8f6-11e5-917f-2fa47ad47ffd.png)
        1. on the next screen, find the line with the name of the service account you just created.  At the far right of that line, click on the 3-dots button and select `Edit`.
![gam-84](https://cloud.githubusercontent.com/assets/1683475/14229294/1c1ebc3c-f8f6-11e5-9aab-8d9e6a9095c2.png)
        1. in the pop-up dialog, check the box to `Enable Google Apps Domain-wide Delegation` and then click `Save`.<br />
![gam-85](https://cloud.githubusercontent.com/assets/1683475/14229295/1c2b2396-f8f6-11e5-83d1-bd66b5ef703c.png)
        1. in the top left corner of the screen, click on the card-stack menu button, then click on `API Manager`, then click on `Credentials`.<br />
![gam-89](https://cloud.githubusercontent.com/assets/1683475/14229296/1c36a98c-f8f6-11e5-8380-7db03a84c370.png)<br />
![gam-90](https://cloud.githubusercontent.com/assets/1683475/14229297/1c4364ba-f8f6-11e5-82c5-dc9f84855b65.png)<br />
![gam-91](https://cloud.githubusercontent.com/assets/1683475/14229298/1c4faf9a-f8f6-11e5-8340-79159289bce2.png)<br />
            1.  in the main part of the screen, the section labeled `OAuth 2.0 client IDs` now has two lines: one for the OAuth2 client (`Other`) and one for the `Service account client`.  The column to the far right lsts the Client ID for each client.  These Client IDs will be used in the next step. 
![gam-92](https://cloud.githubusercontent.com/assets/1683475/14229299/1c5cbdde-f8f6-11e5-862d-afbd2f3f132f.png)
1. Authorize the API scopes for use with GAM in the Admin Console
    1. In this step, you will switch between the Developer's console and the domain's Admin console.  To access the Admin console, you must use an account with domain super-admin account or an account with delegated Security rights.  The Developer's console window must be logged in to the account in which the project was created.  These can be the same account or different accounts.
    1. Authorize scopes for OAuth2
        1. select the `Client ID` for the OAuth client (type `Other`) and copy it (Control/Command-C).<br />
![gam-60](https://cloud.githubusercontent.com/assets/1683475/11798259/d2b077ce-a28e-11e5-992c-4d3e044ac610.png)
        1. in another browser window or tab, login to Google Apps using a domain super-admin account
        1. go to the [Google Apps Admin Console](http://admin.google.com)
        1. click the `Security` icon  
![gam23](https://cloud.githubusercontent.com/assets/1683475/11096322/07bd8492-885f-11e5-9365-55a2dead8455.png)
        1. in the Admin Console, go to the Security section, click on `Show more`, then `Advanced settings`, then `Manage API client access`
        1. near the top of the screen, paste the Client ID into the field labeled `Client Name`
        1. select the entire list of _API scopes - OAuth2_ below, copy it (Control/Command-C) and paste it into the field labeled `One or More API Scopes` on the Admin Console screen
        1. click the `Authorize` button 
![gam26](https://cloud.githubusercontent.com/assets/1683475/11096329/07c82474-885f-11e5-9741-90121987b508.png)
        1. in the list of projects and scopes, the OAuth2 Client ID will appear in the left column and the list of API scopes will appear in the right column<br />
![gam-61](https://cloud.githubusercontent.com/assets/1683475/11919919/2953b4de-a725-11e5-9c00-dd8cc49d2d4c.png)
    1. Authorize scopes for the service account
        1. in the Developer's Console, return to the screen with the project's credentials listed
        1. in the `OAuth 2.0 Client IDs` section, click and drag to select the Service Account's client ID and copy it (Control/Command-C).  The client ID is a long string of numbers and/or letters (but is not the same client ID as the OAuth client ID)
        1. switch to the Admin Console and paste the client ID into the field labeled `Client Name`
        1. select the entire list of _API scopes - Service Account_ below, copy it (Control/Command-C) and paste it into the field labeled `One or More API Scopes` on the Admin Console screen
        1. click the `Authorize` button
        1. in the list of projects and scopes, the Service Account ID will appear in the left column and the list of API scopes will appear in the right column<br />
![gam-62](https://cloud.githubusercontent.com/assets/1683475/12075487/fda9ef9c-b147-11e5-8d7c-a2a417078f64.png)
1. Run GAM to authorize the configuration
    1. open a command line window and navigate to the file gam.exe or gam.py
    1. run the command `gam oauth create`
    1. the configuration options will be displayed.  Most API scopes will be selected by default. 
        1. There is a limit to the number of API scopes that a project can have active.  If you need the services provided by one of the unselected APIs you must disable one of the other APIs (type its number and press `Enter`) and then selecting the required API (type its number and press `Enter`).
        1. Choose the last option in the list (`Continue`): type its option number and press `Enter`.<br />
![gam-95](https://cloud.githubusercontent.com/assets/1683475/14229585/7fd2e9e6-f8fc-11e5-80c1-c117b2f2eb15.png)
    1. a browser window will open to display the confirmation screen.  
        1. if the computer that you are running GAM on does not have a web browser, you can use a browser on another computer to complete this step.  On the other computer, enter the goo.gl short URL that is displayed in the command line window  
![gam22](https://cloud.githubusercontent.com/assets/1683475/11096324/07c046f0-885f-11e5-9ece-2cc76b4bb59d.png)
            * if you are replacing existing client_secrets.json and oauth2service.json files, it may be necessary to remove or rename your existing oauth2.txt file for the goo.gl short URL to be displayed
    1. scroll to the bottom of the list of permissions and click `Allow`<br />
![gam21](https://cloud.githubusercontent.com/assets/1683475/11096323/07be2bc2-885f-11e5-9822-35a6cd35b8e9.png)
    1. the web page will report that the authentication flow has completed.
    1. in the command line window, the GAM command will complete, and you will see information about the Google Apps domain

If you access the web via a Proxy is may be necessary to set a Proxy in GAM, to do so:

set http_proxy=http://1.2.3.4:8080
set https_proxy=http://1.2.3.4:8080

Obviously you need to set your proxy to the correct IP address that you use.  The above 1.2.3.4 and port 8080 is for example purposes.  Credit for this to Craig Box

gam oauth request


GAM is now ready for use.


API scopes - OAuth2:

````
https://mail.google.com/,
https://www.googleapis.com/auth/activity,
https://www.googleapis.com/auth/admin.datatransfer,
https://www.googleapis.com/auth/admin.directory.customer,
https://www.googleapis.com/auth/admin.directory.domain,
https://www.googleapis.com/auth/admin.directory.resource.calendar,
https://www.googleapis.com/auth/calendar,
https://www.googleapis.com/auth/classroom.courses,
https://www.googleapis.com/auth/classroom.profile.emails,
https://www.googleapis.com/auth/classroom.profile.photos,
https://www.googleapis.com/auth/classroom.rosters,
https://www.googleapis.com/auth/cloudprint,
https://www.googleapis.com/auth/drive,
https://www.googleapis.com/auth/plus.login,
https://www.googleapis.com/auth/plus.me,
https://www.googleapis.com/auth/siteverification
````

API scopes - Service Account:

````
https://mail.google.com/,
https://sites.google.com/feeds,
https://www.google.com/m8/feeds/contacts,
https://www.googleapis.com/auth/activity,
https://www.googleapis.com/auth/calendar,
https://www.googleapis.com/auth/drive,
https://www.googleapis.com/auth/gmail.settings.basic,
https://www.googleapis.com/auth/gmail.settings.sharing,
https://www.googleapis.com/auth/plus.login,
https://www.googleapis.com/auth/plus.me,
https://www.googleapis.com/auth/userinfo.email,
https://www.googleapis.com/auth/userinfo.profile
````


From time to time, Google changes one or more of the tools used in this process.  Some of the steps may change, or what you see on the screen may differ from what is shown here.  Please post a comment in the discussion forum if you find an outdated or incorrect instruction (or just fix it - anyone can edit the wiki).
