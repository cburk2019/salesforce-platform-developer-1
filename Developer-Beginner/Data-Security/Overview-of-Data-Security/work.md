# Salesforce -> Developer Beginner -> Data Security -> Overview of Data Security

## Learning Objectives

- Explain the importance of giving the right people access to the right data.
- List the four levels at which you can control data access.
- Describe a typical scenario for limiting data access at each of the four levels.

## Introduction

Choosing the data set a group of users can see or have access to is a key decision that affects the security of your SF org or app. Giving thought to the kinds of things your users are doing and the data they need to do it.

### Example

Building a recruiting app to help manage open positions, candidates, and job applications.

You'll store confidential data such as:

- social security numbers
- salary amounts
- applicant reviews

Only some users should see this information.

Secure the data without making life harder for recruiters, hiring managers, interviewers, etc.

### Salesforce platform's flexible, layered sharing model

It's easy to assign different data sets to different sets of users. You can:

- balance security and convenience
- reduce the risk of stolen or misused data
- make sure all users can easily get the data they need

The platform makes it easy to specify which users can view, create, edit, or delete (CRUD) any record or field in the app.

You can control access to the whole org, a specific object, a specific field, or even an individual record. By combining security controls at different levels, you can provide the right level of data access to thousands of users without having to specify permissions for each user individually.

### Note

Although you can configure the security and sharing model entirely using the user interface, the model works at the API level. That means any permissions you specify apply even if you query or update the data via API calls. The security of your data is protected, regardless of how users get to it.

## Levels of Data Access

You can control which users have access to which data in your:

- whole org
- a specific object
- a specific field
- an individual record

### Organization

For the whole org:

- you can maintain a list of authorized users
- set password policies
- limit logins to certain hours and locations

### Objects

Access to object-level data is the simplest thing to control. You set permissions on particular types of objects / object. You can prevent a group of users from creating, viewing, editing, or deleting any records of that object.

For example:

- you can use object permissions to ensure that interviewers can view positions and job applications but not edit or delete them.
- you can use profiles to manage the objects that suers can access and the permissions they have for each object.
- you can use permission sets and permissions set groups to extend access and permissions without modifying users' profiles.

### Fields

You can restrict access to certain fields, even if a user has access to the object.

For example:

- you can make the salary field in a position object invisible to interviewers but visible to hiring managers and recruiters.

### Records

You can allow particular users to view an object, but then restrict the individual object records they're allowed to see. For example, an interviewer can see and edit her own reviews, but not the reviews of other interviewers. You can manage record-level access in these four ways.

#### `Organization-wide defaults`

Organization-wide defaults specify the default level of access users have to each others’ records. You use org-wide sharing settings to lock down your data to the most restrictive level, and then use the other record-level security and sharing tools to selectively give access to other users.

#### `Role hierarchies`

Role hierarchies give access for users higher in the hierarchy to all records owned by users below them in the hierarchy. Role hierarchies don’t have to match your organization chart exactly. Instead, each role in the hierarchy should represent a level of data access that a user or group of users needs.

#### `Sharing rules`

Sharing rules are automatic exceptions to organization-wide defaults for particular groups of users, so they can get to records they don’t own or can’t normally see. Sharing rules, like role hierarchies, are only used to give additional users access to records. They can’t be stricter than your organization-wide default settings.

#### `Manual sharing`

Manual sharing allows owners of particular records to share them with other users. Although manual sharing isn’t automated like org-wide sharing settings, role hierarchies, or sharing rules, it can be useful in some situations, such as when a recruiter going on vacation needs to temporarily assign ownership of a job application to someone else.

### Note

Make a table of the various types of users in your organization. In the table, specify the level of access to data that each type of user should have for each object and for fields and records within the object. You can then refer to this table as you set up your security model.

## Controlling Data Access with the Salesforce Platform

![access control](/assets/access-control.png)

## Audit System Use

Auditing provides important information for diagnosing potential security issues or dealing with real ones. Someone in your organization should audit regularly to detect potential abuse. Look for unexpected changes or patterns of use.

### `Record Modification Fields`

All objects include fields to store the name of the user who created the record and who last modified the record. This provides some basic auditing information.

### `Login History`

You can review a list of successful and failed login attempts for the past six months. For more information, see [Monitor Login History](https://help.salesforce.com/HTViewHelpDoc?id=users_login_history.htm&language=en_US).

### `Field History Tracking`

You can turn on auditing to automatically track changes in the values of individual fields. Although field-level auditing is available for all custom objects, only some standard objects allow it. For more information, see [Field History Tracking](https://help.salesforce.com/HTViewHelpDoc?id=tracking_field_history.htm&language=en_US).

### `Setup Audit Trail`

The Setup Audit Trail logs when modifications are made to your organization’s configuration. For more information, see [Monitor Setup Changes](https://help.salesforce.com/HTViewHelpDoc?id=admin_monitorsetup.htm&language=en_US).

## Resources

- [Security Implementation Guide](https://developer.salesforce.com/docs/atlas.en-us.224.0.securityImplGuide.meta/securityImplGuide/)
