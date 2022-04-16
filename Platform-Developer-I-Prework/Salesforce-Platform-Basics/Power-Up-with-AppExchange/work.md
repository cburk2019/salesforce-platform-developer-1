# Power Up with AppExchange

## Learning Objectives

- Develop your own AppExchange strategy.
- Install an app from AppExchange.

## What is AppExchange

The "enterprise ecosystem". Salesforce has a community of partners that use the flexibility of the Salesforce platform to build amazing apps and other solutions that anyone can use. These offerings are available (some for free, some at a cost) for installation on AppExchange.

![AppExchange pic](/Salesforce-Platform-Basics/Power-Up-with-AppExchange/assets/AppExchange.png)

## Strategies for Success

D’Angelo’s DreamHouse app is a raging success among the company real estate brokers. But if we’re being realistic, D’Angelo is only one guy. There are only so many hours in the day for him to develop new apps for his colleagues.

Luckily, AppExchange is full of apps D’Angelo can download to help DreamHouse manage everything from payroll to travel approval to integrations with other tools like Evernote and MailChimp.

The possibilities AppExchange offers are exciting, but before you start downloading every app in sight you need to develop a strategy. A solid AppExchange strategy helps ensure that you’re getting the highest value apps without duplicating functionality or investing in something that you don’t need.

Follow these steps to develop a good AppExchange strategy.

1) Identify departments that use or plan to use Salesforce. These are your primary stakeholders.
2) Research what’s available on AppExchange that best meets your stakeholder requirements. Discuss business cases with department heads to determine exact needs. Here are some good questions to ask:

        a. What business problem are you trying to solve?
        b. What are your main pain points right now?
        c. How many users need this app?
        d. What’s your budget?
        e. What’s your timeline?

        These questions help you identify apps that are the best fit for each department or business case.

3) When you find an app that you think meets your needs, download the app in a test environment (like a free Developer Edition or sandbox). Ensure that the app you’re installing doesn’t interfere with any other apps you’ve installed or customizations you’ve made. Sandboxes are copies of your organization in a separate environment. They’re used for development and testing. See Sandbox Overview.
4) If you’re choosing between multiple apps, take some time to evaluate what you’ve tested. Determine whether there are feature gaps or unwanted functionality. If necessary, invite your stakeholders to demo the apps and provide feedback.
5) You’re ready to go! You’ll install and deploy your app in your production environment. Make sure you keep your users in the loop about what’s changing, and provide training and documentation as necessary.

## Installing an App

Remember:

    While AppExchange resembles a traditional app store like you can find on your phone or tablet, it’s important to remember that your Salesforce org is a complicated environment. You can’t just install an app because it has a cool logo or a convincing catchphrase.

1) Click: "**Get It Now**"
    - Where do I install the app, production or sandbox?
      - In general, it's best practice to install in a sandbox  first. Testing will help avoid conflicts in production.
    - Should I give my app permissions to admins only, all users, or specific profiles?
        - Depends on who the app is for. If you want to limit access to a particular set of uses, plan to modify those user profiles ***BEFORE*** your install the app.

When apps are installed, the are installed as packages. To find the app/package:

- From Setup, search and select "Installed Packages" in the Quick Find box.
- Click the name of the package you installed. Same name as AppExchange name.
- Click ***View Components*** to see more info about the package. Including custom fields, custom objects, Apex classes, etc. This info can help to identify if you have any conflicts in your own customizations.

## Final Thoughts

As you start to explore AppExchange, be sure to check out free apps provided by Salesforce Labs. The great thing about Salesforce Labs apps, other than that they’re free, is that they’re open source. You can customize them as needed and peek under the hood to see how they work. It’s a great way to learn more about how the platform works.
