(TODO: Add table of contents.)

_**Comments have been turned off for these help pages, please post your questions and comments to the [Mailing List](http://groups.google.com/group/google-apps-manager)**_

# Users
## Creating a User
### Syntax
```
gam create user <email address> firstname <First Name> lastname <Last Name> password <Password> [suspended on|off] [changepassword on|off] [admin on|off] [sha] [md5] [nohash] [ipwhitelisted on|off] [quota #] [agreedtoterms on|off] [org <Org Name>] [customerid <Customer ID>]
```
Create an user account. First Name, Last Name and Password arguments are required and should be single quoted if they contain spaces or special characters like ! or $ that the shell might try to interpret itself. Optional parameter suspended on creates the account but marks it as suspended (suspended off, otherwise known as active is the default).  The optional parameter changepassword on will force the user to change their password after their first successful login (changepassword off is the default). The optional parameter admin on makes the user a Google Apps Super Admin (admin off is the default). The optional parameters sha and md5 indicate that the password is a hash of the given type. By default, if neither sha1 or md5 are specified, GAM will do a sha1 hash of the provided password and send the hash instead of the plain text password for an additional layer of security. However, when hashes are sent, Google is unable to ensure password length and strength so it's possible to set passwords that do not conform to Google's length requirement this way. The optional parameter nohash disable's GAM's automatic hashing of the password (password is still sent over encrypted HTTPS) so that Google can evaluate the length and strength of the password. Optional parameter ipwhitelisted on turns IP Whitelisting on for the user (ipwhitelisted off is default). Optional parameter quota # (where # is the user's quota in gigabytes) allows you to set the user's email quota (Note: Unless You have specifically requested this ability from Google, setting quotas will not work, don't use this). Optional parameter agreedtoterms on flags the user as having agreed to Google's Terms of Service (ToS). For most domains, agreedtoterms is read-only by the admin in which case Google will ignore this setting for the user. Optional parameter org allows the user to be moved into the desired Organization after being created. Note that this requires one or two separate API calls (depending on whether or not customerid is also specified) which will cause GAM to take longer. Optional parameter customerid specifies the customer ID which is used only when setting the user's org. If not specified, GAM will lookup the customerid itself causing an additional API call. For best performance when bulk provisioning, use the "gam info domain" command to lookup the customer ID and specify it.

### Example
This example creates a user account. Note that the password is in single quotes to prevent the shell from acting on the special characters.

```
gam create user droth firstname "David Lee" lastname Roth password 'MightAsWellJump!'
```

---


## Update (and Rename) a User
### Syntax
```
gam update user <email address> [firstname <First Name>] [lastname <Last Name>] [password <Password>] [username <New Email>] [admin on|off] [suspended on|off] [ipwhitelisted on|off] [sha] [md5] [nohash] [changepassword on|off] [agreedtoterms on|off] [org <Org Name>] [customerid <Customer ID>]
```
Update a user account. firstname, lastname and password arguments are optional and should be single quoted if they contain spaces or special characters like $ or ! that may be interpreted by the shell. Username is optional and will rename the user's account name (and thus their email address). admin, suspended and ipwhitelisted arguments are optional and can be turned on or off. sha and md5 arguments are optional and indicate that the password specified is a hash of the given type. By default, if neither sha1 or md5 are specified, GAM will do a sha1 hash of the provided password and send the hash instead of the plain text password for an additional layer of security. However, when hashes are sent, Google is unable to ensure password length and strength so it's possible to set passwords that do not conform to Google's length requirement this way. The optional parameter nohash disable's GAM's automatic hashing of the password (password is still sent over encrypted HTTPS) so that Google can evaluate the length and strength of the password. changepassword is optional and indicates whether the user should be forced to change their password on next login. Optional parameter agreedtoterms on flags the user as having agreed to Google's Terms of Service (ToS). For most domains, agreedtoterms is read-only by the admin in which case Google will ignore this setting for the user. Optional parameter org allows the user to be moved into the desired Organization. Note that this requires one or two separate API calls (depending on whether or not customerid is also specified) which will cause GAM to take longer. Optional parameter customerid specifies the customer ID which is used only when setting the user's org. If not specified, GAM will lookup the customerid itself causing an additional API call. For best performance when bulk updating users, use the "gam info domain" command to lookup the customer ID and specify it.

Google makes the following recommendations when renaming a user account:
  * Before renaming a user, it is recommended that you logout the user from all browser sessions and services. For instance, you can get the user on your support desk telephone line during the rename process to ensure they have logged out. The process of renaming can take up to 10 minutes to propagate across all services.
  * Google Talk will lose all remembered chat invitations after renaming. The user must request permission to chat with friends again.
  * When a user is renamed, the old username is retained as a alias to ensure continuous mail delivery in the case of email forwarding settings and will not be available as a new username. If you prefer not to have the alias in place after the rename, you'll need to [Delete the Alias](ExamplesProvisioning#Deleting_an_Alias)

### Example
This example updates a user account, setting the firstname, lastname and password and giving them admin access to the domain. Notice that the password is in single quotes to prevent the shell from acting on the !.
```
gam update user pmcartney firstname Paul lastname McCartney password 'LetItBe!' admin on suspended off
```

This example renames ljones to lsmith, also setting her last name to Smith (in the case of marriage)
```
gam update user ljones username lsmith lastname Smith
```

In this example, George Otfired is no longer at the company and Nate Ewguy has taken his position, we'll change the username, first and last name and password all in one stroke thus retaining George's old Google Apps mail, documents, etc
```
gam update user gotfired username newguy firstname Nate lastname Ewguy password HopeILastHere
```

---


## Get User Info
### Syntax
```
gam info user <email address> [noaliases] [nogroups] [noorg]
```
retrieve details about the given user. GAM will print out a summary of the user. By default, GAM will retrieve the user's aliases, group memberships and Organization which results an API call each. If you do not require this information you can disable these API calls by specifying noaliases, nogroups and/or noorg.

### Example
This example will show information on the user
```
gam info user rstarr

User: rstarr
First Name: Ringo
Last Name: Star
Is an admin: false
Has agreed to terms: true
IP Whitelisted: false
Account Suspended: false
Must Change Password: false
Quota: 25600
Organization: Drummers
Email Aliases:
  drummer
  havingthemostfun
Groups:
  The Beatles <beatles@beatles.com> (direct member)
```

---


## Delete a User
### Syntax
```
gam delete user <email address> [dorename]
```
delete the given user's account. The optional parameter dorename invokes GAM's old behavior of renaming an account before deleting it which should no longer be necessary.

### Example
This example deletes Pete Best's account
```
gam delete user pbest
```

---


# Groups
## Create a Group
### Syntax
```
gam create group <group> [name <Group Name>] [description <Group Description>] [permission owner|member|domain|anyone]
```
create a group. Group Name and Description are optional and set the groups full name and description. Use quotes around them if they contain spaces. permission is optional and can be set to owner, member, domain or anyone which determines who has rights to post to the group. If the Google Groups for Business (user-managed groups) service is enabled for the Google Apps domain, additional groups security settings are available but cannot be set by GAM, this is a Google limitation. For details on User Groups and how rights translate, see [here](http://www.google.com/support/a/bin/answer.py?hl=en&answer=166148).

### Example
This example creates a group:
```
gam create group mygroup@example.com
```

This example creates a group that all group members can send to
```
gam create group beatles name "The Beatles" description "Members of the Fab Four" permission member
```

---


## Update Group Settings
### Syntax
```
gam update group <group> [name <Group Name>] [description <Group Description>] [permission owner|member|domain|anyone]
```
update a group's settings, modifying it's full name, description and/or permissions. Many more group settings can be modified using the [GAM Group Settings commands](GroupSettingsExamples).

### Example
This example modifies the group, changing it's full name, description and permissions
```
gam update group beatles name "The Beatles Rock Band" description "British Invasion Band" permission owner
```

---


## Add Members/Owners to a Group
### Syntax
```
gam update group <group> add owner|member <email address>
```
add a member or owner to a group. It's important to understand that membership and ownership are entirely separate. A user can be a owner of a group without being a member, a member of a group without being a owner, a member and owner of a group or neither.

**Note:** instead of an email address, the special user ` * ` can be specified to add all Google Apps users to the group. You may want to put quotes around the ` * ` to prevent the OS shell from interpreting it incorrectly.

### Example
This example adds a member to the group
```
gam update group beatles add member rstarr@beatles.com
```

---


## Remove owners/members from a Group
### Syntax
```
gam update group <group> remove owner|member <email address>
```
Remove a member or owner from the given group. Removing the user as a member does not revoke their owner status.

**Note:** instead of an email address, the special user ` * ` can be specified to delete the "all Google Apps users" special entity from the group (assuming it was already added). This doesn't actually empty the group, only remove the special "all users" user from the group. You may want to put quotes around the ` * ` to prevent the OS shell from interpreting it incorrectly.

### Example
This 2-command example removes the user from the group. First his ownership is revoked then his membership. Both are necessary to remove all his rights to the group.
```
gam update group students remove owner grad@school.edu
gam update group students remove member grad@school.edu
```

---


## Get Group Info
### Syntax
```
gam info group <group name>
```
retrieve information about a given group.

### Example
This example will provide information about the group
```
gam info group beatles

Group Name:  The Beatles
Email Permission:  Member
Group ID:  beatles@beatles.com
Description:  The Fab Four
Owner: jlennon@beatles.com
Owner: pmccartney@beatles.com
Member: gharrison@beatles.com
Member: rstarr@beatles.com
```

---


## Delete a Group
### Syntax
```
gam delete group <group name>
```
Delete a given group.

### Example
This example will delete the group
```
gam delete group beatles
```

---


# Email Aliases
## Creating an Alias
### Syntax
```
gam create alias <alias> user <user name>
```
create a alias for the given user.

### Example
This example will create a alias for the user
```
gam create alias theking user epresley
```

---


## Updating an Alias
### Syntax
```
gam update alias <alias> user <user name>
```
update an existing alias, changing the user it points to.

### Example
This example will update an existing alias, pointing it at another user
```
gam update alias ceo user sbalmer
```

---


## Retrieving alias Information
### Syntax
```
gam info alias <alias>
```
retrieve information about the given alias

### Example
This example will retrieve information about the alias
```
gam info alias president

Alias: president
User: bobama
```

---


## Deleting an Alias
### Syntax
```
gam delete alias <alias>
```
removes an alias.

### Example
This example will remove the alias
```
gam delete alias sales
```

---


# Determining if an email address is a User, Alias or Group
### Syntax
```
gam whatis <email address>
```
determines if the given email address is a user, alias or group and prints out information about the given resource.

### Example
This example looks up info@acme.com and determines that it is an alias.
```
gam whatis info@acme.com
info@acme.com is not a user...
info@acme.com is an alias

 Alias Email: info@acme.com
 User Email: jdoe@acme.com
```

---


# Resource Calendars
## Creating a Resource Calendar
### Syntax
```
gam create resource <id> <Common Name> [description <description>] [type <type>]
```
create a calendar resource. id is the short name of the calendar and is used to identify it. Common Name is a longer more detailed name, use quotes around the common name if it contains spaces. The optional argument description allows you enter further details about the calendar resource. The optional argument type allows you to classify the resource. For details on using the type argument to organize your resource calendars, see Google's [guidance on organizing resource calendars](https://developers.google.com/google-apps/calendar-resource/#developing_a_naming_strategy_for_your_calendar_resources).

### Example
This example will create a calendar resource
```
gam create resource business-calendar "Acme Inc. Business Calendar"
```

This example will create a calendar with optional attributes
```
gam create resource ed101 "ED101 Conference Room" description "Conference Room containing conference phone, whiteboard and projector" type "Conference Room"
```

---


## Updating a Resource Calendar
### Syntax
```
gam update resource <id> [name <Name>] [description <Description>] [type <Type>]
```
update a calendar resource. Required argument id is the short name of the calendar and is used to identify it. Optional argument name is the resources Common Name and allows you to change the resource calendar name that users see. The optional argument description allows you enter further details about the calendar resource. The optional argument type allows you to classify the resource. For details on using the type argument to organize your resource calendars, see Google's [guidance on organizing resource calendars](http://code.google.com/googleapps/domain/calendar_resource/docs/1.0/calendar_resource_developers_guide_protocol.html#naming_strategy).

### Example
This will update the calendar resource, changing the common name, description and type
```
gam update resource board-room name "Board Room 1" description "Board Room #1 with 25 seats and projector" type "Conference Room"
```

---


## Retrieving Resource Calendar Information
### Syntax
```
gam info resource <id>
```
retrieve information for a calendar resource. Required argument id is the short name of the calendar and is used to identify it.

### Example
```
gam info resource ed101
 Resource ID: ed101
 Common Name: ED101 Conference Room
 Email: jay.powerposters.org_6564313031@resource.calendar.google.com
 Type: Conference Room
```

---


## Deleting a Resource Calendar
### Syntax
```
gam delete resource <id>
```
delete a calendar resource. Required argument id is the short name of the calendar and is used to identify it.

### Example
```
gam delete resource ed101
```