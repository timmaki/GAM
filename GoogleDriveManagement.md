- [Managing Google Drive Files and Folders for users](#managing-google-drive-files-and-folders-for-users)
  - [Printing User Drive Files to a CSV](#printing-user-drive-files-to-a-csv)
  - [Creating and Uploading Drive Files for Users](#creating-and-uploading-drive-files-for-users)
  - [Updating Drive Files for Users](#updating-drive-files-for-users)
  - [Downloading Drive Files For Users](#downloading-drive-files-for-users)
  - [Deleting Google Drive Files for Users](#deleting-google-drive-files-for-users)
- [Managing Google Drive Permissions for Users](#managing-google-drive-permissions-for-users)
  - [Showing the Permissions of a File/Folder for a user](#showing-the-permissions-of-a-filefolder-for-a-user)
  - [Adding permissions to a file/folder for a user](#adding-permissions-to-a-filefolder-for-a-user)
  - [Updating permissions to a file/folder for a user](#updating-permissions-to-a-filefolder-for-a-user)
  - [Removing permissions to a file/folder for a user](#removing-permissions-to-a-filefolder-for-a-user)

GAM now supports Google Drive Management with the ability to add, update, view and delete Drive files and folders for users as well as adding, updating, viewing and deleting file and folder permissions.

# Managing Google Drive Files and Folders for users
## Printing User Drive Files to a CSV
### Syntax
```
gam user <username>|group <groupname>|ou <ouname>|all users show filelist [todrive] [query <query>] [allfields]
  [createddate] [description] [fileextension] [filesize] [id] [restricted] [starred] [trashed] [viewed]
  [lastmodifyingusername] [lastviewedbymedate] [modifieddate] [originalfilename] [quotaused] [shared] [writerscanshare]
```
Outputs a CSV file listing the Google Drive files/folders that the given user(s) own. By default, the output is sent to the screen and only the file owner, title and URL columns are shown. The optional todrive argument will upload the CSV data to a Google Docs Spreadsheet file in the Administrator's Google Drive rather than displaying it locally. The optional query argument allows the results to be narrowed to files/folders matching the given query. The query format is described in [Google's documentation](https://developers.google.com/drive/web/search-parameters). The optional allfields arguments causes all possible columns to be included in the output. The optional createddate, description, fileextension, filesize, id, restricted, starred, trashed, viewed, lastmodifyingusername, lastviewedbymedate, modifieddate, originalfilename, quotaused, shared and writerscanshare arguments cause the given columns to be included in the output.

### Example
This example displays all of Joe Schmo's files
```
gam user jschmo@acme.com show filelist
```

This example displays all files for all users that contain the text "ProjectX". The results are uploaded to a Google spreadsheet for the admin user.
```
gam all users show filelist query "fullText contains 'ProjectX'" todrive
```

This example displays all PDF files that users under the Students OU own.

```
gam ou_and_children Students show filelist query "mimeType = 'application/pdf'"
```

---


## Creating and Uploading Drive Files for Users
### Syntax
```
gam user <username>|group <groupname>|ou <ouname>|all users add drivefile [localfile <filepath>]
  [drivefilename <filename>] [convert] [ocr] [ocrlanguage <language>] [restricted] [starred] [trashed] [viewed]
  [lastviewedbyme <date>] [modifieddate <date>] [description] [mimetype <type>] [parentid <folder id>]
  [parentname <folder name>] [writerscantshare]
```
Create or upload a new file to Google Drive for the given user(s). By default, the command will create a new, empty file/folder. If the optional argument localfile is specified along with the full path to a document on the local computer, GAM will upload that file's contents to Drive. The optional argument drivefilename sets the name of the file/folder in Drive. The optional argument convert causes files to be converted into native Google Docs format where possible. The optional argument ocr causes OCR analysis of images and PDF files when they are converted to native Google Docs format. The optional argument ocrlanguage determines what language is used for ocr analysis. The optional argument restricted prevents users who have reader/commenter access to a file from downloading the file content. The optional arguments starred, trashed and viewed cause the respective action to take place on the new file. The optional arguments lastviewedbyme and modifieddate set the respective timestamps for the new file, the date should follow the format YYYY-MM-DDTHH:MM:SS.000Z. For example, 2013-04-20T12:33:47.166Z. The optional argument description gives a description for the new file. The optional argument mimetype forces the given MIME file type to be used for the new file. The optional argument parentid sets a parent folder for the uploaded/created file to show underneath. The optional argument parentname searches for the given folder name to put the file under. The optional argument writerscantshare prevents users who have writer/editor access to the file from adding additional permissions to the file (only owner can add permissions).

### Examples
This example uploads the file sillycat.mp4 to Google Drive for a user
```
gam user jsmith@acme.com add drivefile localfile sillycat.mp4
```

This example creates a new folder called TPS Reports for all users and then creates a new, empty Google Doc, Spreadsheet, Presentation and Drawing under each user's folder.
```
gam all users add drivefile drivefilename "TPS Reports" mimetype gfolder
gam all users add drivefile drivefilename "TPS Doc" mimetype gdoc parentname 'TPS Reports'
gam all users add drivefile drivefilename "TPS Sheet" mimetype gsheet parentname 'TPS Reports'
gam all users add drivefile drivefilename "TPS Presentation" mimetype gpresentation parentname 'TPS Reports'
gam all users add drivefile drivefilename "TPS Drawing" mimetype gdrawing parentname 'TPS Reports'
```

This example uploads the MyRamblings.docx file to Google Drive and converts it to Google Doc native format. It also renames the file to a nicer looking "My Ramblings".
```
gam user jjones@acme.com add drivefile localfile MyRamblings.docx convert drivefilename "My Ramblings"
```

---


## Updating Drive Files for Users
### Syntax
```
gam user <username>|group <groupname>|ou <ouname>|all users update drivefile [id <drive file id> | drivefilename <filename>] [localfile <filename>] [newfilename <filename>] [convert] [ocr] [ocrlanguage <language>] [restricted true|false] [starred true|false] [trashed true|false] [viewed true|false] [lastviewedbyme <date>] [modifieddate <date>] [description <description>] [mimetype <MIME type>] [parentid <folder id>] [parentname <folder name>] [writerscantshare]
```
Update a Drive file's metadata and/or content. In order to determine which file(s) are updated, either the id or drivefilename arguments must be specified. id specifies the exact unique id of the file to be updated. drivefilename performs a search for files matching the given name. The optional argument localfile specifies a local file whose content will completely replace the content of the given drive file (file id, name, etc will remain unchanged). The optional arguments convert, ocr, ocrlanguage, restricted, starred, trashed, description, mimetype and viewed specify updates that should occur to a file's metadata. The optional lastviewedbyme and modifieddate arguments specify new timestamps that should be placed on the Drive file. The date should follow the format YYYY-MM-DDTHH:MM:SS.000Z. For example, 2013-04-20T12:33:47.166Z. The optional parentid and parentname arguments specify folders under which the drive file should be placed. The optional writerscantshare argument prevents file writers/editors from sharing the file with additional users.

### Examples
This example updates the "My Ramblings" file to be starred and placed under a folder called "Brilliant things I've said" (assumes a folder by that name already exists for the user)
```
gam user bsmith@acme.com update drivefile drivefilename "My Ramblings" starred true parentname 'Brilliant things I've said'
```

This example updates the Drive file DailyReport.pdf with the contents of the local file Report-3-28-2014.pdf.
```
gam user hgregg@acme.com update drivefile drivefilename DailyReport.pdf localfile Report-3-28-2014.pdf
```

---


## Downloading Drive Files For Users
### Syntax
```
gam user <username>|group <groupname>|ou <ouname>|all users get drivefile [id <file id> | query <query>] [format <openoffice|microsoft|pdf>] [targetfolder <local path>]
```
Download the given Drive files to the local computer. Either the id or query parameters must be specified to determine which files should be downloaded. By default, Google Docs native format files are downloaded in openoffice format. The optional argument format allows you to download the files in Microsoft format (docx, xlsx, pptx, etc) or PDF format. The optional argument targetfolder allows you to specify where on the local computer the downloaded files should be placed.

Note that drive folder hierarchy is NOT maintained when downloading files with this command.

### Examples
This example downloads the file with Drive ID adifd08 to the current path
```
gam user asmith@acme.com get drivefile id adifd08
```

This example downloads all of a user's files to c:\jsmith-files using Microsoft Office format for downloading native Google Docs.
```
gam user jsmith@acme.com get drivefile query "'me' in owners" format microsoft
```

---


## Deleting Google Drive Files for Users
### Syntax
```
gam user <username>|group <groupname>|ou <ouname>|all users delete drivefile <file id> [purge]
```
Delete the given Drive files for user(s). The "file id" argument is the exact ID of a Google Drive file or a query to search the user's Drive for files in the format ` "query:<query>" `. By default, deleted folders are simply moved to the user's Trash folder which is purged after 30 days. The optional parameter purge causes the files to be immediately purged from the user's Google Drive so that they are no longer recoverable from Trash.

### Examples
This example moves the given Drive file to the user's Trash in Drive.
```
gam user jsmith@acme.com delete drivefile 8sidfddosa
```

This example completely purges all files from a user's Drive that are PDFs (danger Will Robinson!!!)
```
gam user jsmith@acme.com delete drivefile "query:mimeType = 'application/pdf'" purge
```

---


# Managing Google Drive Permissions for Users
## Showing the Permissions of a File/Folder for a user
### Syntax
```
gam user <email> show drivefileacl <file id>
```
shows the current permissions of a file or folder owned or shared with a given user.

### Example
This example shows the permissions of one of jsmith's files
```
gam user jsmith@acme.org show drivefileacl 0B8aCWH-xLi2NckxXOEp5REUtNEE

John Smith
 domain: acme.org
 emailAddress: jsmith@acme.org
 photoLink: https://lh5.googleusercontent.com/-AzWvbYordY/AAAAAAAAAAE/AAAAAAAAERg/nzagv0IV4yQ/s64/photo.jpg
 role: owner
 type: user
 id: 17297927562723854745

George Wilson
 domain: gmail.com
 emailAddress: gwilson@gmail.com
 photoLink: https://lh5.googleusercontent.com/-woxYfVbgI4w/AAAAAAAAAaI/AAAAAAAAb
SI/Y0RRW2LWX5U/s64/photo.jpg
 role: writer
 type: user
 id: 00772439636938147216
```

---


## Adding permissions to a file/folder for a user
### Syntax
```
gam user <user email> add drivefileacl <file id> [user|group|domain|anyone <value>] [withlink] [role <reader|commenter|writer|owner>] [sendemail] [emailmessage <message text>]
```
Grants a user, group, domain or anyone permission to the given Drive file/folder. The role parameter determines the level of access the given user(s) have to the file and can be one of reader, commenter, writer or owner. Specifying owner will change ownership of the file/folder and only works when the source and target accounts are in the same Google Apps instance. The optional withlink parameter specifies that the file is not "discoverable" or indexed. It is only available if the accessing user knows the exact URL. The optional sendemail parameter will send an email to the user(s) who have been granted access to the file (no email sent by default). The optional emailmessage parameter allows you to specify a portion of the email message body sent to the user.

### Examples
This example silently gives Sally access to Tim's file
```
gam user tim@acme.org add drivefileacl 0B8aCWH-xLi2NckxXOEp5REUtNEE user sally@acme.org role writer withlink
```

This example gives the IT Google Group access to Tim's file and sends an email notification
```
gam user tim@acme.org add drivefileacl 0B8aCWH-xLi2NckxXOEp5REUtNEE group it@acme.org role reader sendemail
```

This example gives anyone in the Acme organization access to Tim's file if they know the URL
```
gam user tim@acme.org add drivefileacl 0B8aCWH-xLi2NckxXOEp5REUtNEE domain acme.org role commenter withlink
```

This example gives anyone on the Internet (logged in to Google or not) access to Tim's file and makes it searchable/discoverable via Google.com search and other search engines
```
gam user tim@acme.org add drivefileacl 0B8aCWH-xLi2NckxXOEp5REUtNEE anyone role reader
```

---


## Updating permissions to a file/folder for a user
### Syntax
```
gam user <user email> update drivefileacl <file id> <permission id> [withlink] [role <reader|commenter|writer|owner>] [transferownership <true|false>]
```
Changes a user or groups permissions to the given Drive file/folder. The permisson id parameter can be an email address or a numeric id as shown when listing a file's permissions. If an email address is used, GAM must first look up the permission id of that email address before updating (2 API calls instead of 1). If using numeric id, you must prefix it with "id:". The role parameter determines the level of access the given user(s) have to the file and can be one of reader, commenter, writer or owner. Specifying owner will change ownership of the file/folder and only works when the source and target accounts are in the same Google Apps instance. The optional withlink parameter specifies that the file is not "discoverable" or indexed. It is only available if the accessing user knows the exact URL. The optional transferownership parameter indicates whether changing a role to 'owner' downgrades the current owners to writers. 

### Example
This example changes Sally from a reader to a writer for the file.
```
gam user tim@acme.org update drivefileacl 0B8aCWH-xLi2NckxXOEp5REUtNEE sally@acme.org role writer withlink
```

### Example
This example changes Sally from a reader to a writer for the file using her numeric permission ID.
```
gam user tim@acme.org update drivefileacl 0B8aCWH-xLi2NckxXOEp5REUtNEE id:65337053707119961365 role writer withlink
```
### Example
This example makes Sally the owner for the file and changes Tim from owner to writer for the file.
```
gam user tim@acme.org update drivefileacl 0B8aCWH-xLi2NckxXOEp5REUtNEE sally@acme.org role owner transferownership true
```

---


## Removing permissions to a file/folder for a user
### Syntax
```
gam user <user email> delete drivefileacl <file id> <permission id>
```
Removes the give permission from the file. The permisson id parameter can be an email address or a numeric id as shown when listing a file's permissions. If an email address is used, GAM must first look up the permission id of that email address before updating (2 API calls instead of 1).

### Example
This example removes Sally's access to Tim's file
```
gam user tim@acme.org delete drivefileacl 0B8aCWH-xLi2NckxXOEp5REUtNEE sally@acme.org
```