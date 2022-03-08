# Understand the Salesforce Architecture

## Learning Objectives

- Define key terms related to the Salesforce architecture.
- Find information related to trust.
- Explain at least one use case for Salesforce APIs.

## What is the Salesforce Architecture?

When you think about the Salesforce architecture, imagine a series of layers that sit on top of each other. Sometimes it helps to think of it as a cake because cake is delicious, and it makes everything better.

![salesforce architecture](/assets/salesforce-architecture.png)

### Salesforce Architecture

- Salesforce is a cloud company. Everything we offer resides in the trusted, multitenant cloud.
- The Salesforce platform is the foundation of our services. It’s powered by metadata and made up of different parts, like data services, artificial intelligence, and robust APIs for development.
- All our apps sit on top of the platform. Our prebuilt offerings like Sales Cloud and Marketing Cloud, along with apps you build using the platform, have consistent, powerful functionality.
- Everything is integrated. Our platform technologies like predictive analytics and the development framework are built into everything we offer and everything you build.

## Extra Important Terms to Understand

- trust
- multitenancy
- metadata
- API

### ***Trust***

[Salesforce's trust website -> vital resource.](https://trust.salesforce.com/en/) Can be used to view performance data and get more information about how we secure your data.

### ***Multitenancy***

![multitenancy apt building](/assets/multitenancy.png)

Multitenancy is a great word for making you sound smart at dinner parties, but really all it means is that you’re sharing resources. Salesforce provides a core set of services to all our customers in the multitenant cloud. No matter the size of your business, you get access to the same computing power, data storage, and core features.

Trust and multitenancy go hand in hand. Despite the fact that you’re sharing space with other companies, you can trust Salesforce to keep your data secure. You can also trust that you’re getting the latest and greatest features with automatic, seamless upgrades three times a year. Since Salesforce is a cloud service, you never have to install new features or worry about your hardware. All this is possible because of multitenancy.

### ***Metadata***

Data about data.

When we say data about data, we’re really talking about the structure of your Salesforce org.

Let’s think about an object like Property. When our friends at DreamHouse use Salesforce, they input and view data about properties. For example, a property can be located in Boston, cost $500,000, and have 3 bedrooms.

Now, imagine you stripped away all that specific data. What are you left with? You are left with the Property object along with all its fields, like address, price, and number of bedrooms. You can also have page layouts, security settings, and any other customizations you’ve made.

All of these standard and custom configurations, functionality, and code in your org are metadata. Part of the reason you can move so fast on the platform is that Salesforce knows how to store and serve you that metadata immediately after you create it.

### ***API***

Fundamentally, APIs allow different pieces of software to connect to each other and exchange information.

APIs are similar. Without knowing the details, you can connect your apps with other apps or software systems. The underlying technology takes care of the specifics of how information passes throughout the system.

Earlier, we talked about the database. When you add a custom object or field, the platform automatically creates an API name that serves as an access point between your org and the database. Salesforce uses that API name to retrieve the metadata and data you’re looking for.

For example, we can use a contact’s Name field in a bunch of places, like the Salesforce mobile app, a custom page, or even an email template. That’s all possible because of the API name.

![API example](/assets/API-example.png)
