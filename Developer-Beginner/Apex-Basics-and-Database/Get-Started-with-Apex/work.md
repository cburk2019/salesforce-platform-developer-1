# Salesforce -> Developer Beginner -> Apex Basics & Database -> Get Started with Apex

## Learning Objectives

- Describe the key features of the Apex programming language.
- Save an Apex class and call methods with Anonymous.Apex.
- Use the Developer Console to inspect debug logs.

## Before You Begin

We're excited to accompany you on your Apex adventure. While this module covers basic information about the programming language, it also goes deep, quickly. If this module is your first exposure to Apex, we highly recommend that you first go through the [Quick Start: Apex](https://trailhead.salesforce.com/content/learn/projects/quickstart-apex) project. ([Here is the link to the project folder in this repo](/Developer-Beginner/Apex-Basics-and-Database/Get-Started-with-Apex/Project-Quick-Start-Apex/README.md)) Then come on back, we'll be waiting for you!

Complete!

## What is Apex?

Apex is a programming language that uses Java-like syntax and acts like database stored procedures. Apex enables developers to add business logic to system events, such as button clicks, updates of related records, and Visualforce pages.
As a language, Apex is:

- Hosted
  - Apex is saved, compiled, and executed on the server
    - the Lightning Platform.

- Object oriented
  - Apex supports classes, interfaces, and inheritance.

- Strongly typed

  - Apex validates references to objects at compile time.

- Multitenant aware
  - Because Apex runs in a multitenant platform, it guards closely against runaway code by enforcing limits, which prevent code from monopolizing shared resources.

- Integrated with the database
  - It is straightforward to access and manipulate records. Apex provides direct access to records and their fields, and provides statements and query languages to manipulate those records.

- Data focused
  - Apex provides transactional access to the database, allowing you to roll back operations.

- Easy to use
  - Apex is based on familiar Java idioms.

- Easy to test
  - Apex provides built-in support for unit test creation, execution, and code coverage. Salesforce ensures that all custom Apex code works as expected by executing all unit tests prior to any platform upgrades.

- Versioned
  - Custom Apex code can be saved against different versions of the API.

![Apex is a cloud-based programming language](/Developer-Beginner/Apex-Basics-and-Database/Get-Started-with-Apex/assets/apex-cloud-based-language.png)

### Apex Language Highlights

Like other object-oriented programming languages, these are some of the language constructs that Apex supports:

- Classes, interfaces, properties, and collections (including arrays).
- Object and array notation.
- Expressions, variables, and constants.
- Conditional statements (if-then-else) and control flow statements (for loops and while loops).

Unlike other object-oriented programming languages, Apex supports:

- Cloud development as Apex is stored, compiled, and executed in the cloud.
- Triggers, which are similar to triggers in database systems.
- Database statements that allow you to make direct database calls and query languages to query and search data.
- Transactions and rollbacks.
- The `global` access modifier, which is more permissive than the `public` modifier and allows access across namespaces and applications.
- Versioning of custom code.

In addition, Apex is a *case-insensitive language*.

### Development Tools

You can write and debug Apex on your client computer using the Salesforce Extensions for Visual Studio Code. See [Salesforce Visual Studio Code Extensions](https://developer.salesforce.com/tools/vscode).

You can also write Apex and access debugging information directly in the browser by using the Salesforce user interface. Open the Developer Console under Your Name or the quick access menu (Setup gear icon).

## Data Types Overview

Apex supports various data types, including a data type specific to Salesforce:

- the sObject data type

Apex supports the following data types:

- A primitive, such as:
  - an Integer
  - Double
  - Long
  - Date
  - Datetime
  - String
  - ID
  - Boolean
  - others.

- An sObject, either as a generic sObject or as a specific sObject, such as:
  - an Account
  - Contact
  - or MyCustomObject__c (you’ll learn more about sObjects in a later unit.)

- A collection, including:
  - A list (or array) of primitives, sObjects, user defined objects, objects created from Apex classes, or collections
  - A set of primitives
  - A map from a primitive to a primitive, sObject, or collection

- A typed list of values, also known as an `enum`
- User-defined Apex classes
- System-supplied Apex classes

## Apex Collections: List

Lists hold an ordered collection of objects. Lists in Apex are synonymous with arrays and the two can be used interchangeably.

The following two declarations are equivalent. The `colors` variable is declared using the List syntax.

    ```js
    List<String> colors = new List<String>();
    ```

Alternatively, the colors variable can be declared as an array but assigned to a list rather than an array.

    ```js
    String[] colors = new List<String>();
    ```

Grow collections as needed by using the `List.add()` method to add new elements. Use the square bracket array notation to reference existing elements in the collection by index. You can't, however, use square bracket array notation to add more elements.

This example shows how to add elements to a list when you create it, and then use the `add()` method to add more elements. 

    ```js
    1. // Create a list and add elements to it in one step
    2. List<String> colors = new List<String> { 'red', 'green', 'blue' };
    3. // Add elements to a list after it has been created
    4. List<String> moreColors = new List<String>();
    5. moreColors.add('orange');
    6. moreColors.add('purple');
    ```

List elements can be read by specifying an index between square brackets, just like with array elements. Also, you can use the `get()` method to read a list element. This example is based on the lists created in the previous example and shows how to read list elements using either method. The example also shows how to iterate over array elements.

    ```js
    1. // Get elements from a list
    2. String color1 = moreColors.get(0);
    3. String color2 = moreColors[0];
    4. System.assertEquals(color1, color2);
    5. // Iterate over a list to read elements
    6. for(Integer i=0;i<colors.size();i++) {
    7.     // Write value to the debug log
    8.     System.debug(colors[i]);
    9. }
    ```

### Note

Beyond the Basics

- Apex supports two other collection types: `Set` and `Map`. You can learn more about these in the [Collections](https://developer.salesforce.com/docs/atlas.en-us.224.0.apexcode.meta/apexcode/langCon_apex_collections.htm) section of the Apex Developer Guide.

## Apex Classes

One of the benefits of Apex classes is code reuse. Class methods can be called by triggers and other classes. The following tutorial walks you through saving an example class in your organization, using this class to send emails, and inspecting debug logs.

### Save an Apex Class

Save the `EmailManager` class in your organization:

1. Open the Developer Console under Your Name or the quick access menu (Setup gear icon).
2. In the Developer Console, click `File` | `New` | `Apex Class`, and enter EmailManager for the class name, and then click `OK`.
3. Replace the default class body with the `EmailManager` class example.

    The `EmailManager` class has a public method (`sendMail()`) that sends email and uses built-in Messaging methods of the Apex class library. Also, this class has a private helper method (`inspectResults()`), which can’t be called externally because it is private but is used only within the class. This helper method inspects the results of the email send call and is called by `sendMail()`.

    ```js
    1. public class EmailManager {
    2.     // Public method
    3.     public void sendMail(String address, String subject, String body) {
    4.         // Create an email message object
    5.         Messaging.SingleEmailMessage mail = new Messaging.SingleEmailMessage();
    6.         String[] toAddresses = new String[] {address};
    7.         mail.setToAddresses(toAddresses);
    8.         mail.setSubject(subject);
    9.         mail.setPlainTextBody(body);
    10.         // Pass this email message to the built-in sendEmail method 
    11.         // of the Messaging class
    12.         Messaging.SendEmailResult[] results = Messaging.sendEmail(
    13.                                  new Messaging.SingleEmailMessage[] { mail });
    14.         // Call a helper method to inspect the returned results
    15.         inspectResults(results);
    16.     }
    17.     // Helper method
    18.     private static Boolean inspectResults(Messaging.SendEmailResult[] results) {
    19.         Boolean sendResult = true;
    20.         // sendEmail returns an array of result objects.
    21.         // Iterate through the list to inspect results. 
    22.         // In this class, the methods send only one email, 
    23.         // so we should have only one result.
    24.         for (Messaging.SendEmailResult res : results) {
    25.             if (res.isSuccess()) {
    26.                 System.debug('Email sent successfully');
    27.             }
    28.             else {
    29.                 sendResult = false;
    30.                 System.debug('The following errors occurred: ' + res.getErrors());                 
    31.             }
    32.         }
    33.         return sendResult;
    34.     }
    35. }
    ```

4. Click `File` | `Save` to save your class.

### **NOTE**:

If your code isn’t syntactically correct, an error shows up in the Problems tab. You can use the error details to correct your code.

### Note

#### **Beyond the Basics**

The class you just saved makes use of object-oriented programming (OOP). The class encapsulates the methods that are related to managing email. To be a perfect example of OOP, the class would also contain member variables (attributes) and accessor methods to access those attributes, but for simplicity our class doesn’t have these.

Salesforce compiles your class when you save it.

### Call a Method to Send an Email

Let’s invoke the public method. We’ll use anonymous Apex execution to do so.

- Anonymous Apex allows you to run lines of code on the fly and is a handy way to invoke Apex, especially to test out functionality. Debug log results are generated, as with any other Apex execution.

#### Note

There are other ways to invoke Apex, for example, through triggers. You’ll learn more about triggers in another module.

1. In the Developer Console, click `Debug` | `Open Execute Anonymous Window`.
2. In the window that opens, enter the following. Replace 'Your email address' with your email address.

    ```js
        1. EmailManager em = new EmailManager();
        2. em.sendMail('Your email address', 'Trailhead Tutorial', '123 body');
    ```

3. Click `Execute`. Now that this method has executed, you should have received an email in your inbox. Check your email!

### **Inspect Debug Logs**

Debug logs are useful for debugging your code. When Apex methods execute, the calls are logged in the debug log. Also, you can write your own debug messages to the log, which helps in debugging your code in case there are errors.

The `inspectResults()` helper method, which is called by `sendMail()`, writes messages to the log by using the `System.debug()` method to indicate whether the email send operation was successful or had errors. You can look for these messages in the debug log that was generated when you executed the method.

1. In the Developer Console, click the ***Logs*** tab and double-click the most recent log in the list.
2. Select `Debug Only` to filter the log so that only log lines for `System.debug()` statements are shown.

![Filter the debug log in the Developer Console to view debug messages](/Developer-Beginner/Apex-Basics-and-Database/Get-Started-with-Apex/assets/filter-debug-log.png)

You’ll see the following message in the filtered log view, assuming the email was sent without errors.

`DEBUG|Email sent successfully`

#### Note

Also, you can filter the debug log by searching for any keyword in the Filter field, or by selecting any of the other options. For more information, see the [Log Inspector help](https://help.salesforce.com/HTViewHelpDoc?id=code_dev_console_view_system_log.htm&language=en_US).

### **Call a Static Method**

Because the `sendMail()` method in our class doesn’t access class member variables, it doesn’t need to be an instance method. Let’s change it to a static method by adding the `static` keyword to its declaration.

- Static methods are easier to call than instance methods because they don’t need to be called on an instance of the class but are called directly on the class name.

1. In the Developer Console, find the open tab for the `EmailManager` class and modify the first line of the `sendMail()` method definition to the following (the only change is the added `static` keyword.)

    ```js
    1. public static void sendMail(String address, String subject, String body) {
    ```

2. Click `File` | `Save` to save your class.
3. Modify the statements in your Execute Anonymous window to call the static method on the class name.

    ```js
    EmailManager.sendMail('Your email address', 'Trailhead Tutorial', '123 body');
    ```

4. Click `Execute`. Now that this method has executed, you can check your email, and optionally, the debug log as in the previous steps.

## Resources

- [Introduction to Apex Code (Recorded Webinar)](https://www.youtube.com/watch?v=WBeCWlbGX38)
- [Apex Developer Guide: Introducing Apex](https://developer.salesforce.com/docs/atlas.en-us.224.0.apexcode.meta/apexcode/apex_intro.htm)
- [Trailhead: Developer Console Basics](https://trailhead.salesforce.com/content/learn/modules/developer_console)

## Completed Challenge

### The Challenge

![Create an Apex class with a method that returns a list of strings](/Developer-Beginner/Apex-Basics-and-Database/Get-Started-with-Apex/assets/get-started-with-apex-challenge.png)

### The Solution

![the solution](/Developer-Beginner/Apex-Basics-and-Database/Get-Started-with-Apex/assets/get-started-with-apex-challenge-solution.png)
