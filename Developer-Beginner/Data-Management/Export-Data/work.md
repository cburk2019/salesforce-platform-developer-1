# Salesforce -> Developer Beginner -> Data Management -> Export Data

## Learning Objectives

- Describe and compare the two methods of exporting data from Salesforce.
- Export data manually using the Data Export Service.
- Set up automatic export of data on a weekly or monthly schedule.

## Introduction to Data Export

Exporting data from Salesforce is easy and it can be done manually or on an automatic schedule.

Data is exported as a set of comma-separated values (CSV) files.

Data export tools provide a convenient way to obtain a copy of your Salesforce data for either backup or for importing into a different system.

Salesforce offers two main methods for exporting data:

### 1. Data Export Service

This is an in-browser service that is accessible through the Setup menu.

- allows data to be exported manually once every 7 days (weekly reports) or 29 days (monthly reports).
- allows data to be exported automatically at weekly or monthly intervals

Weekly exports are available in Enterprise, Performance, and Unlimited Editions. In Professional and Developer Edition, you can generate backup files only every 29 days, or automatically at monthly intervals ONLY.

### 2. Data Loader

- client application
- must be installed separately
- can be operated through either the UI (user interface) or the CL (command line)
  - command line is useful if you want to automate the export process, or use APIs to integrate with another system

## Using the Data Export Service

Get Cloudy

- a high-tech consulting firm that specializes in CRM implementations.
- financial analyst, Charnice, knows that data loss can have a serious financial impact on the business
- sets up meeting with Salesforce admin, Chinua, to discuss backups
- Chinua explains that he automates weekly backups with the Data Export Service

### Follow These Steps to Export Data Using the Data Export Service

1. From Setup, enter Data Export in the Quick Find box, then select `Data Export` and `Export Now` or `Schedule Export`.
    - The `Export Now` option prepares your files for export immediately. This option is only available if enough time has passed since your last export.
    - The `Schedule Export` option allows you to schedule the export process for weekly or monthly intervals.
2. Select the desired encoding for your export file.
3. If you want images, documents, attachments, and so on included in your data, select the appropriate options.
4. Select Replace carriage returns with spaces to have spaces instead of carriage returns or line breaks in your export files. This is useful if you plan to use your export files for importing or other integrations.
5. If you're scheduling your export, select the frequency (only available for organizations with monthly exports), start and end dates, and time of day for your scheduled export.
6. Under Exported Data, select the types of data to include in your export. We recommend that you select `Include all data` if you’re not familiar with the terminology used for some of the types of data.
7. Click `Start Export` or `Save`. Salesforce creates a zip archive of CSV files and emails you when it's ready. Exports will complete as soon as possible, however we can't guarantee the date and time the export will complete. Large exports are broken up into multiple files. Follow the link in the email or click `Data Export` to download the zip file. Zip files are deleted 48 hours after the email is sent.

## Resources

- [Data Loader Overview](https://help.salesforce.com/HTViewHelpDoc?id=data_loader.htm&language=en_US)
- [Installing Data Loader](https://help.salesforce.com/apex/HTViewHelpDoc?id=installing_the_data_loader.htm&language=en_US)
- [Exporting Data using the Data Loader](https://help.salesforce.com/HTViewHelpDoc?id=exporting_data.htm&language=en_US)
- [Explore how to export data more effectively in Salesforce](http://pages.mail.salesforce.com/achievemore/managedata/?utm_source=trailhead&utm_medium=resources&utm_campaign=datamanagement&utm_content=exportdata)
- [Best Practice Hub: Improve Data Quality](http://pages.mail.salesforce.com/page.aspx?QS=3935619f7de112ef3fdd44cfb3dcb15df8ef83257379ba31&utm_source=trailhead&utm_medium=resources&utm_campaign=072016)
