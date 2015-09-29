- [Printing All Users](#printing-all-users)
- [Printing All Groups](#printing-all-groups)
- [Print All Aliases](#print-all-aliases)
- [Print All Organizational Units](#print-all-organizational-units)
- [Print All Resource Calendars](#print-all-resource-calendars)
- [Print All Domains and Domain Aliases](#print-all-domains-and-domain-aliases)
- [Print Mobile Devices](#print-mobile-devices)
- [Print Chrome OS Devices](#print-chrome-os-devices)
- [Print Licenses](#print-licenses)
- [Reports](#reports)
  - [User Report](#users-report)
  - [Domain Report](#domain-report)
  - [Drive Report](#drive-report)
  - [Admin Actions Report](#admin-actions-report)
  - [Login Audit Report](#login-audit-report)

# Printing All Users

### Syntax
```
gam print users [allfields] [custom all|list,of,schemas] [userview] [ims] [emails] [externalids] [relations] [addresses] [organizations] [phones] [licenses] [firstname] [lastname] [emailparts] [deleted_only] [orderby email|firstname|lastname] [ascending|descending] [domain] [query <query>] [fullname] [ou] [suspended] [changepassword] [agreed2terms] [admin] [gal] [id] [creationtime] [lastlogintime] [aliases] [groups] [todrive]
```
prints a CSV file of all users in the Google Apps Organization. The CSV output can be redirected to a file using the operating system's pipe command (such as "> users.csv") see examples below. By default, the only column printed is the user's full email address. The optional argument allfields adds all fields (except groups which requires per-user API calls) to the CSV. The optional argument deleted\_only prints only users deleted within the past 5 days. The optional custom argument adds custom schemas. If all is specified, all custom schemas will be included. Otherwise only those listed in a comma separated list will be included. The optional userview parameter returns only fields that are viewable by regular users and can be run even if GAM is authenticated against a regular user account. The optional licenses parameter includes a column for all SKUs assigned to each user. The optional query parameter should match the [API search for users](https://developers.google.com/admin-sdk/directory/v1/guides/search-users) format. All other arguments add the respective additional column to the CSV output. Note that adding groups will require 1 additional call to Google's servers <b>per user</b> which will significantly increase the length of time for the command to complete. The optional todrive argument will upload the CSV data to a Google Docs Spreadsheet file in the Administrators Google Drive rather than displaying it locally.

### Example
This example will generate the csv file users.csv showing with columns many fields
```
gam print users allfields > users.csv
Getting all users in the organization (may take some time on a large Google Apps account)...

users.csv contains:
--
Email,Firstname,Lastname,Fullname,Username,OU,Suspended,SuspensionReason,ChangePassword,AgreedToTerms,DelegatedAdmin,Admin,CreationTime,LastLoginTime,Aliases,NonEditableAliases,ID,PhotoURL,IncludeInGlobalAddressList
jsmith@acme.com,Jon,Smith,Jon Smith,jsmith,/Sales,False,,False,True,False,False,2012-03-23T15:04:19.000Z,2013-05-06T16:02:36.000Z,,jsmith@acme-alias.gov,106100537778424449519,,True
--
```

---


# Printing All Groups
### Syntax
```
gam print groups [name] [description] [admincreated] [id] [aliases] [members] [owners] [managers] [settings] [todrive]
```
prints a CSV file of all groups in the Google Apps domain. The CSV output can be redirected to a file using the operating system's pipe command (such as "> groups.csv") see examples below. By default, the only column printed is the Group email address. The optional arguments name, description, id and admincreated add the respective additional column to the CSV output. The optional arguments members, owners, managers and settings each perform 1 additional API call per group which may greatly increase the time it takes the command to complete. settings will add multiple columns for the groups advanced settings. The optional todrive argument will upload the CSV data to a Google Docs Spreadsheet file in the Administrators Google Drive rather than displaying it locally.

### Examples
this example will output all details for all groups to the file groups.csv
```
gam print groups name description admincreated id aliases members owners managers settings > groups.csv
```

---


# Print All Aliases
### Syntax
```
gam print aliases [todrive]
```
prints a CSV file of all email aliases in the Google Apps domain for both users and groups. The CSV output can be redirected to a file using the operating system's pipe command (such as "> nicknames.csv") see examples below. The optional todrive argument will upload the CSV data to a Google Docs Spreadsheet file in the Administrators Google Drive rather than displaying it locally.

### Example
this example will output all nicknames to the file aliases.csv
```
gam print aliases > aliases.csv
```

---


# Print All Organizational Units
### Syntax
```
gam print orgs [name] [description] [parent] [inherit] [allfields] [todrive]
```
prints a CSV file of all organizational units in the Google Apps account. The CSV output can be redirected to a file using the operating system's pipe command (such as "> orgs.csv") see examples below. By default, the only column output is "Path" (OUs full path). The optional argument allfields will include all possible fields in the CSV. The optional arguments name, description, parent and inherit add the respective additonal column to the CSV output. Only 1 call to Google's servers is done no matter which arguments are specified so the optional arguments should not significantly increase the time it takes for the command to complete. The optional todrive argument will upload the CSV data to a Google Docs Spreadsheet file in the Administrators Google Drive rather than displaying it locally.

### Example
this example will output all organizations to the file orgs.csv including all optional columns
```
gam print orgs name description parent inherit > orgs.csv
```

---


# Print All Resource Calendars
### Syntax
```
gam print resources [id] [description] [email] [todrive]
```
prints a CSV file of all resource calendars in the Google Apps account. The CSV output can be redirected to a file using the operating system's pipe command (such as "> resources.csv") see examples below. By default, the only column output is "Name"The optional arguments id, description and email add the respective additonal column to the CSV output. Only 1 call to Google's servers is done no matter which arguments are specified so the optional arguments should not significantly increase the time it takes for the command to complete. The optional todrive argument will upload the CSV data to a Google Docs Spreadsheet file in the Administrators Google Drive rather than displaying it locally.

### Example
this example will output all resource calendars to the file resources.csv including all optional columns
```
gam print resources id description email > resources.csv
```
---

# Print All Domains and Domain Aliases
### Syntax
```
gam print domains [todrive]
```

Outputs CSV of all domains. The todrive parameter causes GAM to create a Google Spreadsheet of results rather than outputting a CSV.
---

# Print Mobile Devices
### Syntax
```
gam print mobile [query <query>] [orderby deviceid|email|lastsync|model|name|os|status|type] [ascending|descending] [todrive]
```

Prints all mobile devices connected to the Google Apps instance. All fields are included in the CSV. Optional argument query specifies an optional query to limit output results. The format of the query parameter should match the [Search format of the Control Panel](http://support.google.com/a/bin/answer.py?hl=en&answer=1408863#search). orderby and ascending/descending parameters determine how the CSV output is sorted. The optional todrive argument will upload the CSV data to a Google Docs Spreadsheet file in the Administrators Google Drive rather than displaying it locally.

### Example
This example prints details on all mobile devices in the domain
```
gam print mobile
```

This example prints all of jsmith@acme.org's mobile devices
```
gam print mobile query "email:jsmith@acme.org"
```

---


# Print Chrome OS Devices
### Syntax
```
gam print cros [query <query>] [orderby location|user|lastsync|serialnumber|supportenddate] [ascending|descending] [todrive]
```
Print all Chrome OS devices enrolled in the Google Apps instance. All fields are included in CSV output. Optional parameter query specifies a query to perform, limiting the results to matching devices. The query format is described in Google's [help article](http://support.google.com/chrome/a/bin/answer.py?hl=en&answer=1698333). orderby and ascending/descending parameters determine sorting of CSV output. The optional todrive argument will upload the CSV data to a Google Docs Spreadsheet file in the Administrators Google Drive rather than displaying it locally.

### Example
This example prints all Chrome OS Devices enrolled in the domain.

```
gam print cros
```

This example prints all Chrome OS devices annotated as belonging to jsmith@acme.org

```
gam print cros query "user:jsmith@acme.org"
```

---


# Print Licenses
### Syntax
```
gam print licenses [todrive]
```
Print Google Apps, Google Drive storage and Google Coordinate license assignments for the domain. The optional todrive argument will upload the CSV data to a Google Docs Spreadsheet file in the Administrators Google Drive rather than displaying it locally.

### Example
This example gets all license assignments for the Google Apps instance and uploads the spreadsheet to Google Docs.
```
gam print licenses todrive
```

---


# Reports
## Users Report
### Syntax
```
gam report users [todrive] [date <yyyy-mm-dd>] [user <email>] [filter <filter terms>] [fields <included fields>]
```

Display or upload to Google Drive a CSV report of current users. The optional todrive parameter specifies that the results should be uploaded to Google Drive rather than being displayed on screen or piped to a CSV text file. The optional date parameter specifies when the report should be pulled for, when not specified, GAM pulls the most recently available report from Google. The optional user parameter specifies the email address of a single user whose data should be returned, by default all users in the Google Apps instance are pulled. The optional filter parameter specifies search terms as described in [Google's API documentation](https://developers.google.com/admin-sdk/reports/v1/reference/userUsageReport/get). The optional fields parameter specifies a comma-separated list of fields (columns) to be included in the output, if not specified all columns are returned.

### Example
This command will pull the most recently available users report and upload to drive.
```
gam report users todrive
```

This command will pull a list of users who have not logged in since the begging of the year.
```
gam report users filter 'accounts:last_login_time<2013-01-01T00:00:00.000Z'
```

---


## Domain Report
### Syntax
```
gam report domain [todrive] [date <yyyy-mm-dd>]
```
Display or upload to Google Drive a CSV report of aggregate user data across the Google Apps instance (all users). The optional todrive parameter specifies that the results should be uploaded to Google Drive rather than being displayed on screen or piped to a CSV text file. The optional date parameter specifies when the report should be pulled for, when not specified, GAM pulls the most recently available report from Google.

### Example
This example uploads to Google Drive the most recent domain report
```
gam report domain todrive
```

## Drive Report
### Syntax
```
gam report drive [todrive] [user <user email> [ip <ip address>] [start <start time>] [end <end time>] [event view|edit]
```
Display or upload to Google Drive a CSV report of Google Drive activities by users. The optional todrive parameter specifies that the results should be uploaded to Google Drive rather than being displayed on screen or piped to a CSV text file. The optional user parameter narrows the results down to documents viewed or edited by the given user. The optional ip address parameter narrows results down to activities performed from the given IPv4 or IPv6 address. The optional start and end parameters narrow the results down to actions performed during the given period. The optional event parameter narrows the results down to just views or just edits.

### Example
This example uploads to Drive a CSV of all doc actions.
```
gam report drive todrive
```

This example narrows the results down to actions performed by john@acme.com on Christmas Day (GMT).

```
gam report drive user john@acme.com start 12-25-2013T00:00:00.000Z end 12-25-2013T23:59:59.999Z
```

## Admin Actions Report
### Syntax
```
gam report admin [todrive] [user <user email>] [ip <ip address>] [start <start time>] [end <end time>] [event <event name>]
```
Display or upload to Google Drive a CSV report of administrator activities for the Google Apps domain. The optional todrive parameter specifies that the results should be uploaded to Google Drive rather than being displayed on screen or piped to a CSV text file. The optional user parameter narrows the results down to admin activities performed by the given user. The optional ip address parameter narrows results down to activities performed from the given IPv4 or IPv6 address. The optional start and end parameters narrow the results down to actions performed during the given period. The optional event parameter narrows the results down to the given admin event type.

### Example
This example uploads all recent admin changes to Google Drive.
```
gam report admin todrive
```

This example shows the admin activities of joe@schmo.com for 6/9/13 through 6/12/13 (GMT).
```
gam report admin todrive user joe@schmo.com start 06-09-2013T00:00:00.000Z end 06-12-2013T11:59:59.999Z
```

## Login Audit Report
### Syntax
```
gam report logins [todrive] [user <user email>] [ip <ip address>] [start YYYY-MM-DDThh:mm:ss.000Z] [end YYYY-MM-DDThh:mm:ss.000Z] [event <event name>]
```
Display or upload to Google Drive a CSV report of user login activities for the Google Apps domain. The optional todrive parameter specifies that the results should be uploaded to Google Drive rather than being displayed on screen or piped to a CSV text file. The optional user parameter narrows the results down to login activities performed by the given user. The optional ip address parameter narrows results down to activities performed from the given IPv4 or IPv6 address. The optional start and end parameters narrow the results down to actions performed during the given period. The optional event parameter narrows the results down to the given admin event type.

### Example
This example uploads all recent admin changes to Google Drive.
```
gam report admin todrive
```

This example shows the login activities of joe@schmo.com.
```
gam report logins todrive user joe@schmo.com
```