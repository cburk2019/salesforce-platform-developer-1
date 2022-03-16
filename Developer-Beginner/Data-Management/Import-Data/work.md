# Salesforce -> Developer Beginner -> Data Management -> Import Data

## Learning Objectives

- Describe and compare the different options for importing data into Salesforce.
- List the steps involved in preparing and importing data from a sample .csv file using the Data Import Wizard.

## Introduction to Data Import

Importing data into Salesforce can be easily done. Supported data sources include any program that can save data in the comma delimited text format (.csv)

Salesforce offers two main methods for importing data:

1. `Data Import Wizard`

    - accessible via `Setup`
    - allows you to import data in common standard objects such as contacts, leads, accounts, as well as custom objects.
    - it can import up to 50,000 records at a time!
    - simple interface that can specify configuration parameters, data sources, and field mappings that map the field names in your import file with the field names in Salesforce.

2. `Data Loader`

    - client application
    - import up to 5,000,000 records at a time!!!!! of any type
    - either from files or a database connection.
    - operated either through the UI (user interface) or the CL (command line)
    - in the CL, you need to specify data sources, field mappings, and other parameters via configuration files.
        - this makes it possible to automate the import process, using API calls

### Note

With either the Data Import Wizard or the Data Loader, the number of records you can import depends on:

- your permissions
- the type of data you are importing
- the overall data storage limits for your org
- the type of objects you can import depends on your edition

## Use the Data Import Wizard When

- You need to load less than 50,000 records
- The objects you need to import are supported by the wizard
- You do not need the import process to be automated

## Use the Data Loader When

- You need to load 50,000 to 5,000,000 records. If you need to load more than 5,000,000 records, we recommend you work with a Salesforce partner or visit the [AppExchange](http://appexchange.salesforce.com/) for a suitable partner product.

### Note

Data Loader uses the SOAP API to process records. For faster processing, you can configure it to use the Bulk API instead.

The Bulk API is optimized to load a larger number of records simultaneously. It is faster than the SOAP API due to parallel processing and fewer network round-trips.

## Prepare for Data Import

### Example Company - Cloud Kicks

Cloud Kicks manufactures custom sneakers, designed and personalized for their customers.

Sales - Candace and Jose
Salesforce Admin - Linda

They want to bring their CRM data into Salesforce. They have less than 50,000 records, Linda decides Data Import Wizard.

### Follow These Steps Before You Start Importing Any Data

1. Use your existing software to create an export file.
2. Clean up the import file for accuracy and consistency. This involves updating the data to remove duplicates, delete unnecessary information, correct spelling and other errors, and enforce naming conventions.
3. Compare your data fields with the Salesforce fields you can import into, and verify that your data will be mapped into the appropriate Salesforce fields. You might need to fine-tune the mapping before starting the import. For details, see [Field Mapping for Data Sources](https://help.salesforce.com/s/articleView?id=sf.field_mapping_for_other_data_sources_and_organization_import.htm&type=5) in the online help.
4. Make any configuration changes required in Salesforce to handle the imported data. For example, you might need to create new custom fields, add new values to picklists, or temporarily deactivate workflow rules.

### Note

Salesforce recommends you import using a small test file first to make sure you've prepared your source data correctly.

## Use the Data Import Wizard

Once you have created an export file and cleaned up the data for import, follow these steps to import data using the Data Import Wizard:

1. Start the wizard.

    - `a`. From Setup, enter Data Import Wizard in the Quick Find box, then select `Data Import Wizard`.
    - `b`. Review the information provided on the welcome page, then click `Launch Wizard!`

2. Choose the data that you want to import.

    - `a`. To import accounts, contacts, leads, solutions, person accounts, or campaign members, click `Standard Objects`. To import custom objects, click `Custom Objects`.
    - `b`. Specify whether you want to add new records to Salesforce, update existing records, or add and update records simultaneously.
    - `c`. Specify matching and other criteria as necessary. Hover over the question marks for more information about each option.
    - `d`. Specify the file that contains your data. You can specify your data file by dragging the CSV to the upload area of the page or by clicking the CSV category you’re using and then navigating to and selecting the file.
    - `e`. Choose a character encoding method for your file. Most users can accept the default character encoding.
    - `f`. Click `Next`

3. Map your data fields to Salesforce data fields. The Data Import Wizard tries to map as many of your data fields as possible to standard Salesforce data fields. If Salesforce can’t automatically map fields, however, you do it manually. Unmapped fields are not imported into Salesforce. To see a list of standard Salesforce data fields, from Setup, at the top of the page, click `Object Manager`. Click the object whose fields you’re interested in, and click `Fields & Relationships`. For example, if you want to see a list of standard Salesforce fields for leads, click `Object Manager` | `Lead` | `Fields & Relationships`.

    - `a.` Scan the list of mapped data fields and locate any unmapped fields.
    - `b.` Click `Map` to the left of each unmapped field.
    - `c.` In the Map Your Field dialog box, choose the Salesforce fields you want to map to and click `Map`. The Map Your Field dialog box also gives you the option of saving data from unmapped fields in a general notes field for accounts and contacts. To do so, choose Account Note or Contact Note from the Map To drop-down list and click `Map`.
    - `d.` To change mappings that Salesforce performed automatically, click `Change` to the left of the appropriate field, then choose the Salesforce fields you want to map to and click `Map`.
    - `e.` Click `Next`.

4. Review and start your import.

    - `a.` Review your import information on the Review page. If you still have unmapped fields that you want to import, click `Previous` to return to the previous page and specify your mappings.
    - `b.` Click `Start Import`.

5. Check import status. From Setup, enter “Bulk Data Load Jobs” in the Quick Find box, then select `Bulk Data Load Jobs`.  The user who starts the data import receives a status email when the import is completed.

### Note

Use the zoom option in your browser to adjust (shrink) the size of the content if you cannot see the Map button.

The user who starts the data import receives a status email when the import is completed.

## Tell Me More!!

The following information can help to integrate imported data into Salesforce:

### New Values for Picklists and Multi-Select Picklists

If you import a picklist value that doesn’t match an existing picklist value:

- For an unrestricted picklist, the Data Import Wizard uses the value that’s in the import file.
- For a restricted picklist, the Data Import Wizard uses the picklist’s default value.

### Multi-Select Picklists

- To import multiple values into a multi-select picklist, separate the values by a semicolon `;` in your import file

### Checkboxes

- To import data into a checkbox field, use 1 for checked values and 0 for unchecked values.

### Default Values

- For picklist, multi-select picklist, and checkbox fields, if you do not map the field in the import wizard, the default value for the field, if any, is automatically inserted into the new or updated record.

### Date / Time Fields

- Ensure that the format of any date/time fields you are importing matches how they display in Salesforce per your locale setting.

### Formula Fields

- Formula fields cannot accept imported data because they are read-only.

### Field Validation Rules

- Salesforce runs validation rules on records before they are imported. Records that fail validation aren’t imported. Consider deactivating the appropriate validation rules before running an import if they affect the records you are importing.

## Resources

- [Data Import FAQ](https://help.salesforce.com/HTViewHelpDoc?id=faq_import_general.htm&language=en_US)
- [Preparing Your Data For Import](https://help.salesforce.com/apex/HTViewHelpDoc?id=import_prepare.htm&language=en_US)
- [Data Loader Overview](https://help.salesforce.com/HTViewHelpDoc?id=data_loader.htm&language=en_US)
- [Explore how to import data mre effectively in Salesforce](http://pages.mail.salesforce.com/achievemore/managedata/?utm_source=trailhead&utm_medium=resources&utm_campaign=datamanagement&utm_content=importdata)
- [Data Import Video Series](http://salesforce.vidyard.com/watch/ARIjWm2qrDkJVJxEhReFug?_ga=2.216163155.490959917.1647221935-1683129185.1644972267)
