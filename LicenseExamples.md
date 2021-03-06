- [License Types](#license-types)
- [Adding a License for Users](#adding-a-license-for-users)
- [Updating a License for Users](#updating-a-license-for-users)
- [Deleting a License for Users](#deleting-a-license-for-users)

# License Types
GAM supports the licenses listed in the "Product SKU ID" column of [Google's Documentation](https://developers.google.com/admin-sdk/licensing/v1/how-tos/products). Additionally, GAM supports abbreviations for some of the SKU names:

| license                  | abbreviation  |
|--------------------------|---------------|
| Google-Apps-For-Business |  gafw or apps |
| Google-Apps-Unlimited    | gau           |
| Google-Apps-For-Postini  | gams          |
| Google-Vault             | vault         |
| Google-Vault-Former-Employee | vfe       |

# Adding a License for Users
## Syntax
```
gam user <username>|group <groupname>|ou <ouname>|all users add license <sku>
```
Assign a license for the given SKU to a user or number of users.
## Example
This example gives members of the sales team a Vault license
```
gam group sales add license vault
```

This example gives users in the "Google Coordinate" OU a license for Google Coordinate
```
gam ou "Google Coordinate" add license Google-Coordinate
```

---


# Updating a License for Users
## Syntax
```
gam user <username>|group <groupname>|ou <ouname>|all users update license <sku> from <oldsku>
```
Update the license for the given users.

## Example
This example switches a user from Google Apps Message Security to Google Apps for Work licensing.
```
gam user heavydriveuser@acme.org update license gafw from gams
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
