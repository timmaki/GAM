- [OAuth Key Management](#oauth-key-management)
  - [Selecting Which OAuth Key File to Use](#selecting-which-oauth-key-file-to-use)
  - [Display Info About the Current OAuth Token](#display-info-about-the-current-oauth-token)
  - [Revoking an OAuth Token](#revoking-an-oauth-token)

# OAuth Key Management
## Selecting Which OAuth Key File to Use
### Syntax
```
Windows DOS Shell:
set OAUTHFILE=oauth.txt-mydomain.com

Windows PowerShell:
$env:OAUTHFILE="oauth.txt-mydomain.com"

Linux / OSX:
export OAUTHFILE=oauth.txt-mydomain.com
```
By default, GAM saves OAuth credentials to a file named oauth.txt. This works fine if you only have one Google Apps instance to admin but if you have multiple, juggling this file can get complicated. If the environment variable OAUTHFILE is set, GAM will use that filename instead of oauth.txt for creating and reading OAuth authentication. Note that the file name can be whatever you prefer and is stored in the same location as gam.exe or gam.py.

### Example
This DOS shell example switches between OAuth files for multi GAM runs.
```
set OAUTHFILE=oauth.txt-mydomain.com
gam info domain

Google Apps Domain:  mydomain.com
Default Language: en
Organization Name: My Domain
Maximum Users: 15
...

set OAUTHFILE=oauth.txt-mypalsdomain.com
gam info domain

Google Apps Domain:  mypalsdomain.com
Default Language: en
Organization Name: My Pal's Domain
Maximum Users: 5
...
```

## Display Info About the Current OAuth Token
### Syntax
```
gam oauth info
```
Displays information about the current OAuth token. Note that if the token was created with a version of GAM older than 2.5, it won't be possible to read what admin created the token, you'll need to revoke and recreate the token with 2.5 to see this information.

### Example
This example displays information about the current token
```
gam oauth info

OAuth File: /home/jay/bin/gam/oauth.txt-mydomain.com
Google Apps Domain: mydomain.com
Client ID: 01010101010.apps.googleusercontent.com
Secret: XYZXXYZZZZZZZ
Scopes:
  https://apps-apis.google.com/a/feeds/groups/
  https://apps-apis.google.com/a/feeds/alias/
  https://apps-apis.google.com/a/feeds/policies/
  https://apps-apis.google.com/a/feeds/user/
  https://apps-apis.google.com/a/feeds/emailsettings/2.0/
  https://apps-apis.google.com/a/feeds/calendar/resource/
  https://apps-apis.google.com/a/feeds/compliance/audit/
  https://apps-apis.google.com/a/feeds/domain/
  https://www.googleapis.com/auth/apps/reporting/audit.readonly
  https://www.googleapis.com/auth/apps.groups.settings
  https://www.google.com/m8/feeds
  https://www.google.com/calendar/feeds/
  https://www.google.com/hosted/services/v1.0/reports/ReportingData
Google Apps Admin: jay@mydomain.com
```

## Revoking an OAuth Token
### Syntax
```
gam oauth revoke
```
Revokes the current OAuth token (de-authorizing it from Google's end) and deletes the current OAuth file. **There is no undo from this operation!** Once revoked, you'll need to re-authorize using a Google Apps admin account. Note that you can also revoke OAuth tokens from the [Google Accounts page](https://accounts.google.com/b/0/IssuedAuthSubTokens) of the admin who created the token. Tokens can also be revoked in the Google Apps Control Panel by opening the security tab of the authorizing user.

### Example
This example revokes (destroys) and deletes current OAuth token
```
gam oauth revoke

This OAuth token will self-destruct in 3...2...1...boom!
```