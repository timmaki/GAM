- [License Types]
- [Adding a License for Users](#adding-a-license-for-users)
- [Updating a License for Users](#updating-a-license-for-users)
- [Deleting a License for Users](#deleting-a-license-for-users)

# License Types
GAM supports the licenses listed in the "Product SKU ID" column of [Google's Documentation](https://developers.google.com/admin-sdk/licensing/v1/how-tos/products). Additionally, GAM supports abbreviations for some of the SKU names:

abbreviation  -->  SKU
gafw  -->  Google-Apps-For-Business
gau   -->  Google-Apps-Unlimited
gams  -->  Google-Apps-For-Postini
vault -->  Google-Vault
vfe   -->  Google-Vault-Former-Employee

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
gam user <username>|group <groupname>|ou <ouname>|all users update license <sku> from <oldsku>
```
Update the license for the given users. The SKU can be one of coordinate, drive20gb, drive50gb, drive200gb, drive400gb, drive1tb, drive2tb, drive4tb, drive8tb or drive16tb.

## Example
This example updates the user who previously had 50gb of extra Drive storage licensed to 200gb of Drive space.
```
gam user heavydriveuser@acme.org update license drive200gb from drive50gb
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
