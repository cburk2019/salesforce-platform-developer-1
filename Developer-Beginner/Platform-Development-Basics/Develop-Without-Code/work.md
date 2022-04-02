# Develop Without Code

## Learning Objectives

- Describe the benefits of the metadata-driven development model.
- Define and give examples of the no-code and low-code development approaches.

## The Power of Metadata

### Three Important Terms

1. Objects
2. Fields
3. Records

When you look at data in Salesforce, you might think that you're looking at a user interface sitting on top of a run-of-the-mill relational database. But what you’re actually looking at is an abstraction of the database that’s driven by the platform’s metadata-aware architecture.

- Objects are our database tables.\
- The fields on those objects are columns.\
- Records are rows in the database.

This analogy is true for both standard objects that come with Salesforce by default and any custom objects that you build yourself.

Metadata forms the structure of an org. Whether defining field, business processes or more complex tasks, metadata holds your configuration.

***METADATA-DRIVEN DEVELOPMENT MODEL***

This is one of the key differences between developing on the platform and developing outside of Salesforce.

The Salesforce platform is metadata-aware.\
It can auto-generate a significant part of the user experience for you.

Things like dialogs, record lists, detail views, and forms - things you would normally have to develop on your own - come for free.

CRUD is a built-in functionality on both standard objects and also custom object records in the DB (database).

## What's Inside DreamHouse

The DreamHouse App is an example of what is typically referred to as an internal employee productivity app.

The app itself is built using various parts of the Salesforce platform. Below is an overview diagram of the system landscape of the DreamHouse application set. It includes Heroku services and other connected devices.

![DreamHouse Application Set](/Developer-Beginner/Platform-Development-Basics/Develop-Without-Code/assets/DreamHouse-app-set.png)

For the DreamHouse app, Salesforce has created 3 custom objects that support the core app functionality:

- Brokers - Information about partner brokers
- Properties - Photos and information about properties that are on the market
- Favorites - Properties customers have favorited

### DreamHouse data model

There is a handy tool that the platform provides called ***Schema Builder***.

![schema builder example](/Developer-Beginner/Platform-Development-Basics/Develop-Without-Code/assets/schema-builder-example.png)

## No-Code and Low-Code Development

The Salesforce platform encourages you to minimize code! But.. it's not because Salesforce doesn't love code, rather, it's because the platform's metadata-driven architecture lets the user complete the most basic development tasks without writing a single line.

Salesforce offers a host of tools for "point-and-click" or ***"declarative-development"***. Most of the tools require little to node understanding of development principles: AKA no-code.

Someone who thinks JSON is just missing a letter can construct a robust and complex data model. A person who hears Cron and thinks it’s some kind of sci-fi film can schedule batch jobs. In fact, someone without any coding knowledge at all can develop entire apps in Salesforce using prebuilt components and point-and-click tools.

### Low-Code

Some development tasks, like writing validation rules or hooking up components with UI elements, are considered low code. That means they require some basic programmatic knowledge to complete, but aren’t so rigorous that they’re considered programmatic. For example, if you know something about logic, conditions, and CRUD operations, you can do more with Process Builder.

The no-code and low-code development capabilities that the Salesforce platform provides means that you, as a developer, can move faster. If you’re the only person at your company developing on Salesforce, you can use the platform’s many declarative tools to build more in less time. If you’re working on a team with non-coders, you can leave the declarative development tasks to them while you double down on more code-intensive projects.

![process builder example](/Developer-Beginner/Platform-Development-Basics/Develop-Without-Code/assets/process-builder-example.png)
