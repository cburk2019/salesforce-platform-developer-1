# Extend the Salesforce Platform

6:09pm

## Learning Objectives

- List the Salesforce APIs.
- Explain how Heroku and Salesforce are related.
- Identify ways Salesforce interacts with IoT and bots.

## Get to Know the Lightning Platform APIs

Earlier, declarative development in Salesforce using tolls such as Lightning App Builder and Process Builder. These tools require very little interaction with Salesforce's underlying APIs.

As you move into more programmatic development, you will find a robust set of APIs that let you access your Salesforce data in a variety of ways.

In the previous section, [Code with Salesforce Languages](/Developer-Beginner/Platform-Development-Basics/Code-with-Salesforce-Languages/work.md), we saw the API in action when we looked at Lightning components, Apex, and Visualforce.

Simply put, every object in an org, has an API name that lets you access data for the object. Let's look at the SOQL (Salesforce Object Query Language) query from the last unit:

`Property__c property = [SELECT Name, Price__c from Property__c WHERE Id=:propId];`

The `__c` denotes that the object is a custom object or field. This query us using the automatically created API access point for the Property object to retrieve the info about different properties in your org.

Below is a list of APIs that Salesforce provides and what they're used for:

- SOAP API - Integrate your org's data with other applications using standard [SOAP](https://www.tutorialspoint.com/soap/soap_quick_guide.htm) protocols.
- REST API - Access objects in your org using standard [REST](https://www.codecademy.com/article/what-is-rest) protocols.
- Metadata API - Manage customizations in your org and build tools that manage your metadata model.
- Tooling API - Build custom development tools for platform applications.
- Marketing Cloud API - Expose Marketing Cloud capabilities with the REST API and get comprehensive access to most email functionality with the SOAP API.
- Bulk API - Load, delete, and perform asynchronous queries on large data sets.
- Streaming API - Send and receive notifications securely and efficiently. Notifications can reflect data changes in your org, or custom events.
- Connect REST API - Build UI for Commerce, CMS-Managed Content, Experience Cloud Sites, Notifications, Topics, and more.
- Mobile SDK - While it's technically a software development kit, it's worth including here. Integrate Native or Hybrid mobile apps directly with Salesforce.

## Unleash Your Apps with Heroku

APIs can be used with Salesforce and external systems.

Heroku is all about interacting with the outside world. Quickly build, deploy, and scale web apps. One huge advantage of Heroku is it flexible in accepting Java, JavaScript, Python, PHP, etc.

Heroku is built on AWS (Amazon Web Services) which leads to infrastructure concerns are taken care of for you in app development. Heroku Connect unifies Salesforce data with your Heroku Postgres data, so you don't have to manage moving info across platforms. Which ultimately means more time to focus on new development.

## IoT, Bots, and More

There are ways to flex my development skills and have some fun with the platform 🕺

### IoT

Depending on industry, integrating Salesforce with the Internet of Things (IoT) may or may not be necessary. But, with smart devices on the rise, it's a good idea t get familiar with developing with IoT in mind.

Example, real estate agent prepares to show house. Must unlock the door, turn on lights, set temp. What if agent could do this on the Salesforce mobile app? By connecting smart devices with Salesforce, they can! With a combination of Visualforce/Lightning components, microservices hosted on Heroku, and the IoT interfaces from smart locks, lights, and thermostats, you can build IoT control right on the Salesforce platform.

Connected hardware give an easy way to collect, manage, and analyze data about devices through Salesforce's IoT capabilities. Also helps to do things like monitor performance status of customer's devices and define business logic that supports customer engagement.

### Bots

- Chatbots - used in external customer service. Expedia for example. BUT, you can also build chatbots in your SF org to help employees navigate data.

- DreamBot - At bottom of DreamHouse app, search for 3 bedrooms in Boston, returns results in "chat"
  - DreamBot is coded entirely in Apex.

### And More!

You can use Apex and Einstein Vision API to create custom image recognition and classification engines. Saved 4 projects you can build in the Trailhead.

## Sum It All Up

Salesforce platform can be used to develop quickly with no-code or low-code.

Programmatic pillars of the Salesforce platform:

- Lightning components
- Apex
- Visualforce

One thing to take away is that the platform is extremely dynamic. Accelerated development capabilities and the many technologies that integrate with Salesforce, there are a LOT of options for building out a Salesforce org.