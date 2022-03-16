# Work with Schema Builder

## Learning Objectives

- Describe the advantages of using Schema Builder for data modeling.
- Use Schema Builder to create a schema for a given object model.
- Use Schema Builder to add a custom object to your schema.
- Use Schema Builder to add a custom field to your schema.

## See Your Data in Action

So far, we have created custom objects, fields, and relationships. My app's data model is starting to get a little more complicated.

`Schema Builder` is a tool that lets you visualize and edit your data model. It's useful for designing and understanding complex data models.

### Example Schema Builder

1. From Setup, search for and click Schema Builder in the Quick Find box.
2. In the left panel, click `Clear All`.
3. Check Contact, Favorite, Offer, and Property. You should have the Favorite object from the previous unit, and the Offer and Property objects from the previous challenges.
4. Click `Auto-Layout`.

![schema builder example 2](/assets/schema-builder-example-2.png)

You can drag the objects around the canvas and it won't affect the objects or their relationships. This is to help visualize the data model.

Schema Builder is a handy tool that you can use to introduce your Salesforce customizations to a co-worker or explaining the way data flows throughout the system / app.

## Create an Object with Schema Builder

You can create objects using Schema Builder.

This is a good option if you are designing your system and want to be able to revise all of your customizations on the spot.

1. In the left sidebar, click the `Elements` tab.
2. Click `Object` and drag it onto the canvas.
3. Enter information about your object. You can make it whatever you want!
4. Click `Save`.

## Create Fields with Schema Builder

1. From the Elements tab, choose a field type and drag it onto the object you just created. Notice that you can create relationship fields, formula fields, and normal fields in Schema Builder.
2. Fill out the details about your new field.
3. Click `Save`.

## Sum It Up

We've learned a lot in this learning module!

- data model
- database

- objects
- fields
- records
  - custom objects
  - custom fields
  - custom records

- lookup relationship
- master-detail relationship
- hierarchial relationship

- visualizing data model with Schema Builder

As you dive into more advanced content, custom objects and fields will be EVERYWHERE. But.... before you know it, I'll be a data modeling pro! Yay! Happy building!

## Resources

- [Salesforce Help: Design Your Own Data Model](https://help.salesforce.com/articleView?id=schema_builder.htm&language=en_US)
- [Salesforce Help: Schema Builder Custom Object Reference](https://help.salesforce.com/articleView?id=schema_builder_elements_objects_ref.htm&language=en_US)
