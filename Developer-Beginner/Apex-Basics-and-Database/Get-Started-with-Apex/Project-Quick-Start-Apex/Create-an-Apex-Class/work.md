# Salesforce -> Developer Beginner -> Apex Basics & Database -> Get Started with Apex -> Project: Quick Start: Apex -> Create an Apex Class

## Note

Salesforce has two different user interfaces:

- Lightning Experience
- and Salesforce Classic

This project is designed for Lightning Experience. You can learn about [switching between interfaces, enabling Lightning Experience](https://help.salesforce.com/articleView?id=lex_switching_uis.htm&language=en_US), and more in the [Lightning Experience Basics](https://trailhead.salesforce.com/module/lex_migration_introduction) module here on Trailhead.

## Introduction

Apex is a strongly typed, object-oriented programming language that allows developers to execute flow and transaction control statements on the Salesforce platform.

If you’re used to Java or .NET development, you’ll find the programming in Apex fairly straightforward. If you’ve never coded before, you might be surprised how easy it is to access and manipulate data using Apex. In this Quick Start, you'll create a simple Apex class to update old Account records.

## Create an Apex Class

The Developer Console is where you write and test your code in Salesforce. We’ll take a tour of the `Developer Console` and `Source Code Editor` in just a minute.

The first step is to create an Apex class.

1. If you haven’t already, log in to Trailhead, then launch your Trailhead Playground by clicking `Launch` at the bottom of this page. This opens your Trailhead Playground in a new tab.
2. Click the `setup gear` *Gear icon* to access Setup in Lightning Experience. and select `Developer Console`.
3. From the `File` menu, select `New` | `Apex Class`.
4. For the class name, enter `OlderAccountsUtility` and then click `OK`.

The code in your editor looks like this:

```js
1. public class OlderAccountsUtility {
2. }
```

Excellent! Now let's add a method that can find and update older Accounts.
