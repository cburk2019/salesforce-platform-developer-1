# Salesforce -> Developer Beginner -> Apex Basics & Database -> Get Started with Apex -> Project: Quick Start: Apex -> Add a Method to the Class

## Add a Method to the Class

### Create a Method

A class usually contains one or more methods that do something useful. In this step, you’ll create the `updateOlderAccounts` method, which gets the first five Account records ordered by the date created. It then updates the description field to say that this is a “Heritage Account,” meaning accounts that are older than other accounts.

1. In the body of the `OlderAccountsUtilityclass` (the information between the curly brackets), copy and paste the following method.

    ```js
    1.    public static void updateOlderAccounts() {
    2.      // Get the 5 oldest accounts
    3.      Account[] oldAccounts = [SELECT Id, Description FROM Account ORDER BY CreatedDate ASC LIMIT 5];
    4.      // loop through them and update the Description field
    5.      for (Account acct : oldAccounts) {
    6.          acct.Description = 'Heritage Account';
    7.      }
    8.      // save the change you made
    9.      update oldAccounts;
    10.    }
    ```

2. Click File | Save.

![My first Apex class method!](/assets/my-first-apex-class-method.png)

1. The code first sorts Accounts by the date that they were created on.
2. It then grabs the five oldest records. It uses the SOQL query language (line 3) to do the querying and sorting.
3. It then iterates through each Account record to update the Description field.
4. Finally, it updates the Account records by using the:

- Apex Data Manipulation Language (DML).

If you're familiar with Java and C#, you'll notice a lot of similarity in the syntax.

Well I'm not! I learned JavaScript, what a journey this'll be!
