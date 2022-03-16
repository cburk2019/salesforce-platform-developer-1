# Create Object Relationships

## Learning Objectives

- Define the different types of object relationships and their typical use cases.
- Create or modify a lookup relationship.
- Create or modify a master-detail relationship.

## What Are Object Relationships?

Object relationships are a special field type that connects two objects together.

### Example: Account

If a sales rep opens an account, they've probably been talking to a few people at that account's company. They've probably made contacts like executives, IT managers, etc, and have stored those contacts' information in Salesforce.

It would make sense that would be a relationship between the Account object and the Contact object. And there is!!!! Woohoo!!

On an Account record, there's a section for Contacts under the related tab.

![account contact relationship example](/assets/account-contact-relationship-example.png)

This is an example of a standard relationship in Salesforce.

Similar to Objects and Fields, custom relationships can be built as well.

In the previous unit, [Understand Custom and Standard Objects](../Understand-Custom-and-Standard-Objects/work.md), I created two custom Objects: `Property` and `Offer`. It would be nice if all Offers showed up on the record of each Property.

## The Wide World of Object Relationships

Two main types of object relationships in Salesforce:

- lookup
- master-detail

### Lookup Relationships

Account to Contact relationship is a `lookup relationship`

A lookup relationship essentially links two objects together so you can "look up" one object from the related items on another object.

Lookup relationships can be one-to-one or even one-to-many. Account to Contact is one-to-many because a single account can have many related contacts.

#### Idea

In the DreamHouse app, you can create a one-to-one relationship between the Property object and a Home Seller object.

### Master-Detail Relationships

Lookup relationships are casual. Master-detail relationships are a bit tighter.

In a master-detail relationship, one object is the master and another is the detail.

The master object controls certain behaviors of the detail object, like who can view the detail's data.

#### Example

In the DreamHouse app, if an owner of a property wanted to take their home off of the market, DreamHouse wouldn't want to keep the offers made on that property. With a master-detail relationship between Property and Offer, you could delete the property and all of its associated offers from the system.

### More on Relationships

Just as in life, relationships are complicated. Below is more info on how to differentiate between lookup and master-detail relationships.

Typically, lookup relationships are used when objects are only related in some cases. Sometimes, a contact is associated with a specific account, but sometimes it is just a contact. Objects in lookup relationships usually work as stand-alone objects and have their own tabs in the UI.

In a master-detail relationship, the detail object does not work as a stand-alone. It is highly dependent on the master. If a record on the master object is deleted, all of its related detail records are deleted as well.

#### Master-Detail Relationship Key Note

When you create a master-detail relationship, you always create the relationship on the detail object.

### Hierarchial Relationship

This is a special type of lookup relationship. The main difference between the two us that hierarchial relationships are `only available on the User object.` You can use them for things such as creating management chains between users.

### To Note

When you add relationships, youre increasing the complexity of your data model. While that is not a bad thing, be cautious when you do things like change and delete objects, records, or fields.

## Create a Custom Object

1. Click the `Object Manager` tab.
2. Click `Create | Custom Object` in the top-right corner.
3. For Label, enter `Favorite`.
4. For Plural Label, enter `Favorites`.
5. Check the box for `Launch New Custom Tab Wizard after saving this custom object.`
6. Leave the rest of the values as default and click `Save`.
7. On the New Custom Object Tab page, click the Tab Style field and select a style you like.
8. Click `Next`, `Next`, and `Save`.

## Create a Lookup Relationship

Create two custom relationship fields on the Favorite object.

1. From Setup, go to `Object Manager | Favorite`.
2. On the sidebar, click `Fields & Relationships`.
3. Click `New`.
4. Choose `Lookup Relationship` and click `Next`.
5. For Related To, choose `Contact`. For the purposes of DreamHouse, contacts represent potential home buyers.
6. Click `Next`.
7. For Field Name, enter Contact, then click `Next`.
8. Click `Next`, `Next`, and `Save`.

## Create a Master-Detail Relationship

1. On the Object Manager page for the custom object, click `Fields & Relationships`.
2. Click `New`.
3. Select `Master-Detail Relationship` and click `Next`.
4. For Related To, choose `Property`.
5. Click `Next`.
6. For Field Name, enter Property and click `Next`.
7. Click `Next`, `Next`, and `Save`.

## Add a Favorite Property

1. From the App Launcher (The App Launcher icon. in the navigation bar), find and select `Sales`.
2. Click the `Properties` tab in the navigation bar. If you don’t see it, look under the `More` dropdown.
3. Click the name of a Property record.
4. Click `Related`. You’ll see Favorites (0) in the related tab.
5. Click `New`.
6. Enter a name for Favorite Name, then click `Save`.

Yay! Our Favorite object is all set up!

## Resources

- [Salesforce Help: Object Relationships Overview](https://help.salesforce.com/articleView?id=overview_of_custom_object_relationships.htm&language=en_US)
- [Salesforce Help: Considerations for Relationship](https://help.salesforce.com/articleView?id=relationships_considerations.htm&language=en_US)
