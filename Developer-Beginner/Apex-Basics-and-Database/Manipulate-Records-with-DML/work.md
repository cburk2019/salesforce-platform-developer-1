# Salesforce -> Developer Beginner -> Apex Basics & Database -> Manipulate Records with DML

## Learning Objectives

- Use DML to insert, update, and delete records.
- Perform DML statements in bulk.
- Use upsert to either insert or update a record.
- Catch a DML Exception.
- Use a Database method to insert new records with the partial success option and process the results.
- Know when to use DML statements and when to use Database methods.
- Perform DML operations on related records.

## **Manipulate Records with DML**

Create and modify records in Salesforce by using the Data Manipulation Language, abbreviated as DML. DML provides a straightforward way to manage records by providing simple statements to insert, update, merge, delete, and restore records.

Because Apex is a data-focused language and is saved on the Lightning Platform, it has direct access to your data in Salesforce. Unlike other programming languages that require additional setup to connect to data sources, with Apex DML, managing records is made easy! By calling DML statements, you can quickly perform operations on your Salesforce records.This example adds the Acme account to Salesforce. An account sObject is created first and then passed as an argument to the insert statement, which persists the record in Salesforce.

```js
1. // Create the account sObject
2. Account acct = new Account(Name='Acme', Phone='(415)555-1212', NumberOfEmployees=100);
3. // Insert the account by using DML
4. insert acct;
```

### **DML Statements**

The following DML statements are available.

- `insert`
- `update`
- `upsert`
- `delete`
- `undelete`
- `merge`

Each DML statement accepts either a single sObject or a list (or array) of sObjects. Operating on a list of sObjects is a more efficient way for processing records.

All those statements, except a couple, are familiar database operations. The `upsert` and `merge` statements are particular to Salesforce and can be quite handy.

The `upsert` DML operation creates new records and updates sObject records within a single statement, using a specified field to determine the presence of existing objects, or the ID field if no field is specified.

The `merge` statement merges up to three records of the same sObject type into one of the records, deleting the others, and re-parenting any related records.

### **ID Field Auto-Assigned to New Records**

When inserting records, the system assigns an ID for each record. In addition to persisting the ID value in the database, the ID value is also auto-populated on the sObject variable that you used as an argument in the DML call.

This example shows how to get the ID on the sObject that corresponds to the inserted account.

```js
1. // Create the account sObject 
2. Account acct = new Account(Name='Acme', Phone='(415)555-1212', NumberOfEmployees=100);
3. // Insert the account by using DML
4. insert acct;
5. // Get the new ID on the inserted sObject argument
6. ID acctID = acct.Id;
7. // Display this ID in the debug log
8. System.debug('ID = ' + acctID);
9. // Debug log result (the ID will be different in your case)
10. // DEBUG|ID = 001D000000JmKkeIAF
```

### **Note**

#### **Beyond the Basics**

Because the sObject variable in the example contains the ID after the DML call, you can reuse this sObject variable to perform further DML operations, such as updates, as the system will be able to map the sObject variable to its corresponding record by matching the ID.

You can retrieve a record from the database to obtain its fields, including the ID field, but this can’t be done with DML. You’ll need to write a query by using SOQL. You’ll learn about SOQL in another unit.

### **Bulk DML**

You can perform DML operations either on a single sObject, or in bulk on a list of sObjects. Performing bulk DML operations is the recommended way because it helps avoid hitting governor limits, such as the DML limit of 150 statements per Apex transaction. This limit is in place to ensure fair access to shared resources in the Lightning Platform. Performing a DML operation on a list of sObjects counts as one DML statement, not as one statement for each sObject.

This example inserts contacts in bulk by inserting a list of contacts in one call. The sample then updates those contacts in bulk too.

1. Execute this snippet in the Developer Console using Anonymous Apex.

    ```js
    1. // Create a list of contacts
    2. List<Contact> conList = new List<Contact> {
    3.     new Contact(FirstName='Joe',LastName='Smith',Department='Finance'),
    4.         new Contact(FirstName='Kathy',LastName='Smith',Department='Technology'),
    5.         new Contact(FirstName='Caroline',LastName='Roth',Department='Finance'),
    6.         new Contact(FirstName='Kim',LastName='Shain',Department='Education')};
    7. // Bulk insert all contacts with one DML call
    8. insert conList;
    9. // List to hold the new contacts to update
    10. List<Contact> listToUpdate = new List<Contact>();
    11. // Iterate through the list and add a title only
    12. //   if the department is Finance
    13. for(Contact con : conList) {
    14.     if (con.Department == 'Finance') {
    15.         con.Title = 'Financial analyst';
    16.         // Add updated contact sObject to the list.
    17.         listToUpdate.add(con);
    18.     }
    19. }
    20. // Bulk update all contacts with one DML call
    21. update listToUpdate;
    ```

2. Inspect the contacts recently created in your org.

    Two of the contacts who are in the Finance department should have their titles populated with `Financial analyst`.

### **Upsert Records**

If you have a list containing a mix of new and existing records, you can process insertions and updates to all records in the list by using the `upsert` statement. Upsert helps avoid the creation of duplicate records and can save you time as you don’t have to determine which records exist first.

The `upsert` statement matches the sObjects with existing records by comparing values of one field. If you don’t specify a field when calling this statement, the `upsert` statement uses the sObject’s ID to match the sObject with existing records in Salesforce. Alternatively, you can specify a field to use for matching. For custom objects, specify a custom field marked as external ID. For standard objects, you can specify any field that has the idLookup property set to true. For example, the Email field of Contact or User has the idLookup property set. To check a field’s property, see the [Object Reference for Salesforce and Lightning Platform](https://developer.salesforce.com/docs/atlas.en-us.224.0.object_reference.meta/object_reference/).

### **Upsert Syntax**

`upsert sObject | sObject[]`

`upsert sObject | sObject[] field`

The optional field is a field token. For example, to specify the MyExternalID field, the statement is:

```js
1. upsert sObjectList Account.Fields.MyExternalId;
```

Upsert uses the sObject record's primary key (the ID), an idLookup field, or an external ID field to determine whether it should create a new record or update an existing one:

- If the key is not matched, a new object record is created.
- If the key is matched once, the existing object record is updated.
- If the key is matched multiple times, an error is generated and the object record is neither inserted or updated.

This example shows how upsert updates an existing contact record and inserts a new contact in one call. This upsert call updates the existing Josh contact and inserts a new contact, Kathy.

### **Note**

The upsert call uses the ID to match the first contact. The `josh` variable is being reused for the upsert call. This variable has already been populated with the record ID from the previous insert call, so the ID doesn’t need to be set explicitly in this example.

1. Execute this snippet in the Execute Anonymous window of the Developer Console.

    ```js
    1. // Insert the Josh contact
    2. Contact josh = new Contact(FirstName='Josh',LastName='Kaplan',Department='Finance');       
    3. insert josh;
    4. // Josh's record has been inserted
    5. //   so the variable josh has now an ID
    6. //   which will be used to match the records by upsert
    7. josh.Description = 'Josh\'s record has been updated by the upsert operation.';
    8. // Create the Kathy contact, but don't persist it in the database
    9. Contact kathy = new Contact(FirstName='Kathy',LastName='Brown',Department='Technology');
    10. // List to hold the new contacts to upsert
    11. List<Contact> contacts = new List<Contact> { josh, kathy };
    12. // Call upsert
    13. upsert contacts;
    14. // Result: Josh is updated and Kathy is created.
    ```

2. Inspect all contacts in your org.

    Your org will have only one Josh Kaplan record, not two, because the upsert operation found the existing record and updated it instead of creating a new contact record. One Kathy Brown contact record will be there too.

Alternatively, you can specify a field to be used for matching records. This example uses the Email field on Contact because it has idLookup property set. The example inserts the Jane Smith contact, and creates a second Contact sObject, populates it with the same email, then calls `upsert` to update the contact by using the email field for matching.

### **Note**

If `insert` was used in this example instead of `upsert`, a duplicate Jane Smith contact would have been inserted.

1. Execute this snippet in the Execute Anonymous window of the Developer Console.

    ```js
    1. Contact jane = new Contact(FirstName='Jane',
    2.                          LastName='Smith',
    3.                          Email='jane.smith@example.com',
    4.                          Description='Contact of the day');
    5. insert jane;
    6. // 1. Upsert using an idLookup field
    7. // Create a second sObject variable.
    8. // This variable doesn’t have any ID set.
    9. Contact jane2 = new Contact(FirstName='Jane',
    10.                          LastName='Smith',  
    11.                          Email='jane.smith@example.com',
    12.                          Description='Prefers to be contacted by email.');
    13. // Upsert the contact by using the idLookup field for matching.
    14. upsert jane2 Contact.fields.Email;
    15. // Verify that the contact has been updated
    16. System.assertEquals('Prefers to be contacted by email.',
    17.                    [SELECT Description FROM Contact WHERE Id=:jane.Id].Description);
    ```

2. Inspect all contacts in your org.

    Your org will have only one Jane Smith contact with the updated description.

### **Delete Records**

You can delete persisted records using the `delete` statement. Deleted records aren’t deleted permanently from Lightning Platform, but they’re placed in the Recycle Bin for 15 days from where they can be restored.

This example shows how to delete all contacts whose last name is Smith. If you’ve run the sample for bulk DML, your org should already have two contacts with the last name of Smith. Execute this snippet in the Developer Console using Anonymous Apex, and then verify that there are no contacts with the last name Smith anymore.

```js
1. Contact[] contactsDel = [SELECT Id FROM Contact WHERE LastName='Smith']; 
2. delete contactsDel;
```

### **Note**

This snippet includes a query to retrieve the contacts (a SOQL query). You’ll learn more about SOQL in another unit.

### **DML Statement Exceptions**

If a DML operation fails, it returns an exception of type `DmlException`. You can catch exceptions in your code to handle error conditions.

This example produces a `DmlException` because it attempts to insert an account without the required Name field. The exception is caught in the catch block.

```js
1. try {
2.     // This causes an exception because 
3.     //   the required Name field is not provided.
4.     Account acct = new Account();
5.     // Insert the account 
6.     insert acct;
7. } catch (DmlException e) {
8.     System.debug('A DML exception has occurred: ' +
9.                 e.getMessage());
10. }
```

## Database Methods

Apex contains the built-in Database class, which provides methods that perform DML operations and mirror the DML statement counterparts.
These Database methods are static and are called on the class name.

- `Database.insert()`
- `Database.update()`
- `Database.upsert()`
- `Database.delete()`
- `Database.undelete()`
- `Database.merge()`

Unlike DML statements, Database methods have an optional allOrNone parameter that allows you to specify whether the operation should partially succeed. When this parameter is set to `false`, if errors occur on a partial set of records, the successful records will be committed and errors will be returned for the failed records. Also, no exceptions are thrown with the partial success option.

This is how you call the `insert` method with the allOrNone set to `false`.

```js
1. Database.insert(recordList, false);
```

The Database methods return result objects containing success or failure information for each record. For example, insert and update operations each return an array of `Database.SaveResult` objects.

```js
1. Database.SaveResult[] results = Database.insert(recordList, false);
```

### **Note**

Upsert returns `Database.UpsertResult` objects, and delete returns `Database.DeleteResult` objects.

By default, the allOrNone parameter is `true`, which means that the Database method behaves like its DML statement counterpart and will throw an exception if a failure is encountered.

The following two statements are equivalent to the `insert recordList`; statement.

```js
1. Database.insert(recordList);
```

And:

```js
1. Database.insert(recordList, true);
```

### **Note**

#### **Beyond the Basics**

In addition to these methods, the Database class contains methods that aren’t provided as DML statements. For example, methods used for transaction control and rollback, for emptying the Recycle Bin, and methods related to SOQL queries. You’ll learn about SOQL in another unit.

### **Example: Insert Records with Partial Success**

Let’s take a look at an example that uses the Database methods. This example is based on the bulk DML example, but replaces the DML statement with a Database method. The `Database.insert()` method is called with the partial success option. One contact in the list doesn’t have any fields on purpose and will cause an error because the contact can’t be saved without the required LastName field. Three contacts are committed and the contact without any fields generates an error. The last part of this example iterates through the returned results and writes debug messages to the debug log.

1. Execute this example in the Execute Anonymous window of the Developer Console.

    ```js
    1. // Create a list of contacts
    2. List<Contact> conList = new List<Contact> {
    3.         new Contact(FirstName='Joe',LastName='Smith',Department='Finance'),
    4.         new Contact(FirstName='Kathy',LastName='Smith',Department='Technology'),
    5.         new Contact(FirstName='Caroline',LastName='Roth',Department='Finance'),
    6.         new Contact()};
    7. // Bulk insert all contacts with one DML call
    8. Database.SaveResult[] srList = Database.insert(conList, false);
    9. // Iterate through each returned result
    10. for (Database.SaveResult sr : srList) {
    11.     if (sr.isSuccess()) {
    12.         // Operation was successful, so get the ID of the record that was processed
    13.         System.debug('Successfully inserted contact. Contact ID: ' + sr.getId());
    14.     } else {
    15.         // Operation failed, so get all errors
    16.         for(Database.Error err : sr.getErrors()) {
    17.             System.debug('The following error has occurred.');
    18.             System.debug(err.getStatusCode() + ': ' + err.getMessage());
    19.             System.debug('Contact fields that affected this error: ' + err.getFields());
    20.   }
    21.     }
    22. }
    ```

2. Verify the debug messages (use the DEBUG keyword for the filter).

    One failure should be reported and three contacts should have been inserted.

### **Should You Use DML Statements or Database Methods?**

- Use DML statements if you want any error that occurs during bulk DML processing to be thrown as an Apex exception that immediately interrupts control flow (by using try. . .catch blocks). This behavior is similar to the way exceptions are handled in most database procedural languages.
- Use Database class methods if you want to allow partial success of a bulk DML operation—if a record fails, the remainder of the DML operation can still succeed. Your application can then inspect the rejected records and possibly retry the operation. When using this form, you can write code that never throws DML exception errors. Instead, your code can use the appropriate results array to judge success or failure. Note that Database methods also include a syntax that supports thrown exceptions, similar to DML statements.

## **Work with Related Records**

Create and manage records that are related to each other through relationships.

### **Insert Related Records**

You can insert records related to existing records if a relationship has already been defined between the two objects, such as a lookup or master-detail relationship. A record is associated with a related record through a foreign key ID. For example, if inserting a new contact, you can specify the contact's related account record by setting the value of the `AccountId` field.

This example shows how to add a contact to an account (the related record) by setting the `AccountId` field on the contact. Contact and Account are linked through a lookup relationship.

1. Execute this snippet in the Anonymous Apex window of the Developer Console.

    ```js
    1. Account acct = new Account(Name='SFDC Account');
    2. insert acct;
    3. // Once the account is inserted, the sObject will be 
    4. // populated with an ID.
    5. // Get this ID.
    6. ID acctID = acct.ID;
    7. // Add a contact to this account.
    8. Contact mario = new Contact(
    9.     FirstName='Mario',
    10.     LastName='Ruiz',
    11.     Phone='415.555.1212',
    12.     AccountId=acctID);
    13. insert mario;
    ```

2. Inspect the contacts in your org.

    A new account (SFDC Account) has been created and has the Mario Ruiz contact in the account’s Contacts related list.

### **Update Related Records**

Fields on related records can't be updated with the same call to the DML operation and require a separate DML call. For example, if inserting a new contact, you can specify the contact's related account record by setting the value of the `AccountId` field. However, you can't change the account's name without updating the account itself with a separate DML call. Similarly, when updating a contact, if you also want to update the contact’s related account, you must make two DML calls. The following example updates a contact and its related account using two `update` statements.

    ```js
    1. // Query for the contact, which has been associated with an account.
    2. Contact queriedContact = [SELECT Account.Name 
    3.                           FROM Contact 
    4.                           WHERE FirstName = 'Mario' AND LastName='Ruiz'
    5.                           LIMIT 1];
    6. // Update the contact's phone number
    7. queriedContact.Phone = '(415)555-1213';
    8. // Update the related account industry
    9. queriedContact.Account.Industry = 'Technology';
    10. // Make two separate calls 
    11. // 1. This call is to update the contact's phone.
    12. update queriedContact;
    13. // 2. This call is to update the related account's Industry field.
    14. update queriedContact.Account;
    ```

### **Delete Related Records**

The `delete` operation supports cascading deletions. If you delete a parent object, you delete its children automatically, as long as each child record can be deleted.

For example, deleting the account you created earlier (SFDC Account) will delete its related contact too.

1. Execute this snippet in the Anonymous Apex window of the Developer Console.

    ```js
    1. Account[] queriedAccounts = [SELECT Id FROM Account WHERE Name='SFDC Account'];
    2. delete queriedAccounts;
    ```

2. Check the accounts and contacts in your org.

    You’ll see that both the account and its related contact were deleted.

### **About Transactions**

DML operations execute within a transaction. All DML operations in a transaction either complete successfully, or if an error occurs in one operation, the entire transaction is rolled back and no data is committed to the database. The boundary of a transaction can be a trigger, a class method, an anonymous block of code, an Apex page, or a custom Web service method. For example, if a trigger or class creates two accounts and updates one contact, and the contact update fails because of a validation rule failure, the entire transaction rolls back and none of the accounts are persisted in Salesforce.

## Resources

- [Apex Developer Guide](https://developer.salesforce.com/docs/atlas.en-us.224.0.apexcode.meta/apexcode)
- Apex Developer Guide: [Working with Data in Apex](https://developer.salesforce.com/docs/atlas.en-us.224.0.apexcode.meta/apexcode/apex_data_intro.htm)
- Apex Developer Guide: [Adding and Retrieving Data With DML](https://developer.salesforce.com/docs/atlas.en-us.224.0.apexcode.meta/apexcode/apex_dml_section.htm)
- Apex Developer Guide: [Database Class](https://developer.salesforce.com/docs/atlas.en-us.224.0.apexcode.meta/apexcode/apex_methods_system_database.htm)

## Hands-On Challenge

![the challenge - Create a method for inserting accounts.](/assets/manipulate-records-with-DML-challenge.png)

### Solution

![the solution](/assets/manipulate-records-with-DML-challenge-solution.png)
