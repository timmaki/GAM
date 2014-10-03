(TODO: Add table of contents.)

_**Comments have been turned off for these help pages, please post your questions and comments to the [Mailing List](http://groups.google.com/group/google-apps-manager)**_

# Users
## Creating a User
### Syntax
```
gam create user <email address> firstname <First Name> lastname <Last Name> password <Password> [suspended on|off] [changepassword on|off] [gal on|off] [admin on|off] [sha] [md5] [crypt] [nohash] [org <Org Name>]
```
Create a user account. firstname, lastname and password arguments are optional and should be single quoted if they contain spaces or special characters like ! or $ that the shell might try to interpret. If not set, firstname and lastname will default to "Unknown" and password will default to a random, 25-character string. Optional parameter "suspended on" creates the account but marks it as suspended (suspended off, AKA active is the default).  The optional parameter "changepassword on" will force the user to change their password after their first successful login (changepassword off is the default). The optional parameter "gal off" will hide the user from the Global Address List. This user will not be searchable in the Contacts Directory and will not autocomplete for other users composing emails unless they already have the user in their personal contacts (gal on is the default). The optional parameter "admin on" makes the user a Google Apps Super Admin (admin off is the default). The optional parameters sha, md5 and crypt indicate that the password is a hash of the given type. By default, if neither sha1, crypt or md5 are specified, GAM will do a sha1 hash of the provided password and send the hash instead of the plain text password for an additional layer of security. However, when hashes are sent, Google is unable to ensure password length and strength so it's possible to set passwords that do not conform to Google's length requirement this way. The optional parameter nohash disables GAM's automatic hashing of the password (password is still sent over encrypted HTTPS) so that Google can evaluate the length and strength of the password. Optional parameter org moves the user into the desired Organizational Unit. At the same time a user account is created, rich profile information for the user such as phone numbers, organizational information, address and IM can be set. For details on profile fields, see Setting User Profile Details at Create or Update.

### Example
This example creates a user account. Note that the password is in single quotes to prevent the shell from acting on the special characters.

```
gam create user droth firstname "David Lee" lastname Roth password 'MightAsWellJump!'
```

This example creates a user who is hidden from the GAL, forced to change their password after first login and a super admin.

```
gam create user jsmith gal off changepassword on admin on
```

---


## Update and Rename a User
### Syntax
```
gam update user <email address> [firstname <First Name>] [lastname <Last Name>] [password <Password>] [email <New Email>] [gal on|off] [admin on|off] [suspended on|off] [sha] [md5] [crypt] [nohash] [changepassword on|off] [org <Org Name>]
```
Update a user account. firstname, lastname and password arguments are optional and should be single quoted if they contain spaces or special characters like $ or ! that may be interpreted by the shell. Username is optional and will rename the user's account name (and thus their email address). admin, gal and suspended are optional and can be turned on or off. sha, crypt and md5 arguments are optional and indicate that the password specified is a hash of the given type. By default, if neither sha, crypt or md5 are specified, GAM will do a sha hash of the provided password and send the hash instead of the plain text password for an additional layer of security. However, when hashes are sent, Google is unable to ensure password length and strength so it's possible to set passwords that do not conform to Google's length requirement this way. The optional parameter nohash disable's GAM's automatic hashing of the password (password is still sent over encrypted HTTPS) so that Google can evaluate the length and strength of the password. changepassword is optional and indicates whether the user should be forced to change their password on next login. Optional parameter org allows the user to be moved into the desired Organization.

At the same time a user account is created, rich profile information for the user such as phone numbers, organizational information, address and IM can be set. For details on profile fields, see Setting User Profile Details at Create or Update.

Google makes the following recommendations when renaming a user account:
  * Before renaming a user, it is recommended that you logout the user from all browser sessions and services. For instance, you can get the user on your support desk telephone line during the rename process to ensure they have logged out. The process of renaming can take up to 10 minutes to propagate across all services.
  * Google Talk will lose all remembered chat invitations after renaming. The user must request permission to chat with friends again.
  * When a user is renamed, the old username is retained as a alias to ensure continuous mail delivery in the case of email forwarding settings and will not be available as a new username. If you prefer not to have the alias in place after the rename, you'll need to [Delete the Alias](wiki/ExamplesProvisioning#Deleting_an_Alias)

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


## Setting User Profile Details at Create or Update
### Syntax
Line breaks are for readability, when run, command should be one long line.
```
gam create|update user <email address>
[relation <relation type> <relation value>]
[externalid <id type> <id value>]
[phone type <phone type> value <phone value> primary|notprimary]
[organization name <org name> title <org title> type <org type> department <org dept> symbol <org symbol> costcenter <org cost center> location <org location> description <org desc> domain <org domain> primary|notprimary]
[address type <address type> unstructured <unstructered address> pobox <address pobox> extendedaddress <address extended address> streetaddress <address street address> locality <address locality> region <address region> postalcode <address postal code> countrycode <address country code> primary|notprimary]
[im type <im type> protocol <im protocol> primary <im value>]
```

Updates the rich profile information for a user at the same time the user is created or updated (single API call). These additional attributes can all be specified in one GAM command but are separated in the documentation for clarity. All attributes are optional and will show in the user's directory information assuming they have not been hidden from the Global Address List (gal off). The relation attribute allows you to set a relation of the user (e.g. manager). Relation value should be the relations email address in most cases. externalid allows you to specify other identification attributes or numbers for the user. Note that these are visible within the directory so private information like social security numbers or unique org identifiers should not be used. The phone attribute allows you to set phone numbers where the user can be reached. The organization attribute allows you to describe organizations which the member is a part of as well as their role and placement in the org, note that this is entirely unrelated to the Google Apps org setting. The address attribute allows you to set the addresses of a user. The address can be structured with each field separated or unstructured (one large address not broken into fields). The im attribute allows you to set instant messaging addresses for the user.

### Examples
This example will set multiple organizations, addresses, relations, managers and phones for the user.

```
gam.py update user jsmith@acme.org
relation manager admin@acme.org
relation spouse psmith@mymail.com
externalid employeeID 1234567
externalID "Frequent Flyer Number" ac321905
phone type mobile value 321-654-0987 notprimary
phone type work value 123-457-7890 primary
organization name "Acme Inc." type "Work" title "Product Manager" department "Wafers Division" symbol "ACME" costcenter 1234 location "Richmond Office" domain acme.org primary
organization name "ACME Softball Team" type unknown title "Pitcher" description "2.3 ERA" notprimary
im type work protocol gtalk primary jsmith@acme.org
im type home protocol jabber jsmith@jabber.org
```

---

## Get User Info
### Syntax
```
gam info user <email address> [nogroups]
```
retrieve details about the given user. GAM will print out a summary of the user. By default, GAM will retrieve the user's group membership which results in an additional API call. If you do not require this information you can disable it by specifying nogroups.

### Example
This example will show information on the user
```
gam info user rstarr

User: rstarr@acme.org
First Name: Ringo
Last Name: Starr
Is a Super Admin: False
Is Delegated Admin: False
Has Agreed to Terms: True
IP Whitelisted: False
Account Suspended: False
Must Change Password: False
Google Unique ID: 117553266811361050021
Customer ID: C02azef93
Mailbox is setup: True
Included in GAL: False
Creation Time: 2011-08-24T12:08:44.000Z
Last login time: 2013-05-08T16:58:54.000Z
Google Org Unit Path: /Google Users

IMs:
 protocol: gtalk
 im: rstarr@acme.org
 type: work
 primary: True

 protocol: jabber
 im: rstarr@jabber.org
 type: home

Addresses:
 countryCode: US
 locality: Richmod
 region: VA
 primary: True
 streetAddress: 321 Acme Rd
 postalCode: 03920
 type: work

 sourceIsStructured: False
 type: home
 formatted: 250 Robins Lane, Richmond, VA 03920

Organizations:
 domain: acme.org
 name: Acme Inc.
 title: Product Manager
 symbol: ACME
 customType:
 primary: True
 location: Richmond Office
 costCenter: 1234
 department: Wafers Division

 description: 2.3 ERA
 customType:
 name: ACME Softball Team
 title: Pitcher

Phones:
 type: mobile
 value: 321-654-0987

 type: work
 primary: True
 value: 123-457-7890

Relations:
 type: manager
 value: admin@acme.org

 type: spouse
 value: psmith@mymail.com

External IDs:
 type: employeeID
 value: 1234567

 type: Frequest Flyer Number
 value: ac321905

Email Aliases:
  ringo@acme.org
  ringo.starr@acme.org

Non-Editable Aliases:
  ringo@acme-alias.org
  ringo.starr@acme-alias.org

Groups:
  2sv <2sv@acme.org>
  users <users@acme.org>
```

---


## Delete a User
### Syntax
```
gam delete user <email address>
```
delete the given user's account.

### Example
This example deletes Pete Best's account
```
gam delete user pbest
```

---


## Undelete a User
### Syntax
```
gam undelete user <email address>
```
Undeletes a user account deleted in the last 5 days. In order to undelete a user, there must not be any other users or groups with conflicting primary or alias email addresses. See Google's [Restore a recently deleted user](http://support.google.com/a/bin/answer.py?hl=en&answer=1397578) documentation for more help.

# Groups
## Create a Group
### Syntax
```
gam create group <group email> [name <Group Name>] [description <Group Description>]
```
create a group. Group Name and Description are optional and set the groups full name and description. Use quotes around them if they contain spaces. If the Google Groups for Business (user-managed groups) service is enabled for the Google Apps domain, additional groups security settings are available and can be set with the same GAM command as described on the [Groups Settings page](wiki/GAM3GroupSettings#Updating__Group_Settings).

### Example
This example creates a group:
```
gam create group mygroup@example.com
```

This example creates a group and [sets max message size](wiki/GAM3GroupSettings#Max_Message_Bytes) to 25mb
```
gam create group large_attachments@acme.org maxmessagebytes 25m
```

---


## Update and Rename a Group
### Syntax
```
gam update group <group email> [name <Group Name>] [description <Group Description>] [email <new email address>]
```
modifying a groups name, description or email address. When changing a group's email address, the new address must not already be in use. Note that unlike renaming a user, the group's old address is NOT retained as an alias. If you'd like to keep the group's old address, you should immediately add it back via the [Create Alias](wiki/GAM3DirectoryCommands#Creating_an_Alias_for_a_User_or_Group) command.

If the Google Groups for Business (user-managed groups) service is enabled for the Google Apps domain, additional groups security settings are available and can be set with the same GAM command as described on the [Groups Settings page](wiki/GAM3GroupSettings#Updating__Group_Settings).

### Example
This example modifies the group, changing it's name and description
```
gam update group beatles name "The Beatles Rock Band" description "British Invasion Band"
```

This example modifies the group, changing it's description and [allowing posters from other domains](wiki/GAM3GroupSettings#Allow_External_Members).
```
gam update group beatles name "The Beetles" allow_external_members true
```

---


## Add Members/Owners/Managers to a Group
### Syntax
```
gam update group <group email> add owner|member|manager {user <email address> | group <group address> | org <org name> | file <file name> | all users}
```
add members, owners or managers to a group. You can specify a single user, a group of users, an org of users, a file with users (one per line), or "all users" for all users in Google Apps.

### Example
This example adds a manager to the group
```
gam update group beatles add manager user rstarr@beatles.com
```

This example adds all members in the Google Apps domain to a group
```
gam update group everyone add member all users
```

---


## Update Members/Owners/Managers in a Group
### Syntax
```
gam update group <group email> update owner|member|manager {user <email address> | group <group address> | org <org name> | file <file name> | all users}
```
update members, owners or managers in a group. You can specify a single user, a group of users, an org of users, a file with users (one per line), or "all users" for all users in Google Apps. The specified users who are already a member of the group will have their membership type changed to the specified level.

### Example
This example makes a user who is currently a manager of a group an owner
```
gam update group beatles update owner user rstarr@beatles.com
```

---


## Sync owners/members/managers to a Group
### Syntax
```
gam update group <group email> sync owner|member|manager {user <email address> | group <group address> | org <org name> | file <file name> | all users}
```

Adds/removes users from the specified group in order to sync membership with the specified entity. The sync operation should result in a minimal amount of API calls when some of the specified users are already in the group. When adding users, their membership type (member, manager, owner) will be set as specified in the command but existing members not being removed will not see their membership type change.

### Example
This example syncs the students@acme.edu group membership with the "Students" Org Unit in Google.
```
gam update group students@acme.edu sync member org "Students"
```

---


## Remove Users from a Group
### Syntax
```
gam update group <group email> remove {user <email address> | group <group address> | org <org name> | file <file name> | all users}
```
Remove users from the given group. The users are completely removed from the group whether they were a member, owner or manager.

### Example
This command removes a user from a group.

```
gam update group students remove user grad@school.edu
```

this example removes all current members from a group
```
gam update group membersclub@acme.org remove group membersclub@acme.org
```

---


## Get Group Info
### Syntax
```
gam info group <group email>
```
retrieve information about a given group.

### Example
This example will provide information about the group
```
gam info group beatles

 nonEditableAliases:
   beatles@acme-alias.org
   the-beatles@acme.org
 description:
 adminCreated: True
 email: test6@jay.powerposters.org
 aliases:
   the-beatles@acme.org
 id: 02ce457m25wwh7z
 name: beatles@acme.org
 allowExternalMembers: false
 whoCanJoin: CAN_REQUEST_TO_JOIN
 whoCanViewMembership: ALL_MANAGERS_CAN_VIEW
 defaultMessageDenyNotificationText:
 includeInGlobalAddressList: true
 archiveOnly: false
 isArchived: true
 membersCanPostAsTheGroup: true
 allowWebPosting: true
 messageModerationLevel: MODERATE_NONE
 replyTo: REPLY_TO_LIST
 customReplyTo:
 sendMessageDenyNotification: false
 messageDisplayFont: DEFAULT_FONT
 whoCanPostMessage: ALL_IN_DOMAIN_CAN_POST
 whoCanInvite: ALL_MANAGERS_CAN_INVITE
 spamModerationLevel: ALLOW
 whoCanViewGroup: ALL_MEMBERS_CAN_VIEW
 showInGroupDirectory: false
 maxMessageBytes: 25M
 allowGoogleCommunication: true
Members:
 member: rstarr@acme.org (user)
 member: gharrison@acme.org (user)
 owner: jlennon@acme.org (user)
 owner: pmccartney@acme.org (user)
```

---


## Delete a Group
### Syntax
```
gam delete group <group email>
```
Delete a given group.

### Example
This example will delete the group
```
gam delete group beatles
```

---


# Email Aliases
## Creating an Alias for a User or Group
### Syntax
```
gam create alias <alias> user|group|target <primary address>
```
Create an alias for the given user or group. user or group should be specified based on whether the target primary address is a user or group. If it's unknown which it is, target can be specified in which case both will be tried.

### Example
This example will create an alias for a user
```
gam create alias theking user epresley
```

This example will create an alias for a group
```
gam create alias the-beatles group beatles
```

This example will create an alias for target jimmy-hendrix whether it's a user or a group
```
gam create alias the-jimmy-hendrix target jimmy-hendrix
```

---


## Updating an Alias
### Syntax
```
gam update alias <alias> user|group|target <user name>
```
update an existing alias, changing the user or group it points to.

### Example
This example will update an existing alias, pointing it at another user
```
gam update alias ceo user sbalmer
```

---


## Retrieving Alias Information
### Syntax
```
gam info alias <alias>
```
retrieve information about the given alias.

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


# Determine if an Email Address is a User, Alias or Group
### Syntax
```
gam whatis <email address>
```
determines if the given email address is a user, alias, group or group alias and prints out information about the given resource.

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


# Mobile Devices
## Perform Wipe, Approve and Other Actions on Mobile Devices
### Syntax
```
gam update mobile <mobile id> action wipe|approve|block|cancel_remote_wipe_then_activate|cancel_remote_wipe_then_block
```

Perform the given action on a mobile device. The mobile id must be specified and can be found by listing all mobile devices. wipe will tell the mobile device to perform a full data reset on next sync. approve will allow the device to sync with Google Apps. block will block sync attempts from the device. cancel\_remote\_wipe\_then\_activate and cancel\_remote\_wipe\_then\_block will cancel a remote wipe and then set the status to approved or blocked accordingly.

### Example
This example will wipe the given device.

```
gam update mobile AFiQxQ8n8E7HjDsk13hHSoAIfF6NE78bUsfqjXkrLquNnBo5OyJrn7tR1bnKJmeaT7a_o_hElS1blK0nvNfxOCBnR-Wa5VE9VBbUOzEwK4w-Ik61wkrmtlo action wipe
```

---


## Get Info on a Mobile Device
### Syntax
```
gam info mobile <mobile id>
```

Print info about the given mobile device.

### Example
```
gam info mobile AFiQxQ8n8E7HjDsk13hHSoAIfF6NE78bUsfqjXkrLquNnBo5OyJrn7tR1bnKJmeaT7a_o_hElS1blK0nvNfxOCBnR-Wa5VE9VBbUOzEwK4w-Ik61wkrmtlo

 status: APPROVED
 lastSync: 2013-03-31T01:05:52.164Z
 name: John Smith
 firstSync: 2013-03-29T01:03:54.990Z
 resourceId: AFiQxQ8n8E7HjDsk13hHSoAIfF6NE78bUsfqjXkrLquNnBo5OyJrn7tR1bnKJmeaT7a_o_hElS1blK0nvNfxOCBnR-Wa5VE9VBbUOzEwK4w-Ik61wkrmtlo
 hardwareId: 
 deviceId: android946305472025
 type: GOOGLE_SYNC
 userAgent: Android/4.2.2-EAS-1.3,gzip(gfe)
 model: Unknown
 os: Unknown
 email: jsmith@acme.org
```

---


## Delete a Mobile Device
### Syntax
```
gam delete mobile <mobile id>
```

Deletes the given mobile device. Note that this does not break the device's sync, it simply removes it from the list of devices connected to the domain. If the device still has a valid login/authentication, it will be added back on it's next successful sync.

### Example
This example deletes the given mobile device.

```
gam delete mobile AFiQxQ8n8E7HjDsk13hHSoAIfF6NE78bUsfqjXkrLquNnBo5OyJrn7tR1bnKJmeaT7a_o_hElS1blK0nvNfxOCBnR-Wa5VE9VBbUOzEwK4w-Ik61wkrmtlo
```

# Chrome OS Devices
## Updating Chrome OS Devices
### Syntax
```
gam update cros <device id> [user <user info>] [location <location info>] [notes <notes info>] [ou <new org unit>]
```

Updates information about the given Chrome OS device. <device id> can be determined using the [gam print cros](wiki/GAM3CSVListings#Print_Chrome_OS_Devices) command. user, location and notes information is optional. ou is optional and allows the Chrome device to be moved to a new Google organizational unit, changing the policies that will be applied to the device.

### Example
This example will update the user, location and notes for the given Chromebook.

```
gam update cros 647cf127-ab85-4c2b-b07e-63ad1b705c19 user jsmith@acme.org location "Richmond Office" notes "tracking ID #329234"
```

This example moves the Chrome device into a OU configured for Kiosk / Public Session mode.
```
gam update cros 647cf127-ab85-4c2b-b07e-63ad1b705c19 ou "Kiosk Chromebooks"
```

---


## Getting Info About a Chrome OS Device
### Syntax
```
gam info cros <device id>
```

Print out information about the given Chrome OS device.

### Example
This example will print out information about the given Chromebook.
```
gam info cros 647cf127-ab85-4c2b-b07e-63ad1b705c19

 status: ACTIVE
 lastSync: 2013-03-28T23:40:00.014Z
 lastEnrollmentTime: 2013-02-23T20:03:35.332Z
 orgUnitPath: /Chromebooks
 notes: Jay's Chromebook
 serialNumber: HY3A91ECA01698
 annotatedUser: jsmith@acme.org
 bootMode: Verified
 deviceId: 647cf127-ab85-4c2b-b07e-63ad1b705c19
 platformVersion: 3701.62.0 (Official Build) beta-channel daisy
 osVersion: 26.0.1410.40
 firmwareVersion: Google_Snow.2695.117.0
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