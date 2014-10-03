<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](http://doctoc.herokuapp.com/)*

- [Adding a License for Users](#adding-a-license-for-users)
  - [Syntax](#syntax)
  - [Example](#example)
  - [](#)
- [Updating a License for Users](#updating-a-license-for-users)
  - [Syntax](#syntax-1)
  - [Example](#example-1)
  - [](#-1)
- [Deleting a License for Users](#deleting-a-license-for-users)
  - [Syntax](#syntax-2)
  - [Example](#example-2)
  - [](#-2)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

(TODO: Add table of contents.)

_**Comments have been turned off for these help pages, please post your questions and comments to the [Mailing List](http://groups.google.com/group/google-apps-manager)**_

# Adding a License for Users
## Syntax
```
gam user <username>|group <groupname>|ou <ouname>|all users add license <sku>
```
Assign a license for the given SKU to a user or number of users. The SKU can be one of coordinate, drive20gb, drive50gb, drive200gb, drive400gb, drive1tb, drive2tb, drive4tb, drive8tb or drive16tb.

## Example
This example gives members of the sales team an extra 50gb of Drive space
```
gam group sales add license drive50gb
```

This example gives users in the "Google Coordinate" OU a license for Google Coordinate
```
gam ou "Google Coordinate" add license coordinate
```

---


# Updating a License for Users
## Syntax
```
gam user <username>|group <groupname>|ou <ouname>|all users update license <sku>
```
Update the license for the given users. The SKU can be one of coordinate, drive20gb, drive50gb, drive200gb, drive400gb, drive1tb, drive2tb, drive4tb, drive8tb or drive16tb.

## Example
This example updates the user who previously had 50gb of extra Drive storage licensed to 200gb of Drive space.
```
gam user heavydriveuser@acme.org update license drive200gb
```

---


# Deleting a License for Users
## Syntax
```
gam user <username>|group <groupname>|ou <ouname>|all users delete license <sku>
```
Deletes the given SKU license for the users.

## Example
This example will remove the Coordinate license for all users.
```
gam all users delete license coordinate
```

---
