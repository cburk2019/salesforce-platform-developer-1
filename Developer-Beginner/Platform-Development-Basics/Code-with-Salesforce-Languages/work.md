# Code with Salesforce Languages

## Learning Objectives

- Identify the benefits of Lightning components.
- Describe how Visualforce is used in Lightning Experience.
- Outline the ways Apex is used to support Lightning components and Visualforce.

## Three Core Programmatic Technologies for Salesforce Developers

- ***Lightning Component Framework*** - A UI development framework similar to AngularJS or React
- ***Apex*** - Salesforce's proprietary programming language with Java-like syntax
- ***Visualforce*** - A markup language that lets you create custom Salesforce pages with code that looks a lot like HTML. You can also, in addition, use a powerful combination of JavaScript and Apex.

### Lightning Component Framework

The lightning component framework is a user interface (UI) development framework for desktop and mobile. As implied in its name, it is a component-based approach to UI development. There are prebuilt and custom Light components and you can quickly develop sleek and consistent UIs for apps.

If you are familiar with frameworks like AngularJS, React, or Polymer (I do with React 😊) that I should have a good idea of what to expect with Lightning components.

The biggest plus is that Lightning components are ready to go with all business data in Salesforce.

## Developer Console

The Developer Console is the Salesforce IDE (integrated development environment) that is used to develop, debug, and test code in an org.

![developer console](/assets/developer-console.png)

Things to note from the Developer Console:

- XML markup
- Contains both Aura-specific and static HTML tags
- Uses a `<namespace:tagName>` convention for its tags, each representing a smaller, or child, component

Under the CONTROLLER tab on the right, you can see JavaScript being used. Lightning components use client-side JavaScript controllers and server-side Apex controllers.

![Developer Console JavaScript](/assets/developer-console-javascript.png)

You can create and access the controllers as well as other assets like component style sheets, from the **BUNDLE** menu.

### Lightning Components being Mobile ready

A great thing about Lightning components is that they are mobile-ready. When apps are created for the Salesforce mobile app, there is no need to worry about the way Lightning components display. They can just be added to the app let the SF platform handle the rest.

## Apex

Earlier, Process Builder was covered as a low-code tool.

You can extend the functionality by writing a little code.

Here is how Push Notifications are added in the Developer Console:

![DC push notifications](/assets/developer-console-apex.png)

There are two things to notice in the picture:

1. The `@InvocableMethod` annotation before the method signature. It has a label attribute that allows other tools like Process Builder to execute the method.
2. There arw a few queries in the method body.
    - `Property__c property = [SELECT Name, Price__c from Property__c WHERE Id=:propId];`
        - This SQL-like phrase is actually `SOQL` or ***Salesforce Object Query Language***. SOQL can be used to read records from the database in your code.

Extending Process Builder is only one of many ways you can use Apex to enhance your org's functionality.

## Visualforce

The last major pillar of coding on the SF platform!

If you've done any web development, Visualforce will feel familiar to you. Visualforce allows you to create and customize pages in Salesforce as well as integrate with other standard web technologies, such as HTML, CSS and JavaScript.

### Differences between Lightning components and Visualforce

The primary difference is the name.

With Lightning components, you are developing components that can be pieced together to create pages.

With Visualforce, you are developing entire pages at once.

Lightning components are newer and better for things like mobile development, there are several situations where it can make more sense to use Visualforce.

### SLDS - Salesforce Lightning Design System

The SLDS system allows you to style your pages so that they match the look and feel of Salesforces's new interface, Lightning Experience.

Visualforce uses a similar convention to Lightning components with `<apex:tagName>`.

One thing that is not shown here, but will be covered going forward, are `Apex Controllers`.

As previously mentioned, Lightning components use JavaScript on the client-side and Apex on the server-side. Visualforce pages can also use server-side Apex controllers. Most complex pages use quite a bit.

As I continue to explore Visualforce, I'll get VERY famioliar with Apex controllers.

### Note

You can also access and preview Visualforce pages by searching Visualforce Pages from the Quick Find bar in Setup.
