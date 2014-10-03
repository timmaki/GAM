<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](http://doctoc.herokuapp.com/)*

- [Introduction](#introduction)
- [Rename User Accounts](#rename-user-accounts)
- [Change a User's Email Address Completely](#change-a-users-email-address-completely)
- [Delete and Recreate a User without Waiting 5 days](#delete-and-recreate-a-user-without-waiting-5-days)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

(TODO: Add table of contents.)

_**Comments have been turned off for these help pages, please post your questions and comments to the [Mailing List](http://groups.google.com/group/google-apps-manager)**_

# Introduction
GAM has a number of features that allow Google Apps Admins to do things that aren't normally possible with Google Apps.

# Rename User Accounts
Quite possibly GAM's most popular feature, it's easy to change a user's account name (and thus their email address) with GAM. Google recommends that you verify the user is completely logged out of the web interface (Gmail, Docs, Calendar, etc) before doing the rename. It can also take up to 10 minutes for the name change to propagate across all of Google's servers so you might want to tell the user to take a coffee break before logging back in. Finally, Google Talk will lose all of the user's accepted Chat friends so the user (or their friends) will need to re-accept invitations to chat.

[Update (and Rename) a User](ExamplesProvisioning#Update_(and_Rename)_a_User)

# Change a User's Email Address Completely
For over a year now, GAM has been the best way to rename a user's account name with Google Apps. But you could only change their account name, the part of their email address before the @ symbol. With GAM 1.0, you can now completely change a user's email address including the doman name after the @ symbol. The domain you wish to change the user's email address must be configured as a secondary (sometimes called separate) domain in your Google Apps account.

[Move a User Between Domains](ExamplesMultiDomain#Move_a_User_Between_Domains)

# Delete and Recreate a User without Waiting 5 days
Normally with Google Apps, after you delete a user account, you have to wait 5 days before creating another user account with the same name. During this time, Google must purge their servers of the user account. Unfortunately sometimes this process takes even longer than 5 days. With GAM, you can delete a user account and then recreate it immediately, no 5 day wait, not even a 5 minute wait! The way this works is that [GAM renames the user account](UniqueGAMFeatures#Rename_User_Accounts) before deleting it. Then GAM deletes the renamed account. Google's servers then work on purging the renamed account, not the original user account so you're free to create the user account again immediately. To make sure the renamed, deleted account doesn't block you from recreating a useful account name, the account rename format looks like: "username-YYYYMMDDhhmmss-random-string" where username is the original username, YYYYMMDDhhmmss is the timestamp (for example, 20100719074039 for July 19th 2010 at 7:49am) and random-string is a 25 character random string of letters and numbers (for example vpte8n79mxburka1wshocgd25).

[Delete a User](ExamplesProvisioning#Delete_a_User)