# Salesforce -> Developer Beginner -> Formulas and Validations -> Implement Roll-Up Summary Fields

## Learning Objectives

- Describe what a roll-up summary field is.
- Create a roll-up summary field.
- Apply field-level security to your roll-up summary field.

## Introduction to Roll-Up Summary Fields

While formula fields calculate values using fields within a single record, roll-up summary fields calculate values from a set of related records, such as those in a related list. You can create roll-up summary fields that automatically display a value on a master record based on the values of records in a detail record. These detail records must be directly related to the master through a master-detail relationship.

You can perform different types of calculations with roll-up summary fields. You can count the number of detail records related to a master record, or calculate the sum, minimum value, or maximum value of a field in the detail records. For example, you might want:

- A custom account field that calculates the total of all related pending opportunities.
- A custom order field that sums the unit prices of products that contain a description you specify.

## Defining a Roll-Up Summary Field

Since roll-up summary fields are based on master-detail relationships, it’s useful to review object relationships before creating a roll-up summary field.

## Master-Detail Relationships

Master-detail relationships closely link objects together so that the master record controls specific behaviors of the detail and sub-detail record.

You define a roll-up summary field on the object that is on the master side of a master-detail relationship.

- For example, you can create a roll-up summary field on the Account object, summarizing related opportunities:

    ![Example of fields rolling up to sum opportunities.](/Developer-Beginner/Formulas-and-Validations/Implement-Roll-Up-Summary-Fields/assets/related-opportunities.png)

- There are a few different types of summaries you can use.

| Type | Description |
| ---- | ----------- |
| COUNT | Totals the number of related records. |
| SUM | Totals the values in the field you select in the Field to Aggregate option. Only number, currency, and percent fields are available. |
| MIN | Displays the lowest value of the field you select in the Field to Aggregate option for all directly related records. Only number, currency, percent, date, and date/time fields are available. |
| MAX | Displays the highest value of the field you select in the Field to Aggregate option for all directly related records. Only number, currency, percent, date, and date/time fields are available. |

## Creating the Summary Field

1. From Setup, open Object Manager and click `Account`.
2. On the left sidebar, click `Fields & Relationships`.
3. Click `New`.
4. Choose the Roll-Up Summary field type, and click `Next`.
5. For Field Label, enter Sum of Opportunities and click `Next`.
6. The Summarized Object is the detail object that you want to summarize. Choose Opportunities.
7. Choose the SUM summary type and choose Amount as the Field to Aggregate.
8. Click `Next`, `Next`, and `Save`.

## Examples of Roll-Up Summary Fields

Here are more examples of detail data rolling up to master records.

## Date Opportunity First Created

A roll-up field was created on the Accounts object. The MIN of all Created Date fields on the Opportunities object displays the earliest date an opportunity was created related to an account.

![Example of rolling up the opportunity created date to an account.](/Developer-Beginner/Formulas-and-Validations/Implement-Roll-Up-Summary-Fields/assets/created-date-MIN.png)

## Total Price of All Products Related to an Opportunity

A roll-up field was created on the Opportunities object. Total Price is summarized on the Opportunity Product object to find the grand total of all products related to an opportunity.

![Example of rolling up the product total for an opportunity.](/Developer-Beginner/Formulas-and-Validations/Implement-Roll-Up-Summary-Fields/assets/total-price-roll-up-summary.png)

## Minimum List Price of An Opportunity

A roll-up field was created on the Opportunities object. List Price is summarized on the Opportunity Product object to find the product with the lowest price related to an opportunity.

![Example of rolling up the minimum product price on an opportunity.](/Developer-Beginner/Formulas-and-Validations/Implement-Roll-Up-Summary-Fields/assets/minimum-list-price.png)

## Tell Me More

Congratulations on creating your first roll-up summary field! Keep in mind that the types of fields you can calculate in a roll-up summary field depend on the type of calculation. For example:

- Number, currency, and percent fields are available when you select SUM as the roll-up type.
- Number, currency, percent, date, and date/time fields are available when you select MIN or MAX as the roll-up type.

Learn more about roll-up summary fields at [https://help.salesforce.com](https://help.salesforce.com).

## Resources

- [Salesforce Help: Roll-Up Summary Field](https://help.salesforce.com/articleView?id=fields_about_roll_up_summary_fields.htm&type=5)
- [Salesforce Help: Considerations for Relationships](https://help.salesforce.com/articleView?id=relationships_considerations.htm&type=5)
- [Salesforce Help: Filter Operators Reference](https://help.salesforce.com/articleView?id=filter_operators.htm&type=5)
- [Salesforce Help: Object Relationships](https://help.salesforce.com/articleView?id=overview_of_custom_object_relationships.htm&type=5)
