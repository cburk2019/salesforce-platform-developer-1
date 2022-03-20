# Salesforce -> Developer Beginner -> Salesforce Mobile App Customization -> Get Started with the Salesforce Mobile App

## Learning Objectives

- Name some of the benefits of using the Salesforce mobile app.
- Explain why it’s important to customize the mobile app.
- Find and download the app.
- Choose your working environment for the app.

## Deliver on the Promise of Mobile

Unless you’ve been hiding under a rock, you’ve probably noticed that we’re in the midst of a mobile revolution. Mobile usage is at an all-time high—in fact, most of us spend as much time on our devices as we do in front of our computers. Mobile technology has transformed the way we live, learn, travel, shop, and stay connected.

And the enterprise world is no exception. People want their business tools to be mobile and easy to access. Your employees need to get work done when they’re on the go and away from their desks. (Heck, some employees don’t even have a desk—their desk is a car, a seat on an airplane, or the nearest coffee shop.)

But here’s the problem. Despite the pervasiveness of mobile technology, most companies haven’t been able to deliver on the promise of mobile. Why? Because it’s hard to build mobile apps. Do you build for Android or iOS? What tool do you use? How do you design for multiple screen sizes? What about security?

Luckily, you’ve got the Salesforce mobile app in your bag of admin tricks. We already took care of those pesky development challenges, which means you can reap the rewards of mobile without doing any of the dirty work. Sound good to you? We figured it might. So let’s learn more about the Salesforce mobile app.

## Welcome to the Salesforce Mobile App

The Salesforce mobile app is an enterprise-class app that provides your users with instant access to your company’s CRM data from a phone or tablet. Here are some of the reasons why the app is so awesome.

- **`The mobile app is included with every Salesforce license`**. Yup, you heard us correctly—it’s free. Procrastinating on your mobile rollout is basically like setting piles of money on fire.
- **`The app is plug-and-play`**, which means users just download it from the App Store® or Google Play™— and go. It works out of the box with no setup required. It’s lightning fast—seriously. In the time it took you to read this paragraph, you could have already installed the app and logged in.
- **`The app is cross platform`**, so it runs on Android and iOS operating systems. Like, automatically—without you having to do any development work.
- **`The app has offline capabilities`**. Your mobile users won’t be affected by capricious cellular signals, FAA regulations, subway commutes, or bunker-style buildings.
- **`It works seamlessly with the desktop version of Lightning Experience`**, so users can switch between the two without missing a beat.
- **`It isn’t just an app. It’s a platform`**. Because the mobile app is powered by the Salesforce platform, it’s infinitely customizable. You can use point-and-click tools to make it your own.

## The Magic of Metadata

Perhaps you’re wondering how it’s possible that the Salesforce mobile app works instantly, right out of the box. `The secret is your metadata`.

As an admin, you’ve probably used the point-and-click tools that help you customize Salesforce. Perhaps you’ve created custom objects, tailored page layouts, built list views, and so on.

Those customizations become part of your metadata, which is just a set of definitions that describe your particular Salesforce org. And most of your customizations are automatically available in the Salesforce mobile app because it reads those definitions and displays your data accordingly.

But wait a minute. If all of your Salesforce customizations are already available in the mobile app, then why bother customizing it?

## Mobile Is Different

Well, things that work in a desktop environment don’t always work as well in a mobile environment. Here’s an example. Let’s say you added a bunch of custom fields to the opportunity object, which means your opportunity page layout has over 100 fields.

That’s fine for a desktop user. But think about a sales rep editing an opportunity from their phone. They have spotty cellular coverage, so they have to wait a long time for an enormous page to load. Then to edit the three fields they actually want to update, they have to scroll...and scroll...and scroll...and scroll.

Yuck. That sounds frustrating, doesn’t it? But it doesn’t have to be that way. You can significantly improve the experience of mobile users by taking the time to tweak a few mobile-specific organization settings.

## Make the Mobile App Your Own

By customizing the Salesforce mobile app, you can mold it into a powerful tool that helps your users get work done fast. In this module, we cover three features you can use to customize the mobile app.

- Quick actions
- Compact layouts
- Mobile navigation, for Lightning apps and the Mobile Only app

When you’re new to the Salesforce mobile app, it can be challenging to figure out exactly how to use these features to solve problems for your mobile users. So let’s learn how to customize the mobile app in the context of a real-world scenario.

## Meet DreamHouse Realty

DreamHouse Realty is a thriving real estate business with 75 brokers. And those brokers are busy! They’re constantly on the go, whether they’re meeting with buyers, showing properties, or preparing for open houses.

D’Angelo Cunningham, the Salesforce admin for DreamHouse, heard about the Salesforce mobile app, and he thinks it can help the brokers stay productive when they’re out in the field.

![D'Angelo dreaming up mobile possibilities](/assets/deangelo-dream-mobile.png)

So D’Angelo did his homework. He talked to his brokers and did a few ride-alongs to find moments where the mobile app might be able to solve their problems or speed up certain processes.

After reviewing his notes, D’Angelo identified a handful of the most common tasks his brokers perform on a daily basis. Those tasks are called:

- `use cases`.

## Our Mobile Mission

So what are the mobile use cases D’Angelo identified? Here are the top three things his brokers need to accomplish quickly when they’re in the field.

- Adding a new prospective home buyer
- Scheduling a new showing
- Entering a prospective buyer’s feedback after a showing

Throughout this module, we follow along with D’Angelo as he translates those use cases into mobile customizations.

### Tip

Now is a good time to start thinking about your own mobile use cases. When you’re done with this module, head over to the [Salesforce Mobile App Rollout](https://trailhead.salesforce.com/trails/salesforce1_mgmt/modules/salesforce1_rollout) module. It’s full of advice about launching the Salesforce mobile app, and it includes instructions for developing mobile use cases.

## Get the Salesforce Mobile App

Ready to work side by side with D’Angelo as he customizes the Salesforce mobile app? Of course you are! So let’s get you up and running with the mobile app.

### Check the Requirements

Always run the mobile app on a device that meets minimum platform [requirements](https://help.salesforce.com/HTViewHelpDoc?id=sf1_requirements.htm&language=en_US) . Be aware that the requirements are subject to change.

### Download the App

If you have an Android or iOS device that meets the minimum requirements, you can use the downloadable Salesforce mobile app available from the App Store or Google Play.

### Choose Your Working Environment

When you log into the Salesforce mobile app, you’re automatically connected to your production org. But you can also log into your sandbox, which is the best place to play around with the mobile settings and customizations. If you don’t have a sandbox, log in with your Trailhead Playground (TP) org credentials, or get a free [Developer Edition](https://developer.salesforce.com/signup) account. (If you need your TP’s username and password, you can access them using the instructions [here](https://trailhead.salesforce.com/help?article=Find-the-username-and-password-for-your-Trailhead-Playground).)

### Understand the Limitations

The Salesforce mobile app does a lot, but it doesn’t do everything—be aware that there are some differences from the desktop Salesforce site. Make it a priority to learn about the [Salesforce features that aren’t in the Salesforce mobile app](https://help.salesforce.com/HTViewHelpDoc?id=limits_mobile_sf1_parent.htm&language=en_US), that have functional gaps, or that work differently in the mobile app.

## Embrace Your Mobile Future

Now that Salesforce is installed on your phone, pause for a moment and relish the fact that you’re taking the first step in your organization’s mobile journey. Exciting, isn’t it?

The Salesforce mobile app is the perfect place to start. It delivers a ton of value to your users right out of the box. And if you take advantage of the customization features explained in this module, you can save your users time and make their lives a lot easier. (Warning: They may cry tears of joy. Make sure you have tissues handy.)

An added bonus? With a successful mobile launch, it’s likely that you’ll see a boost in your overall Salesforce adoption. And we know the phrase `increased adoption` is like music to an admin’s ears.

So let’s get started! In the next unit, you learn how to set up quick actions in the Salesforce mobile app that help your users effortlessly accomplish important tasks when they’re on the road.

## Resources

- [Trailhead Module: Salesforce Mobile App Basics](https://trailhead.salesforce.com/modules/lex_salesforce1_basics)
- [Trailhead Module: Salesforce Mobile App Rollout](https://trailhead.salesforce.com/trails/salesforce1_mgmt/modules/salesforce1_rollout)
- [Salesforce Help: Landing Page for Salesforce Mobile App Documentation](https://help.salesforce.com/articleView?id=salesforce_app.htm&language=en_US)
