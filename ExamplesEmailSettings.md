- [General Settings](#general-settings)
  - [Set User Language](#set-user-language)
  - [Set Messages Per Page](#set-messages-per-page)
  - [Enable/Disable Keyboard Shortcuts](#enabledisable-keyboard-shortcuts)
  - [Enable/Disable Personal Indicator Arrows](#enabledisable-personal-indicator-arrows)
  - [Enable/Disable Email Snippets](#enabledisable-email-snippets)
  - [UTF-8 (Unicode) for outgoing mail](#utf-8-unicode-for-outgoing-mail)
  - [Enable/Disable Webclips](#enabledisable-webclips)
- [Signatures and Away Messages](#signatures-and-away-messages)
  - [Retrieving a Signature](#retrieving-a-signature)
  - [Enabling/Disabling and Setting a Vacation (Away) Message](#enablingdisabling-and-setting-a-vacation-away-message)
  - [Retrieving Vacation Settings](#retrieving-vacation-settings)
- [Labels and Filters](#labels-and-filters)
  - [Create a Label](#create-a-label)
  - [Retrieving User's Labels](#retrieving-users-labels)
  - [Delete a Label](#delete-a-label)
  - [Create a Filter](#create-a-filter)
- [Send As, IMAP, POP and Forwarding](#send-as-imap-pop-and-forwarding)
  - [Setting Send As (Custom From)](#setting-send-as-custom-from)
  - [Retrieving Send As (Custom From)](#retrieving-send-as-custom-from)
  - [Setting IMAP Settings](#setting-imap-settings)
  - [Retrieving IMAP Settings](#retrieving-imap-settings)
  - [Setting POP Settings](#setting-pop-settings)
  - [Retrieving POP Settings](#retrieving-pop-settings)
  - [Setting a Forward](#setting-a-forward)
  - [Retrieving Forward Settings](#retrieving-forward-settings)
- [Delegates](#delegates)
  - [Creating a delegate](#creating-a-delegate)
  - [Retrieving delegates](#retrieving-delegates)
  - [Deleting a delegate](#deleting-a-delegate)
- [Hiding/Unhiding users from the domain contacts](#hidingunhiding-users-from-the-domain-contacts)
  - [Changing a users profile to hidden/unhidden](#changing-a-users-profile-to-hiddenunhidden)
  - [Showing users profile hidden/unhidden status](#showing-users-profile-hiddenunhidden-status)
- [User Profile Photos](#user-profile-photos)
  - [Updating Profile Photos](#updating-profile-photos)
  - [Getting Profile Photos](#getting-profile-photos)
  - [Deleting Profile Photos](#deleting-profile-photos)

# General Settings
## Set User Language
### Syntax
```
gam user <username>|group <groupname>|ou <ouname>|all users language <language code>
```
set the display language used for the user. A full list of language codes can be found [here.](https://developers.google.com/admin-sdk/email-settings/?csw=1#language_tags) Note that language changes can take several hours to appear in the user's interface and may require the user to log out and log back in.

### Example
This example sets the user's language to UK English
```
gam user jlennon language en-GB
```

---


## Set Messages Per Page
### Syntax
```
gam user <username>|group <groupname>|ou <ouname>|all users pagesize 25|50|100
```
determine how many messages a user will see on a web page when viewing their Inbox or other labels.

### Example
This example sets the page size to 50 for the user
```
gam user jhendrix pagesize 50
```

---


## Enable/Disable Keyboard Shortcuts
### Syntax
```
gam user <username>|group <groupname>|ou <ouname>|all users shortcuts on|off
```
enable/disable keyboard shortcuts for the given users. List of shortcuts can be found [here.](http://mail.google.com/support/bin/answer.py?hl=en&answer=6594)

### Example
This example turns keyboard shortcuts on for all users
```
gam all users shortcuts on
```

---


## Enable/Disable Personal Indicator Arrows
### Syntax
```
gam user <username>|group <groupname>|ou <ouname>|all users arrows on|off
```
enable/disable personal indicator arrows for the given users. Personal indicator arrows are described [here.](http://mail.google.com/support/bin/answer.py?hl=en&answer=8156)

### Example
This example turns personal indicator arrows off for the user
```
gam user jamesdean arrows off
```

---


## Enable/Disable Email Snippets
### Syntax
```
gam user <username>|group <groupname>|ou <ouname>|all users snippets on|off
```
enable/disable message snippets in Inbox and other message lists.

### Example
This example turns snippets off for the group newbies
```
gam group newbies snippets off
```

---


## UTF-8 (Unicode) for outgoing mail
### Syntax
```
gam user <username>|group <groupname>|ou <ouname>|all users utf on|off
```
turn UTF-8 (Unicode) encoding of outgoing mail on or off.

### Example
This example sets UTF-8 outgoing mail encoding on for members of the faculty group
```
gam group faculty utf on
```

---


## Enable/Disable Webclips
### Syntax
```
gam user <username>|group <groupname>|ou <ouname>|all users webclips on|off
```
enable or disable webclips for the given users. Webclips are described [here](http://mail.google.com/support/bin/answer.py?hl=en&answer=18219).

### Example
This example disables webclips for all users
```
gam all users webclips off
```

---


# Signatures and Away Messages
## Setting a Signature
### Syntax
```
gam user <username>|group <groupname>|ou <ouname>|all users [signature <signature text>] [file <signature file>]
```
sets a email signature for the given users. Use quotes around the signature text if it contains spaces (which it almost certainly will). New lines can be specified with \n. HTML can also be used. An empty string like "" will disable the signature. Use the optional file argument to specify a filename that contains the signature text. This is easier for long, complex signatures.

### Example
This example sets all user's signatures to be:
```
Acme Inc
1321 Main Ave<br>
http://www.acme.com
```

```
gam all users signature
 "Acme Inc<br>1321 Main Ave<br>http://www.acme.com
```

This example reads the signature from a file:
```
gam user bob@example.com signature file bobs-html-sig.txt
```
----

## Retrieving a Signature
### Syntax
```
gam
 user <username> | group <groupname>| ou <ouname> | all users
 show signature<br>
```
gets the email signature for the given users.

### Example
This example shows all user's signature

```
gam all users show signature
```
----

## Enabling/Disabling and Setting a Vacation (Away) Message
### Syntax
```
gam
 user <username> | group <groupname> | ou <ouname> | all users
 vacation on|off subject <subject text>
 [message <message text>]
 [file <message file>]
 startdate <YYYY-MM-DD> enddate <YYYY-MM-DD>
 [contactsonly] [domainonly]
```
enable or disable a vacation/away message for the given users. subject will be the away message subject. message will be the message text. Use quotes around subject and message text if they contain spaces (which they probably will). If file is specified instead of message, the message will be read from the given text file. In the message text, \n will be replaced with a new line. The optional startdate and enddate arguments set a start and end date for the vacation message to be enabld. The optional argument contactsonly will only send away messages to persons in the user's Contacts. The optional argument domainonly will prevent vacation messages from going to users outside the Google Apps domain.

### Example
This example sets the away message for the user
```
gam user epresley vacation on subject "Elvis has left the building"
 message "I will be on Mars for the next 100 years. I'll get back to you when I return.\n\nElvis"
```

This example reads the message from a text file:
```
gam user bob@example.com vacation on subject "I am away" file bobs-away-message.txt
```
----

## Retrieving Vacation Settings
### Syntax
gam
 user <username> | group <groupname> |ou <ouname> | all users
 show vacation
```
show the given user's vacation message and settings.

## Example
This example shows the vacation settings for jsmith
```
gam user jsmith show vacation
```

## Labels and Filters
<h2>Create a Label</h2>
<h3>Syntax</h3>
<pre><code>gam user &lt;username&gt;|group &lt;groupname&gt;|ou &lt;ouname&gt;|all users label &lt;label name&gt;<br>
</code></pre>
create a Gmail Label for the given users. Use quotes around the label name if it contains spaces. Labels are described <a href='http://mail.google.com/support/bin/answer.py?hl=en&answer=118708'>here.</a>

<h3>Example</h3>
This example creates a label called New Label for all users<br>
<pre><code>gam all users label "New Label"<br>
</code></pre>
<hr />
<h2>Retrieving User's Labels</h2>
<h3>Syntax</h3>
<pre><code>gam user &lt;username&gt;|group &lt;groupname&gt;|ou &lt;ouname&gt;|all users show labels<br>
</code></pre>
show the labels for the given users. Default labels including inbox, unread, drafts, sent, chat, muted, spam, trash, popped, and contactcsv will not be shown. Label visibility and number of unread messages in label will also be reported.<br>
<br>
<h3>Example</h3>
This example shows the labels for all members of the marketing group<br>
<pre><code>gam group marketing show labels<br>
</code></pre>
<hr />

<h2>Delete a Label</h2>
<h3>Syntax</h3>
<pre><code>gam user &lt;username&gt;|group &lt;groupname&gt;|ou &lt;ouname&gt;|all users delete label &lt;label name&gt;<br>
</code></pre>
delete the given label for the given users.  Use quotes around the label name if it contains spaces. Labels are described <a href='http://mail.google.com/support/bin/answer.py?hl=en&answer=118708'>here.</a>

<h3>Example</h3>
This example deletes a label called Old Label for all users<br>
<pre><code>gam all users delete label "Old Label"<br>
</code></pre>
<hr />

<h2>Create a Filter</h2>
<h3>Syntax</h3>
<pre><code>gam user &lt;username&gt;|group &lt;groupname&gt;|ou &lt;ouname&gt;|all users filter<br>
  from &lt;email&gt;|to &lt;email&gt;|subject &lt;words&gt;|haswords &lt;words&gt;|nowords &lt;words&gt;|musthaveattachment<br>
  label &lt;label name&gt;|markread|archive|star|forward &lt;email address&gt;|trash|neverspam<br>
</code></pre>
create a Filter for the given users. Filter must have one or more conditions (from, to, subject, haswords, nowords or musthaveattachment) and one or more actions (label, markread, archive, star, forward, trash or neverspam). You do not need to create a label before creating a filter that labels messages, creating a filter that labels messages will automatically create the label. Filters are described <a href='http://mail.google.com/support/bin/answer.py?hl=en&answer=6579'>here.</a>

<b>Warning:</b> GAM cannot delete filters because Google has not provided a method for filter deletion in their APIs. Before creating filters for some or all users in your domain, please make sure you absolutely need/want them. The only way to get rid of them once created is to have each user manually delete them.<br>
<br>
<h3>Example</h3>
This example creates a filter for the user john that labels message from dianne@gmail.com and archives them (thus they will only appear under the label)<br>
<br>
<pre><code>gam user john filter from dianne@gmail.com label Dianne archive<br>
</code></pre>
<hr />

<h1>Send As, IMAP, POP and Forwarding</h1>
<h2>Setting Send As (Custom From)</h2>
<h3>Syntax</h3>
<pre><code>gam user &lt;username&gt;|group &lt;groupname&gt;|ou &lt;ouname&gt;|all users sendas &lt;email address&gt; &lt;name&gt; [default] [replyto &lt;email address&gt;]<br>
</code></pre>
allow the given users to send mail as another email address (also called Custom From). name is the nice name users see with the email (Use quotes if name includes spaces). Optionally, default specifies that this should be the address used for outgoing mail by default (user can choose which address mail is sent from when they compose). Also optional, replyto specifies a Reply To address to be used when mail is sent out via this sendas.<br>
<br>
<b>Note:</b> the email address must be under the direct control of your Google Apps account, the domain must be your Google Apps primary domain, a secondary domain or a domain alias.<br>
<br>
<h3>Example</h3>
This example will allow the user fjones to send mail as fredjones@yourcompany.com by default (it is assumed to fredjones@yourcompany.com is already setup as a user, group or nickname in your domain)<br>
<pre><code>gam user fjones sendas fjones@yourcompany.com "Fred Jones" default<br>
</code></pre>
<hr />

<h2>Retrieving Send As (Custom From)</h2>
<h3>Syntax</h3>
<pre><code>gam user &lt;username&gt;|group &lt;groupname&gt;|ou &lt;ouname&gt;|all users show sendas<br>
</code></pre>
show the given users Send As / Custom From addresses.<br>
<br>
<h3>Example</h3>
This example shows the send as settings for gwashington<br>
<pre><code>gam user gwashington show sendas<br>
</code></pre>

<h2>Setting IMAP Settings</h2>
<h3>Syntax</h3>
<pre><code>gam user &lt;username&gt;|group &lt;groupname&gt;|ou &lt;ouname&gt;|all users imap on|off<br>
</code></pre>
turn IMAP on or off for given users.<br>
<br>
<h3>Example</h3>
This example will turn IMAP on for all current users in the domain.<br>
<pre><code>gam all users imap on<br>
</code></pre>
<hr />

<h2>Retrieving IMAP Settings</h2>
<h3>Syntax</h3>
<pre><code>gam user &lt;username&gt;|group &lt;groupname&gt;|ou &lt;ouname&gt;|all users show imap<br>
</code></pre>
shows the given users' current IMAP settings.<br>
<br>
<h3>Example</h3>
This example shows all user's IMAP status.<br>
<pre><code>gam all users show imap<br>
</code></pre>
<hr />

<h2>Setting POP Settings</h2>
<h3>Syntax</h3>
<pre><code>gam user &lt;username&gt;|group &lt;groupname&gt;|ou &lt;ouname&gt;|all users pop on|off [for allmail|newmail] [action keep|archive|delete]<br>
</code></pre>
turn POP3 on or off for given users, "for allmail" will expose all Inbox mail to the POP client while "for newmail" will expose only mail received after POP was enabled. POPped mail can be left alone (keep), archived (archive) or deleted (delete). If the for and action arguments are not specified, all mail will be popped and kept in the Inbox.<br>
<br>
<h3>Example</h3>
This example will turn POP on for any users in the group students. All mail in the Inbox will be exposed to the POP client and POPped emails will be kept in the Inbox.<br>
<pre><code>gam group students pop on<br>
</code></pre>

This example will turn POP on for Bob but only for new mail he receives. Mail will be archived after it is popped:<br>
<pre><code>gam user bob@example.com pop on for newmail action archive<br>
</code></pre>
<hr />

<h2>Retrieving POP Settings</h2>
<h3>Syntax</h3>
<pre><code>gam user &lt;username&gt;|group &lt;groupname&gt;|ou &lt;ouname&gt;|all users show pop<br>
</code></pre>
show the given users' POP settings.<br>
<br>
<h3>Example</h3>
This example shows the pop settings for the group students<br>
<pre><code>gam group students show pop<br>
</code></pre>
<hr />

<h2>Setting a Forward</h2>
<h3>Syntax</h3>
<pre><code>gam user &lt;username&gt;|group &lt;groupname&gt;|ou &lt;ouname&gt;|all users forward on|off [email address] [keep|archive|delete]<br>
</code></pre>
enable/disable and set an automatic email forward for the given users. If turning forwarding on, an email address and action are both required. Actions (keep, archive and delete) specifies what to do with messages that have been forwarded.<br>
<br>
<b>Warning:</b> Google has recently taken steps to limit what email addresses forwards can be set to via the API (and thus via GAM). See <a href='http://googleappsupdates.blogspot.com/2010/05/gmail-now-requires-verification-of.html'>this blog post</a> for details about what domains you can set forwards to. Generally you are limited to forwarding to your primary domain, alias and secondary domains and subdomains of those.<br>
<br>
<h3>Example</h3>
This example sets a forward for the user, messages will be deleted after they are forwarded so they will not show up in the user's account<br>
<br>
<pre><code>gam user eclapton forward on eclapton@music.com delete<br>
</code></pre>
<hr />

<h2>Retrieving Forward Settings</h2>
<h3>Syntax</h3>
<pre><code>gam user &lt;username&gt;|group &lt;groupname&gt;|ou &lt;ouname&gt;|all users show forward<br>
</code></pre>
shows the given users' forwarding settings.<br>
<br>
<h3>Example</h3>
This example shows alincoln's forwarding settings.<br>
<pre><code>gam user alincoln show forward<br>
</code></pre>
<hr />

<h1>Delegates</h1>
A delegate is someone who has been given access to someone else's email and contacts. The delegator is the one whose email and contacts are accessible by the delegate. Delegate and the delegators must be in the same domain, granting delegate access across multiple domains is currently not possible.<br>
<br>
<h2>Creating a delegate</h2>
<h3>Syntax</h3>
<pre><code>gam user &lt;username&gt;|group &lt;groupname&gt;|ou &lt;ouname&gt;|all users delegate to &lt;delegate email&gt;<br>
</code></pre>
gives email and contact access for the given users (the delegators) to the specified delegate account. Unlike when users request delegate access via Gmail settings, no email will be sent to the delegators for approval, the approval occurs immediately. The delegate and the delegator must be in the same domain, granting delegate access across multiple domains is currently not possible.<br>
<br>
Both the Gmail delegator and the delegate:<br>
<br>
<ul><li>Must be active. A 500 error is returned if either user is suspended and disabled.<br>
</li><li>Must not require a change of password on the next sign in. A 500 error is returned if either user has this flag enabled in the control panel, or, using the Provisioning API, the changePasswordAtNextLogin attribute is true.</li></ul>

you can confirm these settings using the <a href='ExamplesProvisioning#Get_User_Info'>gam info user</a> command. Both "Account suspended" and "Must change password" should show false for both the delegate and the delegator.<br>
<br>
<h3>Example</h3>
This example gives jbezos access to the contacts and email of the sales account.<br>
<pre><code>gam user sales delegate to jbezos@amazon.com<br>
</code></pre>
<hr />

<h2>Retrieving delegates</h2>
<h3>Syntax</h3>
<pre><code>gam user &lt;username&gt;|group &lt;groupname&gt;|ou &lt;ouname&gt;|all users show delegates [csv]<br>
</code></pre>
shows the delegates that have access to the given user accounts. Optional argument csv prints out CSV style output instead of human readable.<br>
<br>
<h3>Example</h3>
This example shows delegates across the entire domain.<br>
<pre><code>gam all users show delegates<br>
</code></pre>
<hr />

<h2>Deleting a delegate</h2>
<h3>Syntax</h3>
<pre><code>gam user &lt;username&gt;|group &lt;groupname&gt;|ou &lt;ouname&gt;|all users delete delegate &lt;delegate email&gt;<br>
</code></pre>
deletes the delegate for the given users.<br>
<br>
<h3>Example</h3>
this example takes away deSecretary's access to deBoss's email and contacts.<br>
<br>
<pre><code>gam user deBoss delete delegate deSecretary<br>
</code></pre>
<hr />

<h1>Hiding/Unhiding users from the domain contacts</h1>
Individual user profiles can be hidden/unhidden from the domain contacts list (sometimes called the Global Address List or GAL).<br>
<br>
<h2>Changing a users profile to hidden/unhidden</h2>
<h3>Syntax</h3>
<pre><code>gam user &lt;username&gt;|group &lt;groupname&gt;|ou &lt;ouname&gt;|all users profile shared|unshared<br>
</code></pre>
Share a user's profile (contact) information with other users in the domain. If a user's profile is shared, they'll show up in autocomplete and contact searches for other users. If a user is unshared, others will not be able to discover the user's address and detailed contact info.<br>
<br>
<h3>Example</h3>
this example hides all users in the asked-to-be-hidden Google group from email address autocomplete and contact searches.<br>
<br>
<pre><code>gam group asked-to-be-hidden profile unshared<br>
</code></pre>
<hr />

<h2>Showing users profile hidden/unhidden status</h2>
<h3>Syntax</h3>
<pre><code>gam user &lt;username&gt;|group &lt;groupname&gt;|ou &lt;ouname&gt;|all users show profile<br>
</code></pre>
Show the current sharing status of the users' profile.<br>
<br>
<h3>Example</h3>
this example shows the status of all user profiles in the domain.<br>
<br>
<pre><code>gam all users show profile<br>
</code></pre>
<hr />

<h1>User Profile Photos</h1>
Support for user profile photo management has been added to GAM 2.3. Note that if you get errors about Authsub token invalid, you should delete the existing oauth.txt file and regenerate the OAuth authentication using GAM 2.3 so that the full Contacts API scope is included.<br>
<br>
<h2>Updating Profile Photos</h2>
<h3>Syntax</h3>
<pre><code>gam user &lt;username&gt;|group &lt;groupname&gt;|ou &lt;ouname&gt;|all users update photo &lt;photo filename&gt;<br>
</code></pre>
Create or replace the user's photo with the one specified by filename. File should be jpg format. You can use #user# as part of the filename and it will be replaced with the user's full email address.<br>
<br>
<br>
<h3>Example</h3>
this example replaces Michael Jones' photo with the one from the employee photo directory<br>
<br>
<pre><code>gam user michael.jones@acme.com update photo h:\employee-photos\mjones.jpg<br>
</code></pre>

this example replaces all user's photos with ones stored in c:\photos\<user email>.jpg<br>
<pre><code>gam all users update photo c:\photos\#user#.jpg<br>
</code></pre>
<hr />

<h2>Getting Profile Photos</h2>
<h3>Syntax</h3>
<pre><code>gam user &lt;username&gt;|group &lt;groupname&gt;|ou &lt;ouname&gt;|all users get photo<br>
</code></pre>
Gets the users' current photo and saves it to a file named username-domain.jpg in the GAM path. Note that if you get errors about Authsub token invalid, you should delete the existing oauth.txt file and regenerate the OAuth authentication using GAM 2.3 so that the full Contacts API scope is included.<br>
<br>
<br>
<h3>Example</h3>
This example retrieves photos for all users in Google Apps and saves them to files.<br>
<br>
<pre><code>gam all users get photo<br>
</code></pre>
<hr />

<h2>Deleting Profile Photos</h2>
<h3>Syntax</h3>
<pre><code>gam user &lt;username&gt;|group &lt;groupname&gt;|ou &lt;ouname&gt;|all users delete photo<br>
</code></pre>
Deletes the given users' profile photo returning it to blank. Note that if you get errors about Authsub token invalid, you should delete the existing oauth.txt file and regenerate the OAuth authentication using GAM 2.3 so that the full Contacts API scope is included.<br>
<br>
<h3>Example</h3>
This example will delete the profile photo for all members of the group named abused-the-system<br>
<br>
<pre><code>gam group abused-the-system delete photo<br>
</code></pre>
---