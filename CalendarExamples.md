(TODO: Add table of contents.)

_**Comments have been turned off for these help pages, please post your questions and comments to the [Mailing List](http://groups.google.com/group/google-apps-manager)**_

GAM now supports Google Calendar Management with the ability to modify Access Control Lists (ACLs) for calendars and to add, list and remove calendars from a users Google Calendar display. GAM can work with user primary and secondary calendars as well as resource calendars.

All Google Calendars have an email address associated with them. All users who have the Calendar service enabled have a primary calendar identified by their email address. Secondary calendars created by or for the user have a special calendar email address which can be learned with the ` gam user <username> show calendars ` command. Resource Calendars also have a special email address that can be learned with the ` gam print resources ` command.

# Modifying and Viewing Calendar Access Control Lists (ACLs)
## Viewing a Calender's ACL
### Syntax
```
gam calendar <calendar email> showacl
```
Prints the ACLs for the given calendar. The ACL list will show who has access to the calendar and what level of access they have.

### Example
This example displays the Calendar ACLs for joe@acme.com
```
gam calendar joe@acme.com showacl
```

---


## Adding Users to a Calendar's ACL
### Syntax
```
gam calendar <calendar email> add freebusy|read|editor|owner <user email>
```
Gives user email the desired level of access to the given calendar by adding the user to the ACL. freebusy allows the user to see only times whe n the calendar is busy without showing event details. read gives the user rights to view but not edit the calendar. editor gives read/write access to the calendar but not ACL or settings modification rights. owner gives the user full access to the calendar with the ability to modify the ACL and calendar settings.

**Note:** The special users domain and default cannot be added to a calendar, they can only be updated or deleted by GAM (see below)

**Note:** giving a user rights to another calendar adds that calendar to their list of calendars automatically. A separate command to add the calendar should not be necessary.

### Example
This example gives Bob editor access to Joe's primary calendar.
```
gam calendar joe@acme.com add editor bob@acme.com
```

---


## Updating a User Entry in a Calendar ACL
### Syntax
```
gam calendar <calendar email> update freebusy|read|editor|owner <user email>
```
Update the given user's rights to the given calendar. The user should already have explicit access to the calendar. This command will upgrade (or downgrade) the user's access to the desired level of freebusy, read, editor or owner.

**Note:** the special users domain and default can be used instead of an actual user email address to modify public sharing of the calendar. domain applies to all users in the Google Apps organization. default applies to anyone with a Google account (even @gmail.com) and is limited to read or freebusy. Note that your Calendar control panel settings may prevent read sharing of calendars outside the domain in which case you'll get an error trying to set default to read.

### Example
This example upgrades Bog to be owner of Joe's Calendar:
```
gam calendar joe@acme.com update owner bob@acme.com
```

This example allows anyone with an account in your domain to edit the given resource calendar (including delete others appointments!).

```
gam calendar example.com_436d6e646572656e6365526f6f6d732d3239352d3372642d5164616d536d6974682d38@resource.calendar.google.com update editor domain
```

This example allows anyone with a Google account to view Bob's calendar
```
gam calendar bob@example.com update read default
```

---


## Deleting Users from a Calendar's ACL
### Syntax
```
gam calendar <calendar email> delete user <user email>
```
Removes user email rights to the given calendar. Note that the user may still have some level of rights (freebusy or read) to the calendar based on the default level of access to calendars set within the domain.

**Note:** deleting the domain and default users disables public sharing of your calendar. domain applies to everyone in your Google Apps domain while default applies to everyone with a Google Account.

### Example
This example removes Bob's direct rights to Joe's calendar
```
gam calendar joe@acme.com delete user bob@acme.com
```

These two examples remove all public sharing of Bob's calendar. Only those with explicit rights will be able to see anything (including freebusy):

```
gam calendar bob@example.com delete user domain
gam calendar bob@example.com delete user default
```

---


# Viewing and Modifying a User's List of Calendars
## Showing the Calendars a User Has Listed
### Syntax
```
gam user <user> show calendars
```
Lists the Calendars the user has listed in their Google Calendar.

### Example
This example lists the calendars that Bob has added to his Google Calendar app
```
gam user bob@acme.com show calendars

bob@acme.com's Calendar List
  Name: bob@acme.com
    ID: bob@acme.com
    Access Level: owner
    Timezone: America/New_York
    Hidden: false
    Selected: false
    Color: #2F6309
  Name: test
    ID: acme.com_r7vmefng3okeo4l48n4urkjvcg@group.calendar.google.c
m
    Access Level: root
    Timezone: America/New_York
    Hidden: false
    Selected: true
    Color: #2952A3
  Name: Canadian Holidays
    ID: en.canadian#holiday@group.v.calendar.google.com
    Access Level: read
    Timezone: America/New_York
    Hidden: false
    Selected: true
    Color: #2952A3
```

---


## Deleting a Calendar from a User(s) List of Calendars
### Syntax
```
gam user <user>|group <group>|ou <ou>|all users delete calendar <calendar email>
```
Removes the given calendar from each of the users' list of calendars. Deleting a calendar from a user's calendar list does not change ACLs on the calendar, it simply removes it from the display.

### Example
This example removes Joe's calendar from Bob's display of calendars.
```
gam user joe@acme.com delete calendar bob@acme.com
```

---


## Adding a Calendar to a User(s) List of Calendars
### Syntax
```
gam user <user>|group <group>|ou <ou>|all users add calendar <calendar email> [selected true|false] [hidden true|false] [color #XXXXXX]
```
Adds the given calendar to each of the users' list of calendars. Adding a calendar to a user's calendar list does not give them any rights to the calendar that they didn't have before. If the user does not have rights to the calendar, use the ACL command above to both grant them rights and add the calendar to their list of calendars.

The optional argument selected determines if the calendar is selected in the user's list of subscribed calendars by default. The optional argument hidden determines if the calendar is hidden from the user's list of subscribed calendars. The optional argument color determine's the HTML color of the calendar. Color must be one of the HTML codes listed  [in the Google Calendar API reference page](http://code.google.com/apis/calendar/data/2.0/reference.html#gcal_reference).

### Example
The following example adds Bob's calendar to Joe's list of calendars without it being selected in Joe's calendar display.

```
gam user joe@acme.com add calendar bob@acme.com selected false
```

---


## Updating a Calendar in a User(s) List of Calendars
### Syntax
```
gam user <user>|group <group>|ou <ou>|all users update calendar <calendar email> [selected true|false] [hidden true|false] [color #XXXXXX]
```
Update how a given calendar is displayed in a user's list of calendars. The optional argument selected determines if the calendar is selected in the user's list of subscribed calendars by default. The optional argument hidden determines if the calendar is hidden from the user's list of subscribed calendars. The optional argument color determine's the HTML color of the calendar. Color must be one of the HTML codes listed  [in the Google Calendar API reference page](http://code.google.com/apis/calendar/data/2.0/reference.html#gcal_reference).

### Example
The following example updates Bob's view of Joe's calendars, changing the color to green.

```
gam user bob@acme.com update calendar joe@acme.com color #0D7813
```

---


# Wiping a User's Primary Calendar
### Syntax
```
gam calendar <user email> wipe
```
Wipe all data from a user's primary calendar. **WARNING: This will delete all user events and there is no way to recover them!** Email address must be a Google Apps user. It's not possible to wipe resource or secondary calendars.

**Note:** You cannot use an anonymous OAuth client ID and secret with this command. You'll need to follow the [OAuth console key instructions](wiki/GettingAnOAuthConsoleKey) except that instead of turning on the Groups Settings API, the Google Calendar API should be turned on (which does not require a request and manual Google approval).

**Note:** If you used a version of GAM earlier than 2.51 to create the OAuth authorization you are using (oauth.txt), you'll need to re-authorize since the wipe command requires an additional scope. If you're seeing 403 Forbidden errors, this is probably the reason why. Just run [gam oauth revoke](wiki/OAuthKeyManagement#Revoking_an_OAuth_Token) and then re-run the wipe command to re-authorize.
### Example
The following example deletes all data for Joe's Calendar.

```
gam calendar joe@acme.com wipe
```

---
