# Salesforce -> Developer Beginner -> Salesforce Mobile App Customization -> Customize Navigation

## Learning Objectives

- Explain how to customize your users’ navigation experience.
- Explain how to get to the Menu and the mobile App Launcher.

## Point Users in the Right Direction

If you’ve ever been to an airport, you’ve likely seen large signposts that help you get your bearings and find your way to certain locations, like baggage claim or a specific gate number.

Well, you need visual cues to find your way in apps, too. And that’s what the mobile navigation menu is: a signpost. Your users rely on it to get from place to place in the Salesforce mobile app as efficiently as possible.

With the mobile app, the navigation items that your users see depend on which Lightning app they’re actively using. And depending on which part they’re in, you can customize their navigation items in different ways.

So let’s talk about how you can customize navigation items to meet your users’ needs. Because, after all, a signpost is only effective if it points people to places they actually want to go.

## The Mobile Navigation Bar and Menu

Before we jump into the customization options, let’s get familiar with:

- the navigation bar
- the navigation menu

The thumb-friendly navigation bar lives at the bottom of your screen. It puts important navigation items in easy reach while users get work done. We’ll talk more about the navigation bar soon.

Go to the navigation menu by tapping `Menu`. This menu is where users can access all the objects, apps, and items available to them.

![Lightning App Builder navigation items with the mobile menu for comparison.](/assets/mobile-app-menu-comparison.png)

If you’ve enabled any Lightning apps for mobile, your users can switch between them with the App Launcher. The default navigation uses the first Lightning app listed. If you change the order of the Lightning apps in the App Launcher on desktop, or if your users can personalize the order themselves, those changes sync to the mobile App Launcher with a quick refresh.

When a Lightning app is enabled for desktop and phone, the navigation tabs on the desktop version of the app sync to the mobile navigation menu. Therefore, if a user has permission to change the tabs on the desktop version of a Lightning app, the user sees those changes in the mobile navigation menu.

If you customize the ordering of your navigation menu, make sure that the four most important items are at the top. These four items also conveniently appear in the navigation bar at the bottom of the screen unless your users switch to a Lightning app.

![Comparison showing that the navigation tabs on desktop match the navigation menu items on mobile.](/assets/mobile-app-navigation-example.png)

Users can also change the order of navigation items while they’re in the mobile app by tapping the `Edit` icon. Of course, if they use the app on desktop, they can see their changes there, too.

![Edit the order of navigation items menu.](/assets/navigation-items-order-menu.png)

## What You Can Change

For mobile navigation, you can change the items in the navigation menu of a Lightning app. These items mirror the tabs that are in the desktop version of the Lightning app. You—and your users, if they have the proper permissions—can change the order of the desktop tabs and see the changes in the mobile navigation menu. Users can also reorder the navigation items from the Salesforce mobile app. The first four items in the navigation menu are also the first four items in the navigation bar at the bottom of the screen.

## Notes About Mobile Navigation

As you customize the mobile navigation menu, here are some important things to keep in mind.

- You can’t set different menu configurations for different types of users. But users in Lightning apps with the correct permissions can change their navigation tabs, and those changes reflect in the Lightning app’s mobile navigation menu and navigation bar.
- If you want to include `Visualforce pages`, `Lightning Pages`, or `Lightning components` in your Lightning apps, you must create tabs for them.
- Before adding a page to the Salesforce mobile app, make sure the page is enabled for mobile. Thoroughly test your Visualforce pages in the Salesforce mobile app because they don’t always work the same as they do on desktop. See the resources section for more information.

## Customize the Navigation Menu

OK, enough preamble! Roll up your sleeves and get ready to help DreamHouse brokers zip around in the mobile app like seasoned pros.

D’Angelo wants to customize the navigation menu so that the most important items are at the top.

1. From Setup, enter `App Manager` in the Quick Find box, then select **`App Manager`**.
2. Click the arrow next to the Sales app (the developer name is `LightningSales`), then select `Edit`.
3. Click `App Options`.
4. Ensure that the app is enabled for mobile by verifying that the radio button for `Desktop and phone` is checked.
5. Click `Navigation Items`.
6. Rearrange the selected items using the arrows so that the top five are in the following order:
    1. Home
    2. Opportunities
    3. Contacts
    4. Tasks
    5. Dashboards. The first four items in the list become the first four icons in the navigation bar for your users on mobile, excluding Home that is only used for desktop.

    ![Navigation item list configuration.](/assets/navigation-item-list.png)

7. Click `Save`.

## Test Your Changes in the Salesforce Mobile App

You know the drill! Let’s see how the improved navigation menu looks in the mobile app.

1. Open Salesforce on your mobile device.
2. Tap `Salesforce mobile app menu icon` to open the navigation menu.
3. Make sure you’re on the Sales Lightning app that you edited by looking at the first app listed.
    - If you’re not on the correct app, tap App Launcher, then tap Sales to open the Sales app.

    ![Salesforce mobile app Lightning navigation screen with a red arrow pointed at the first listed app, Sales.]()

4. Pull down to refresh.

All of our minor adjustments reflect in the menu. And with that final piece of customization, we’ve completed our mobile mission! D’Angelo can confidently roll out the Salesforce app to the DreamHouse brokers, and soon they’ll be enjoying all the productivity gains that mobility has to offer.

## Next Steps

Well, that’s good news for D’Angelo. But what about your org? How do you translate your newfound knowledge into action? Now that you’re comfortable with the mobile customization tools, here’s what to do next.

1. Check out the [Salesforce Mobile App Rollout](https://trailhead.salesforce.com/trails/salesforce1_mgmt/modules/salesforce1_rollout) module. Start developing your mobile use cases and planning your mobile launch.
2. Read the [Salesforce Mobile App Security Guide](https://resources.docs.salesforce.com/sfdc/pdf/salesforce1_mobile_security.pdf) so you can make sure your company’s data is safe when accessed from mobile devices.
3. Roll out the Salesforce mobile app to your users.
4. Get your [Mobile Strategy Development badge](https://trailhead.salesforce.com/trails/salesforce1_mgmt/modules/mobile_strategy) to find out how Salesforce fits your company’s overall mobile strategy.

That’s enough mobile goodness to keep you busy for a while. Now go forth and implement your own awesome use cases in the Salesforce mobile app. Happy customizing!

## Resources

- [Salesforce Help: Customize a Lightning App Navigation Menu in the Salesforce Mobile App](https://help.salesforce.com/s/articleView?id=sf.salesforce_app_customize_lex_app.htm&type=5)
- [Salesforce Help: Personalize the Navigation Bar in Lightning Experience](https://help.salesforce.com/articleView?id=user_userdisplay_tabs_lex.htm&language=en_US)
