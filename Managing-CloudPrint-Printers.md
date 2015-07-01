- [Managing CloudPrint Printers](#managing-cloudprint-printers)
  - [Updating A Printer](#updating-a-printer)
  - [Getting Printer Info](#getting-printer-info)
  - [Deleting A Printer](#deleting-a-printer)
  - [Reporting Printers](#reporting-printers)
- [Sharing CloudPrint Printers](#sharing-cloudprint-printers)
  - [Sharing A Printer](#sharing-a-printer)
  - [Unsharing A Printer](#unsharing-a-printer)
  - [Showing Printer ACLs](#showing-printer-acls)
- [Managing CloudPrint Print Jobs](#managing-cloudprint-print-jobs)
  - [Submitting A Print Job](#submitting-a-print-job)
  - [Cancelling A Print Job](#cancelling-a-print-job)
  - [Deleting A Print Job](#deleting-a-print-job)
  - [Reporting Print Jobs](#reporting-print-jobs)

# Managing CloudPrint Printers
## Updating A Printer
### Syntax
```
gam update printer <id> [quotaEnabled <true|false>] [dailyQuota <number>] [public <true|false> [name <name>] [proxy <proxy>] [description <description>]
```
Updates the given printer. The optional parameter quotaEnabled enables or disables a daily quota for users using the printer. The optional parameter dailyQuota sets the number of pages users can print a day when quotaEnabled is true. The optional parameter public sets the printer to be accessible to anyone who knows the printer's URL when true. The optional parameters name and description adjust the name and description of the printer. The optional parameter proxy adjusts the proxy id for the printer (dangerous).

### Example
This example makes the printer public and sets a 5 pages a day quota.
```
gam update printer 86bee4bb-c43e-8fd4-f06e-e7b8564a1c53 public true quotaEnabled true dailyQuota 5
```
----

## Getting Printer Info
### Syntax
```
gam info printer <id> [everything]
```
Gets detailed information about the given CloudPrint printer. The optional everything argument includes even more printer detail.

### Example
This example prints details about the given printer.
```
gam info printer  __google__docs
status: 
isTosAccepted: False
updateTime: 2013-06-03 15:22:04
displayName: Save to Google Drive
description: Save your document as a PDF in Google Drive
name: Save to Google Docs
tags: save docs pdf google __google__drive_enabled
defaultDisplayName: Save to Google Drive
accessTime: 2011-09-15 20:14:01
id: __google__docs
ownerName: Cloud Print
capsHash: 
ownerId: cloudprinting@gmail.com
type: DRIVE
createTime: 2011-07-22 17:00:03
proxy: google-wide
```
----

## Deleting A Printer
### Syntax
```
gam delete printer <id>
```
Deletes the given printer. Be aware that depending on your printer / print proxy, the printer may be recreated soon after it's deleted. You should make sure your printer or print proxy is no longer registering the printer either.

### Example
This example deletes the printer that has ID 86bee4bb-c43e-8fd4-f06e-e7b8564a1c53
```
gam delete printer 86bee4bb-c43e-8fd4-f06e-e7b8564a1c53
```
----

## Reporting Printers
### Syntax
```
gam print printers [query <query>] [type <type>] [status <status>] [extrafields <connectionStatus|semanticState|uiState|queuedJobsCount>] [todrive]
```
CSV output of printers owned or accessible by the user GAM is running as. The optional parameter query limits results to printers that have a title or tag matching the search value. The optional parameter type limits results to printers of the given type. The optional parameter status limits results to printers with the given status. The optional parameter extrafields includes the given extra CSV fields in the result but may significantly slow the performance of the print command. The optional parameter todrive creates a Google Drive Spreadsheet of the results rather than outputting CSV to the console.

### Examples
This example prints all printers accessible by the user.
```
gam print printers
```
this example prints all printers with a name or tag like "HP".
```
gam print printers query HP
```
----

