- [Creating a Custom User Schema](#creating-a-custom-user-schema)
- [Updating a Custom User Schema](#updating-a-custom-user-schema)
- [Deleting a Custom User Schema](#deleting-a-custom-user-schema)

# Adding a Custom User Schema
## Syntax
```
gam create schema <schemaname>
 field <fieldname> type <bool|double|email|int64|phone|string>
 [indexed] [restricted] [multivalued]
 [minvalue <number>]
 [maxvalue <number>]
 endfield
```
Create a new custom user schema. schemaname is the name of the schema to create. You can have up to 100 schemas in your Google Apps instance and each schema can have up to 100 fields defined. fieldname is the name of the field. type is required and specifies the type of the field. bool, double, email, int64, phone and string are the allowed types. The optional parameter indexed specifies that searching will be performed on this field. The optional parameter restricted specifies that only super administrators and the user themself can read the field value(s), other users will not have access. The optional parameter multivalued specifies that the field can contain multiple values per-user. The endfield parameter is necessary to end the given field.

## Example
This example creates a StudentData schema with the fields id, grade and labels. The id field will be hidden from regular users (restricted) and indexed. The labels field will be multivalue. This example also shows how you would set this schema for an existing user.
```
gam create schema StudentData
 field id type string indexed restricted endfield
 field grade type int64 endfield
 field labels type string multivalued endfield

gam update user tommy.jones
 StudentData.id 839342028
 StudentData.grade 1
 StudentData.labels multivalued TRANSFER_STUDENT
 StudentData.labels multivalued HONOR_ROLL 
```

# Updating a Custom User Schema
## Syntax
```
gam update schema <schemaname>
 field <fieldname> type <bool|double|email|int64|phone|string>
  [indexed] [restricted] [multivalued]
  [minvalue <number>]
  [maxvalue <number>]
  endfield
```
Update a custom user schema. Note that many schema update operations aren't possible in order to preserve existing user data. As a rule of thumb, schemas should be well thought out when first created as after-the-fact changes can prove challenging. schemaname is the name of the schema to create. You can have up to 100 schemas in your Google Apps instance and each schema can have up to 100 fields defined. fieldname is the name of the field. type is required and specifies the type of the field. bool, double, email, int64, phone and string are the allowed types. The optional parameter indexed specifies that searching will be performed on this field. The optional parameter restricted specifies that only super administrators and the user themself can read the field value(s), other users will not have access. The optional parameter multivalued specifies that the field can contain multiple values per-user. The endfield parameter is necessary to end the given field.

---