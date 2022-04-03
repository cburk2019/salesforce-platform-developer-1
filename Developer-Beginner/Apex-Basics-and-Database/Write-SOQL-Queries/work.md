# Salesforce -> Developer Beginner -> Apex Basics & Database -> Write SOQL Queries

## Write SOQL Queries

## Learning Objectives

- Write SOQL queries in Apex.
- Execute SOQL queries by using the Query Editor in the Developer Console.
- Execute SOQL queries embedded in Apex by using Anonymous Apex.
- Query related records.

## Get Started with SOQL

To read a record from Salesforce, you must write a query. Salesforce provides the ***`Salesforce Object Query Language`***, or ***`SOQL`*** in short, that you can use to read saved records. SOQL is similar to the standard SQL language but is customized for the Lightning Platform.

Because Apex has direct access to Salesforce records that are stored in the database, you can embed SOQL queries in your Apex code and get results in a straightforward fashion.

- When SOQL is embedded in Apex, it is referred to as ***inline SOQL***.

To include SOQL queries within your Apex code, wrap the SOQL statement within square brackets and assign the return value to an array of sObjects. For example, the following retrieves all account records with two fields, Name and Phone, and returns an array of Account sObjects.

```js
1. Account[] accts = [SELECT Name,Phone FROM Account];
```

### **Prerequisites**

Some queries in this unit expect the org to have accounts and contacts. Before you run the queries, create some sample data.

1. In the Developer Console, open the Execute Anonymous window from the ***Debug*** menu.
2. Insert the below snippet in the window and click ***Execute***.

```js
1. // Add account and related contact
2. Account acct = new Account(
3.     Name='SFDC Computing',
4.     Phone='(415)555-1212',
5.     NumberOfEmployees=50,
6.     BillingCity='San Francisco');
7. insert acct;
8. // Once the account is inserted, the sObject will be 
9. // populated with an ID.
10. // Get this ID.
11. ID acctID = acct.ID;
12. // Add a contact to this account.
13. Contact con = new Contact(
14.     FirstName='Carol',
15.     LastName='Ruiz',
16.     Phone='(415)555-1212',
17.     Department='Wingo',
18.     AccountId=acctID);
19. insert con;
20. // Add account with no contact
21. Account acct2 = new Account(
22.     Name='The SFDC Query Man',
23.     Phone='(310)555-1213',
24.     NumberOfEmployees=50,
25.     BillingCity='Los Angeles',
26.     Description='Expert in wing technologies.');
27. insert acct2;
```

### **Use the Query Editor**

The Developer Console provides the Query Editor console, which enables you to run your SOQL queries and view results. The Query Editor provides a quick way to inspect the database. It is a good way to test your SOQL queries before adding them to your Apex code. When you use the Query Editor, you must supply only the SOQL statement without the Apex code that surrounds it.

Let’s try running the following SOQL example:

1. In the Developer Console, click the *Query Editor* tab.
2. Copy and paste the following into the first box under Query Editor, and then click ***Execute***.

```js
1. SELECT Name,Phone FROM Account
```

All account records in your org appear in the Query Results section as rows with fields.

## Basic SOQL Syntax

This is the syntax of a basic SOQL query:

```js
1. SELECT fields FROM ObjectName [WHERE Condition]
```

The WHERE clause is optional. Let’s start with a very simple query. For example, the following query retrieves accounts and gets Name and Phone fields for each account.

```js
1. SELECT Name,Phone FROM Account
```

The query has two parts:

1. `SELECT Name,Phone`: This part lists the fields that you would like to retrieve. The fields are specified after the SELECT keyword in a comma-delimited list. Or you can specify only one field, in which case no comma is necessary (e.g. `SELECT Phone`).
2. `FROM Account`: This part specifies the standard or custom object that you want to retrieve. In this example, it’s Account. For a custom object called Invoice_Statement, it is Invoice_Statement__c.

### Note

### **Beyond the Basics**

Unlike other SQL languages, you can’t specify * for all fields. You must specify every field you want to get explicitly. If you try to access a field you haven’t specified in the SELECT clause, you’ll get an error because the field hasn’t been retrieved.

You don’t need to specify the Id field in the query as it is always returned in Apex queries, whether it is specified in the query or not. For example: `SELECT Id,Phone FROM Account` and `SELECT Phone FROM Account` are equivalent statements. The only time you may want to specify the Id field if it is the only field you’re retrieving because you have to list at least one field: `SELECT Id FROM Account`. You may want to specify the Id field also when running a query in the Query Editor as the ID field won’t be displayed unless specified.

### **Filter Query Results with Conditions**

If you have more than one account in the org, they will all be returned. If you want to limit the accounts returned to accounts that fulfill a certain condition, you can add this condition inside the WHERE clause. The following example retrieves only the accounts whose names are SFDC Computing. Note that comparisons on strings are case-insensitive.

```js
1. SELECT Name,Phone FROM Account WHERE Name='SFDC Computing'
```

The WHERE clause can contain multiple conditions that are grouped by using logical operators (AND, OR) and parentheses. For example, this query returns all accounts whose name is SFDC Computing that have more than 25 employees:

```js
1. SELECT Name,Phone FROM Account WHERE (Name='SFDC Computing' AND NumberOfEmployees>25)
```

This is another example with a more complex condition. This query returns all of these records:

- All SFDC Computing accounts
- All accounts with more than 25 employees whose billing city is Los Angeles

```js
1. SELECT Name,Phone FROM Account WHERE (Name='SFDC Computing' OR (NumberOfEmployees>25 AND BillingCity='Los Angeles'))
```

### **Note**

### **Beyond the Basics**

Instead of using the equal operator (=) for comparison, you can perform fuzzy matches by using the `LIKE` operator. For example, you can retrieve all accounts whose names start with SFDC by using this condition: `WHERE Name LIKE 'SFDC%'`. The % wildcard character matches any or no character. The _ character in contrast can be used to match just one character.

### **Order Query Results**

When a query executes, it returns records from Salesforce in no particular order, so you can’t rely on the order of records in the returned array to be the same each time the query is run. You can however choose to sort the returned record set by adding an ORDER BY clause and specifying the field by which the record set should be sorted. This example sorts all retrieved accounts based on the Name field.

```js
1. SELECT Name,Phone FROM Account ORDER BY Name
```

The default sort order is in alphabetical order, specified as ***`ASC`***. The previous statement is equivalent to:

```js
1. SELECT Name,Phone FROM Account ORDER BY Name ASC
```

To reverse the order, use the ***`DESC`*** keyword for ***`descending`*** order:

```js
1. SELECT Name,Phone FROM Account ORDER BY Name DESC
```

You can sort on most fields, including numeric and text fields. *You can’t sort on fields like rich text and multi-select picklists*.

Try these SOQL statements in the Query Editor and see how the order of the returned record changes based on the Name field.

### **Limit the Number of Records Returned**

You can limit the number of records returned to an arbitrary number by adding the `LIMIT n` clause where *`n`* is the number of records you want returned. Limiting the result set is handy when you don’t care which records are returned, but you just want to work with a subset of records. For example, this query retrieves the first account that is returned. Notice that the returned value is one account and not an array when using `LIMIT 1`.

```js
1. Account oneAccountOnly = [SELECT Name,Phone FROM Account LIMIT 1];
```

## Combine All Pieces Together

You can combine the optional clauses in one query, in the following order:

```js
1. SELECT Name,Phone FROM Account 
2.                    WHERE (Name = 'SFDC Computing' AND NumberOfEmployees>25)
3.                    ORDER BY Name
4.                    LIMIT 10
```

Execute the following SOQL query in Apex by using the Execute Anonymous window in the Developer Console. Then inspect the debug statements in the debug log. One sample account should be returned.

```js
1. Account[] accts = [SELECT Name,Phone FROM Account 
2.                    WHERE (Name='SFDC Computing' AND NumberOfEmployees>25)
3.                    ORDER BY Name
4.                    LIMIT 10];
5. System.debug(accts.size() + ' account(s) returned.');
6. // Write all account array info
7. System.debug(accts);
```

### **Access Variables in SOQL Queries**

SOQL statements in Apex can reference Apex code variables and expressions if they are preceded by a colon (:). The use of a local variable within a SOQL statement is called a ***bind***.

This example shows how to use the `targetDepartment` variable in the WHERE clause.

```js
1. String targetDepartment = 'Wingo';
2. Contact[] techContacts = [SELECT FirstName,LastName 
3.                           FROM Contact WHERE Department=:targetDepartment];
```

### **Query Related Records**

Records in Salesforce can be linked to each other through relationships: ***lookup relationships*** or ***master-detail relationships***.

For example, the Contact has a lookup relationship to Account. When you create or update a contact, you can associate it with an account. The contacts that are associated with the same account appear in a related list on the account’s page. In the same way you can view related records in the Salesforce user interface, you can query related records in SOQL.

To get child records related to a parent record, add an inner query for the child records. The FROM clause of the inner query runs against the relationship name, rather than a Salesforce object name. This example contains an inner query to get all contacts that are associated with each returned account. The FROM clause specifies the Contacts relationship, which is a default relationship on Account that links accounts and contacts.

```js
1. SELECT Name, (SELECT LastName FROM Contacts) FROM Account WHERE Name = 'SFDC Computing'
```

This next example embeds the example SOQL query in Apex and shows how to get the child records from the SOQL result by using the Contacts relationship name on the sObject.

```js
1. Account[] acctsWithContacts = [SELECT Name, (SELECT FirstName,LastName FROM Contacts)
2.                                FROM Account 
3.                                WHERE Name = 'SFDC Computing'];
4. // Get child records
5. Contact[] cts = acctsWithContacts[0].Contacts;
6. System.debug('Name of first associated contact: ' 
7.              + cts[0].FirstName + ', ' + cts[0].LastName);
```

You can traverse a relationship from a child object (contact) to a field on its parent (Account.Name) by using dot notation. For example, the following Apex snippet queries contact records whose first name is Carol and is able to retrieve the name of Carol’s associated account by traversing the relationship between accounts and contacts.

```js
1. Contact[] cts = [SELECT Account.Name FROM Contact 
2.                  WHERE FirstName = 'Carol' AND LastName='Ruiz'];
3. Contact carol = cts[0];
4. String acctName = carol.Account.Name;
5. System.debug('Carol\'s account name is ' + acctName);
```

### **Note**

The examples in this section are based on standard objects. Custom objects can also be linked together by using custom relationships. Custom relationship names end with the `_ _r` suffix. For example, invoice statements are linked to line items through the `Line_Items_ _r` relationship on the `Invoice_Statement_ _c` custom object.

### **Query Record in Batches By Using SOQL For Loops**

With a SOQL for loop, you can include a SOQL query within a `for` loop. The results of a SOQL query can be iterated over within the loop. SOQL for loops use a different method for retrieving records—records are retrieved using efficient chunking with calls to the query and queryMore methods of the SOAP API. By using SOQL for loops, you can avoid hitting the heap size limit.

SOQL `for` loops iterate over all of the sObject records returned by a SOQL query. The syntax of a SOQL `for` loop is either:

```js
1. for (variable : [soql_query]) {
2.     code_block
3. }
```

or

```js
1. for (variable_list : [soql_query]) {
2.     code_block
3. }
```

Both  `variable` and  `variable_list` must be of the same type as the sObjects that are returned by the  `soql_query`.

It is preferable to use the sObject list format of the SOQL for loop as the loop executes once for each batch of 200 sObjects. Doing so enables you to work on batches of records and perform DML operations in batch, which helps avoid reaching governor limits.

```js
1. insert new Account[]{new Account(Name = 'for loop 1'), 
2.                      new Account(Name = 'for loop 2'), 
3.                      new Account(Name = 'for loop 3')};
4. // The sObject list format executes the for loop once per returned batch
5. // of records
6. Integer i=0;
7. Integer j=0;
8. for (Account[] tmp : [SELECT Id FROM Account WHERE Name LIKE 'for loop _']) {
9.     j = tmp.size();
10.     i++;
11. }
12. System.assertEquals(3, j); // The list should have contained the three accounts
13.                        // named 'yyy'
14. System.assertEquals(1, i); // Since a single batch can hold up to 200 records and,
15.                        // only three records should have been returned, the 
16.                        // loop should have executed only once
```

## Resources

- [SOQL and SOSL Reference](https://developer.salesforce.com/docs/atlas.en-us.224.0.soql_sosl.meta/soql_sosl/)

## Challenge

![The challenge - Create an Apex class that returns contacts based on incoming parameters.](/Developer-Beginner/Apex-Basics-and-Database/Write-SOQL-Queries/assets/write-soql-queries-challenge.png)

### The Solution

![the solution](/Developer-Beginner/Apex-Basics-and-Database/Write-SOQL-Queries/assets/write-soql-queries-challenge-solution.png)
