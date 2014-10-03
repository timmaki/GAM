(TODO: Add table of contents.)

_**Comments have been turned off for these help pages, please post your questions and comments to the [Mailing List](http://groups.google.com/group/google-apps-manager)**_

# Retrieving Domain Settings
## Syntax
```
gam info domain
```
Retrieves all domain settings for a Google Apps domain and displays them.

## Example
This example displays the domain settings for acme.com
```
gam info domain
Google Apps Domain:  acme.com
Default Language:  en
Organization Name:  Acme Inc.
Maximum Users:  500
Current Users:  436
Domain is Verified:  True
Support PIN:  12345
Domain Edition:  premier
Customer PIN:  123456789
Domain Creation Time:  20100924T095632.704-0700
Domain Country Code:  US
Admin Secondary Email:  acme.backup@gmail.com
CNAME Verification Record Name:  googleffffffffd0b4356f
CNAME Verification Verified:  true
CNAME Verification Method:  cname
MX Verification Verified:  true
MX Verification Method:  mx
SSO Enabled:  false
SSO Signon Page: None
SSO Logout Page:  None
SSO Password Page:  None
SSO Whitelist IPs:  None
SSO Use Domain Specific Issuer:  false
User Migration Enabled:  True
Outbound Gateway Smart Host:  None
Outbound Gateway SMTP Mode:  None
```

---


# Downloading the Domain Logo
## Syntax
```
gam info domain logo <logo file>
```
Download's the current Google Apps domain logo to the file logo file.

## Example
This example downloads the logo file to old-logo.png
```
gam info domain logo old-logo.png
```

---


# Changing the Domain Default Language
## Syntax
```
gam update domain language <language>
```
Changes the default language for the Google Apps domain. This will effect new users but will not change language settings for existing users.  A full list of language codes can be found [here](http://code.google.com/googleapps/domain/email_settings/developers_guide_protocol.html#GA_email_language_tags).

## Example
This example will change the domain default language to the King's English.
```
gam update domain language en-GB
```

---


# Update Organization Name
## Syntax
```
gam update domain name <nice name>
```
Changes the displayed name for the domain displayed when user's login and throughout other various Google Apps pages.

## Example
This example changes the nice display name for acme.com from "Acme Widgets Inc." to "Acme World Wide Widgets Inc."
```
gam update domain name "Acme World Wide Widgets Inc."
```

---


# Update Secondary Email Address of Administrator
## Syntax
```
gam update domain admin_secondary_email <email>
```
Changes the secondary / backup email address that will be used in cases of account recovery.This email address should not be in the Google Apps domain since it is a recovery address.

## Example
This example changes the recovery address to acme.backup@gmail.com.
```
gam update domain admin_secondary_email acme.backup@gmail.com
```

---


# Update the Domain Logo
## Syntax
```
gam update domain logo <logo file>
```
Changes the image displayed on the login pages and various other places in Google Apps. The logo file should be a .jpg, .png or .gif file of less than 20kb that is 143x59 pixels. For details on logo requirements see [here](http://www.google.com/support/a/bin/answer.py?hl=en&answer=36726).

## Example
This example uploads the new-logo.png file to become the new image used on the Google Apps login page.
```
gam update domain logo new-logo.png
```

# Force CNAME Verification Attempt
## Syntax
```
gam update domain cname_verify
```
Forces Google's servers to attempt a CNAME record verification. The CNAME record should already be created in the domain's DNS and some time allowed for propagation. The results of the verification attempt are returned by the command.

## Example
This example forces CNAME verification for the domain.
```
gam update domain cname_verify
Record Name: googleffffffffdcb3346g
Verification Method: cname
Verified: true
```

---


# Force MX Verification Attempt
## Syntax
```
gam update domain mx_verify
```
Forces Google's servers to attempt a MX record verification. The MX records should already be created in the domain's DNS and some time allowed for propogation. The results of the verification attempt are returned by the command.

## Example
This example forces MX verification for the domain.
```
gam update domain mx_verify
Verification Method: mx
Verified: true
```

---


# Modify Domain Single Sign-on (SSO) Settings
## Syntax
```
gam update domain sso_settings enabled true|false sign_on_uri <URI> sign_out_uri <URI> password_uri <URI> whitelist <IP list> use_domain_specific_issuer true|false
```
Updates the Google Apps SSO settings. enabled turns SSO on or off. sign\_on\_uri, sign\_out\_uri and password\_uri should be the full URI used for each of these SSO steps. whitelist is a list of IP addresses where SSO should be applied (other IP addresses will not use SSO). use\_domain\_specific\_issuer determines if a unique domain name is issued in the SAML request based on the Google Apps domain the user visited.

## Example
This example turns SSO on for the domain with the given URIs used for SSO.
```
gam update domain sso_settings enabled true sign_on_uri https://sso.acme.com sign_out_uri https://sso.acme.com/logout password_uri https://sso.acme.com/password use_domain_specific_issuer true
```

---


# Uploading the SSO Key
## Syntax
```
gam update domain sso_key <public key file>
```
Uploads the given public key file, replacing the existing key on Google's servers. It may be necessary to have SSO enabled before uploading the SSO key.

## Example
This example uploads the public-key.der file to Google's servers.
```
gam update domain sso_key public-key.der
```

---


# Enable/Disable User Mail Migrations
## Syntax
```
gam update domain user_migrations true|false
```
Determines whether or not users are allowed to upload mail using the Email Migration API. This API is used by user migration tools like [Google Apps Migration for Microsoft Outlook](http://tools.google.com/dlpage/outlookmigration).

## Example
This example turns user managed migrations on for the domain.
```
gam update domain user_migrations true
```

---


# Outbound Email Gateway Settings
## Syntax
```
gam update domain outbound_gateway <SMTP Server Domain or IP> mode smtp|smtp_tls
```
Configures all outbound Google Apps mail to go directly to the given SMTP Server domain name or IP address. If smtp is specified, plain text smtp is used in the transfer. If smtp\_tls is specified, encryption will be used on the outgoing connection.

**Warning:** Be sure you know what you're doing with this setting. If you enter an invalid IP/domain or the host is not configured to accept mail properly, you could break outgoing mail for your entire Google Apps organization.

## Example
This example turns outbound gateway on, directs it to a Postini server and forces the use of encryption (smtp\_tls) for connections.
```
gam update domain outbound_gateway outbounds10.psmtp.com mode smtp_tls
```

---


# Email Routing
## Syntax
```
gam update domain email_route destination <SMTP Server Domain or IP> rewrite_to true|false enabled true|false bounce_notifications true|false  account_handling all_accounts|provisioned_account|unknown_accounts
```
Creates a new email route for incoming mail. destination is a valid domain or IP address that will accept the mail. rewrite\_to determines if the domain name of the message is replaced with the destination domain. enabled determines if the routing rule is turned on or off. bounce\_notifications determines if delivery failures are sent for messages not received by the destination server. account\_handling determines which set of users mail will be routed for, all, existing/provisioned or unknown.

## Example
This example routes all unknown mail to acme's legacy Exchange server.
```
gam update domain email_route destination exchange.acme.com rewrite_to false enabled true bounce_notifications false account_handling unknown_accounts
```

---
