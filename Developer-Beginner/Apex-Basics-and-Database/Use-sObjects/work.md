# Salesforce -> Developer Beginner -> Apex Basics & Database -> Use sObjects

## Learning Objectives

- Describe the relationship between sObjects and Salesforce records.
- Create and use specific sObject variables.
- Cast a generic sObject to a specific sObject.

## Use sObjects

Because Apex is tightly integrated with the database, you can access Salesforce records and their fields directly from Apex. Every record in Salesforce is natively represented as an **`sObject`** in Apex. For example, the Acme account record corresponds to an Account sObject in Apex. The fields of the Acme record that you can view and modify in the user interface can be read and modified directly on the sObject as well.

The following table lists some populated fields of the Acme account example record. The Account sObject is an abstraction of the account record and holds the account field information in memory as an object.

### Table 1. Account sObject for a Retrieved Record

| **Account Field** | **Value** |
| ------------- | ----- |
| Id | 001D000000JlfXe |
| Name | Acme |
| Phone | (415)555-1212 |
| NumberOfEmployees | 100 |

Each Salesforce record is represented as an sObject before it is inserted into Salesforce. Likewise, when persisted records are retrieved from Salesforce, they’re stored in an sObject variable.

Standard and custom object records in Salesforce map to their sObject types in Apex. Here are some common sObject type names in Apex used for standard objects.

- Account
- Contact
- Lead
- Opportunity

If you’ve added custom objects in your organization, use the API names of the custom objects in Apex.

- For example, a custom object called Merchandise corresponds to the Merchandise__c sObject in Apex.

### **Create sObject Variables**

To create an sObject, you need to:

1. declare a variable
2. and assign an sObject instance to it.

    - The data type of the variable is the sObject type.

The following example creates an sObject of type Account with the name Acme and assigns it to the *`acct` variable*.

```js
1. Account acct = new Account(Name='Acme');
```

### **sObject and Field Names**

Apex references standard or custom sObjects and their fields using their unique API names.

API names of object and fields can differ from their labels. For example, the Employees field has a label of Employees and appears on the account record page as Employees but its API name is NumberOfEmployees. To access this field in Apex, you’ll need to use the API name for the field: NumberOfEmployees.

The following are highlights of some rules used for API names for custom objects and custom fields.

For custom *objects* and custom *fields*, the API name always ends with the `__c` suffix. For custom *relationship fields*, the API name ends with the `__r` suffix. For example:

- A custom object with a label of Merchandise has an API name of Merchandise__c.
- A custom field with a label of Description has an API name of Description__c.
- A custom relationship field with a label of Items has an API name of Items__r.

In addition, `spaces in labels are replaced with underscores` in API names. For example, a custom field name of Employee Seniority has an API name of Employee_Seniority__c.

### **Find Object and Field Names**

To find out the names of standard objects and their fields for use in Apex, refer to the [Object Reference for Salesforce and Lightning Platform](https://developer.salesforce.com/docs/atlas.en-us.224.0.object_reference.meta/object_reference/).

For custom objects, look up the object and field API names in your org.

1. From Setup, click the `Object Manager` tab to the right of the `Home` tab, and then click your object’s name.

### **Create sObjects and Adding Fields**

Before you can insert a Salesforce record, you must create it in memory first as an sObject. Like with any other object, sObjects are created with the `new` operator:

```js
1. Account acct = new Account();
```

The API object name becomes the data type of the sObject variable in Apex. In this example, `Account` is the data type of the `acct` variable.

The account referenced by the acct variable is empty because we haven’t populated any of its fields yet. There are two ways to add fields:

1. through the constructor
2. or by using dot notation

The fastest way to add fields is to specify them as name-value pairs inside the constructor. For example, this statement creates a new account sObject and populates its Name field with a string value.

```js
1. Account acct = new Account(Name='Acme');
```

***The Name field is the only required field for accounts***, which means that it has to be populated before being able to insert a new record. However, you can populate other fields as well for the new record. This example adds also a phone number and the number of employees.

```js
1. Account acct = new Account(Name='Acme', Phone='(415)555-1212', NumberOfEmployees=100);
```

Alternatively, you can use the dot notation to add fields to an sObject. The following is equivalent to the previous example, although it takes a few more lines of code.

```js
1. Account acct = new Account();
2. acct.Name = 'Acme';
3. acct.Phone = '(415)555-1212';
4. acct.NumberOfEmployees = 100;
```

## Work with the Generic sObject Data Type

Typically, you use the specific sObject data type, such as Account for a standard object or Book__c for a custom object called Book, when working with sObjects. However, when you don’t know the type of sObject your method is handling, you can use the generic sObject data type.

Variables that are declared with the generic sObject data type can reference any Salesforce record, whether it is a standard or custom object record.

![A generic sObject variable can point to any Salesforce record](/assets/generic-sObject-variable.png)

This example shows how any Salesforce object, such as an account or a custom object called Book__c, can be assigned to a generic sObject variable.

```js
1. sObject sobj1 = new Account(Name='Trailhead');
2. sObject sobj2 = new Book__c(Name='Workbook 1');
```

In contrast, variables that are declared with the specific sObject data type can reference only the Salesforce records of the same type.

![A specific sObject variable can point to the Salesforce record of the same type only](/assets/specific-sObject-variables.png)

### Cast Generic sObjects to Specific sObject Types

When you’re dealing with generic sObjects, you sometimes need to cast your sObject variable to a specific sObject type. One of the benefits of doing so is to be able to access fields using dot notation, which is not available on the generic sObject. Since sObject is a parent type for all specific sObject types, you can cast a generic sObject to a specific sObject. This example shows how to cast a generic sObject to Account.

```js
1. // Cast a generic sObject to an Account
2. Account acct = (Account)myGenericSObject;
3. // Now, you can use the dot notation to access fields on Account
4. String name = acct.Name;
5. String phone = acct.Phone;
```

## Tell Me More

The fields of a generic sObject can be accessed only through the `put()` and `get()` methods.

In this unit, you’ve learned what sObjects are and how to use them. However, creating an sObject doesn’t persist it as a record in the database.

- To save the sObject as a record, and do other things with it, use the **`Data Manipulation Language`** (**`DML`**).
- To retrieve a record, use the **`Salesforce Object Query Language`** (**`SOQL`**).

Check out later units to learn about `DML` and `SOQL`.

## Resources

- [Object Reference for Salesforce and Lightning Platform](https://developer.salesforce.com/docs/atlas.en-us.224.0.object_reference.meta/object_reference/)
- Apex Developer Guide: [Working with sObjects](https://developer.salesforce.com/docs/atlas.en-us.224.0.apexcode.meta/apexcode/langCon_apex_SObjects.htm)
- Apex Developer Guide: [SObject Methods](https://developer.salesforce.com/docs/atlas.en-us.224.0.apexcode.meta/apexcode/apex_methods_system_sobject.htm#apex_System_SObject_methods)
