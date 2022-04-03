# Understand Custom & Standard Objects

## Learning Objectives

- Describe the perks of using objects on the Salesforce platform.
- Explain the difference between standard objects and custom objects.
- List the types of custom fields an object can have.

## Overview of Objects

- data model - A data model is more or less wat it sounds like. It's a way tp model what database tables look like in a way that makes sense to humans.

### What a Database Spreadsheet looks like, which is not ideal

![database spreadsheet example](/Developer-Beginner/Data-Modeling/Understand-Custom-and-Standard-Objects/assets/database-spreadsheet.png)

In Salesforce:

- database tables are `objects`
- columns are `fields`
- rows are `records`

So, instead of an account spreadsheet, we have an Account object with fields and bunch of identically structured records.

When data model is discussed, a collection of objects and fields in an app is what we're talking about. See below.

![database tables as an object](/Developer-Beginner/Data-Modeling/Understand-Custom-and-Standard-Objects/assets/database-table-as-an-object.png)

## Get to Know Objects

Salesforce supports different types of objects.

- standard objects
- custom objects
- external objects
- platform events
- BigObjects

### Focus on Two Most Common Types of Objects

- `Standard objects` - objects that are included with Salesforce. Common business objects like Account, Contact, Lead, and Opportunity are all standard objects
- `Custom objects` - objects that you create to store information that is specific to your company or industry. DreamHouse example is a Property object that stores information about the homes his company is selling.

Objects are essentially containers that store your information. They give special functionality. For example, when a custom object is created, the platform automatically builds things like the page layout for the UI (user interface).

## Create a Custom Object

This is an example of how to create a custom object. Literally takes 1 minute.

1. Scroll to the bottom of this page and create a trailhead playground. Don’t skip this step! You need to use a fresh and clean Trailhead Playground for this module.
2. Once your playground is created (it takes a minute!), press Launch.
3. Click the gear icon The setup gear. at the top of the page and launch setup.
4. Click the Object Manager tab.
5. Click Create | Custom Object in the top-right corner.
6. For Label, enter Property. Notice that the Object Name and Record Name fields auto-fill.
7. For Plural Label, enter Properties.
8. Prior to saving the custom object, scroll to the bottom of the page and select the checkbox Launch New Custom Tab Wizard after saving this custom object.
9. Leave the rest of the values as default and click Save.
10. On the New Custom Object Tab page, click the Tab Style field and select a style you like. The style sets the icon to display in the UI for the object.
11. Click Next, Next, and Save.

## Get to Know Fields

Every standard and custom object has fields associated with it. Below are the different types of fields:

- `Identity` - A 15-character, case-sensitive field that’s automatically generated for every record. You can find a record’s ID in its URL.
  - *Example* - An account ID looks like 0015000000Gv7qJ.
- System - Read-only fields that provide information about a record from the system, like when the record was created or when it was last changed.
  - *Example* - CreatedDate, LastModifiedById, and LastModifiedDate.
- `Name` - All records need names so you can distinguish between them. You can use text names or auto-numbered names that automatically increment every time you create a record.
  - *Example* - A contact’s name can be Julie Bean. A support case’s name can be CA-1024.
- `Custom`- Fields you create on standard or custom objects are called custom fields.
  - *Example* - You can create a custom field on the Contact object to store your contacts’ birthdays.

Identity, system, and name fields are standard on every object in SF. Each standard object comes with a set of prebuilt, standard fields. Standard object fields can be customized by adding custom fields. You can add custom fields to custom objects.

### Data Types

Every field has a data type. A data type indicates what kind of information the field stores. SF support a variety of different data types, here are a few common types:

- `Checkbox` - for fields that are a simple “yes” or “no,” a checkbox field is what you want.
- `Date` or `DateTime` - these field types represent dates or date/time combinations, like birthdays or sales milestones.
- `Formula` - this special field type holds a value that’s automatically calculated based on a formula that you write. For example, D’Angelo at DreamHouse can write a formula field that automatically calculates a real estate agent’s commission on a home sale.

Data types are pretty straight-forward. One tip is to consider what kind of data to store when creating a custom field.

## Create a Custom Field

1. From Setup, go to `Object Manager` | `Property`.
2. In the sidebar, click `Fields & Relationships`. Notice that there are already some fields there. There’s a name field and some of the system fields we talked about earlier.
3. Click `New` in the top right.
4. For data type, select `Currency`.
5. Click `Next`.
6. Fill out the following:

    a. Field Label: `Price`\
    b. Description: `The listed sale price of the home.`

7. Check the `Required` box.
8. Click `Next`, `Next` again, and then `Save`.

`__c` is an easy way to tell that a particular field is a custom field.

## Create a Record

1. From the App Launcher (The App Launcher icon. in the navigation bar), find and select Sales.
2. Click the Properties tab in the navigation bar. If you don’t see it, look under the More dropdown.
3. Click New in the top corner.
4. Enter a name and price for the property and click Save.

This is what a new record looks like:

![create-a-record](/Developer-Beginner/Data-Modeling/Understand-Custom-and-Standard-Objects/assets/create-a-record.png)

## Customize Responsibly

While it seems easy to add and customize objects, remember what is going on under the hood, because it is technically complicated.

The following are some best practices:

`Be thoughtful of about names`. It can be tempting give them lazy names. Give your objects and fields descriptive, unique names to improve clarity.

`Help out your users`. Even with careful naming, users might not be clear about the purpose of a particular object or field. Include descriptions for custom objects and fields. For specialized or complicated customizations, use help text to give more details.

`Require fields when necessary`. Some fields need to be required, some not. Every property needs a price, right? Make important fields required to avoid incomplete data.

## Resources

- [Salesforce Help: Customize Your Salesforce Org](https://help.salesforce.com/articleView?id=customize_overview.htm&language=en_US)
- [Salesforce Help: Store Information That’s Unique to Your Organization](https://help.salesforce.com/articleView?id=dev_object_def.htm&language=en_US)
- [Trailblazer Community: Customer Success Community](https://trailblazers.salesforce.com/_ui/core/chatter/groups/GroupProfilePage?g=0F9300000001p8wCAA)
