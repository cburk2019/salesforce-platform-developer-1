# Salesforce -> Developer Beginner -> Salesforce Mobile App Customization -> Create Global Quick Actions

## Learning Objectives

- Describe the differences between the two main types of actions.
- Create a global action.
- Configure fields in an action layout.
- Set a predefined value for a field on an action layout.
- Add an action to the Salesforce mobile app by editing the global publisher layout.

## Introducing Quick Actions

Quick actions are the first stop on our tour of mobile customization options. And we’re really putting our best foot forward here.

Because with quick actions, we’ve given you the keys to the mobile kingdom. No kidding! It’s a bold statement, but it’s true. Of all the point-and-click customization tools at your disposal, quick actions have the most potential to transform the mobile experience and make you a hero to your users.

## The Beauty of Quick Actions

So what are `quick actions`? Well, you can think of them as `shortcuts`. They offer a fast way for mobile users to launch a specific workflow in the Salesforce mobile app, like:

- creating records
- logging calls
- or sharing files

The Salesforce mobile app comes with some handy built-in actions, and they live in the action bar and action menu ( Action Menu icon) at the top of the screen. The action bar is visible on most pages, so quick actions are just one tap away for your mobile users.

![The action bar and actions menu in the Salesforce mobile app](/Developer-Beginner/Salesforce-Mobile-App-Customization/Create-Global-Quick-Actions/assets/mobile-action-bar.png)

Pretty convenient, eh? But wait—there’s more!

To call the quick action a mere shortcut doesn’t really do it justice. Here’s why quick actions are so special.

- You can create custom actions tailored to your own business processes and use cases.
- Each action has its own unique page layout, so you can limit the fields to just the ones mobile users truly need.
- You can prepopulate fields on the page layout to save mobile users some time.

See? Quick actions are more than meets the eye. They’re actually three powerful features — a shortcut plus a page layout plus predefined fields — rolled into one small, mighty package.

## The Types of Quick Actions

Now that you understand what actions are, we’re going to throw a curveball at you. There are two types of actions:

- global
- object-specific

Object-specific actions let users create or update records in the context of a particular object. In the Salesforce mobile app, object-specific actions show up on record detail pages. So for example, an action associated with the opportunity object is only available when a user is looking at an opportunity.

Global actions let users create records, but the new record has no relationship with other records. And they’re called *`global actions`* because they can be put anywhere actions are supported—on record detail pages, but also places like the feed or Chatter groups.

Clear as mud? Don’t worry, you’ll feel more comfortable with both kinds of actions after creating a few yourself. We tackle global actions first.

## Our Use Case for Global Actions

Here’s a way to think about global actions:

- They’re things that users want to do quickly, but not necessarily completely. And that’s exactly how D’Angelo Cunningham will use global actions to make his brokers’ lives a little easier. Let’s look at DreamHouse Realty’s first mobile use case.

DreamHouse Realty uses the *contact object* to keep track of their prospective home buyers. Imagine that one of the DreamHouse brokers is out hosting an open house, and she meets a prospective buyer. She needs an efficient way to add the person as a contact without navigating to a specific page or associating the person with other information. That’s what a global action is for—quick things that users can follow up with later.

## Bring the Use Case to Life

D’Angelo wants to customize the Salesforce mobile app to make the process of adding prospective buyers as fast and easy as possible. He decides to:

- Create a ***New Prospect*** global action to collect new potential buyers’ contact info.
- Limit the fields on the layout to just the essentials, like name, number, and email.
- Include a custom `Stage` field to indicate the buyer’s current stage in the home purchasing process, and set the default value of the field to “Prospect”.

To follow along with D’Angelo as he whips up a new global action, first we need to create the custom Stage field in our org, too.

1. Go to Setup. In the Object Manager, enter `Contact` in the Quick Find box, then select `Contact`.
2. Go to Fields and Relationships and click `New`.
3. Select `Picklist` as the data type, then click `Next`.
4. For Field Label, enter `Stage`.
5. Select `Enter values for the picklist, with each value separated by a new line`.
6. In the text area, enter the following values:
    - Prospect
    - Showing
    - Offer
    - Closing
    - Archive

    ![A screesnhot of the Stage field's details](/Developer-Beginner/Salesforce-Mobile-App-Customization/Create-Global-Quick-Actions/assets/stage-field-details.png)

7. Click `Next`.
8. Select `Visible` so the field is available to all profiles, then click `Next`.
9. Click `Save`.

## Create a Global Action

Now that we’re on the same page as D’Angelo, we’re ready to get started. In this step, we add a `global action` that creates a `new contact`.

- [Walk Through It: Create a Global Quick Action](https://login.salesforce.com/services/walkthrough?path=/p/setup/link/ActionButtonLinkList%3FpageName=Global&type=Global&setupid=GlobalActionLinks&tour=create-global-publisher-action)

1. From Setup, enter `Actions` in the Quick Find box, then select `Global Actions`.
2. Click `New Action`.
3. We want this action to create a new contact, so make sure the action type is `Create a Record`. Actions can execute other processes, too, like logging calls or sending email. ***But be aware that global actions can’t update a record. Only object-specific actions can do that.***
4. In the Target Object dropdown list, select `Contact`.
5. In the Label field, enter `New Prospect`.

    ![A screenshot of the new action's details](/Developer-Beginner/Salesforce-Mobile-App-Customization/Create-Global-Quick-Actions/assets/new-action-details-example.png)

6. Click `Save`.

## Customize the Action Layout

The most powerful thing about quick actions is that each action comes with its own unique layout that you can customize. That’s why it’s such a time-saving feature for mobile users; you can pare down to the essentials and remove as many unnecessary fields as possible.

Let’s optimize the layout for the New Prospect action. D’Angelo wants to eliminate a few fields and make sure the custom Stage field gets added to the layout.

1. If the layout editor isn’t already open, go to the Global Actions list, then click `Layout` next to the New Prospect action.
2. Remove the Account Name and Title fields from the layout.
3. Add the Stage field to the layout.

    ![A screenshot of the fields on the action layout](/Developer-Beginner/Salesforce-Mobile-App-Customization/Create-Global-Quick-Actions/assets/action-layout-fields-example.png)

    - Tip When customizing action layouts for mobile users, less is more. A best practice is to include fewer than five fields, and definitely no more than eight.

4. Click `Save`.

## Set Predefined Values

A great way to speed up the process of data entry for your mobile users is to prepopulate values for certain fields on an action layout.

That’s not always possible depending on your use case, but D’Angelo can definitely take advantage of this feature. If you recall, he wants to set the default value of the Stage field to “Prospect.”

1. Go to the Global Actions list and click `New Prospect`.
2. In the Predefined Field Values related list, click `New`.

    ![A screenshot of the New button in the Predefined Field Values list](/Developer-Beginner/Salesforce-Mobile-App-Customization/Create-Global-Quick-Actions/assets/predefined-list-new-button.png)

3. In the Field Name dropdown list, select `Stage`.
4. In the Specify New Field Value section, select `Prospect`.

    ![A screenshot of the predefined value for the Stage field](/Developer-Beginner/Salesforce-Mobile-App-Customization/Create-Global-Quick-Actions/assets/predefined-field-value-example.png)

5. Click `Save`.

## Add an Action to the Global Publisher Layout

OK! We have a spiffy new action with a mobile-friendly layout. But there’s one final step to complete. The action won’t be available in the Salesforce mobile app until we add it to the ***`global publisher layout`***.

***`Global publisher layout`*** - that’s a mouthful, isn’t it? Well, it’s just the technical way of referring to the way actions are listed in the action bar in the mobile app. The global layout only applies to the action bar in places like the feed or Chatter groups—basically, only on pages that aren’t related to a specific object.

D’Angelo wants the brokers to be able to create a new prospect directly from the feed, so let’s add our new action to the global publisher layout.

1. From Setup, enter `Publisher` in the Quick Find box, then select `Publisher Layouts`.
2. Click `Edit` next to Global Layout.
3. In the Salesforce Mobile and Lightning Experience Actions section, if you see a link to `override the predefined actions`, click the link to override.

    ![A screenshot of the Override Predefined Actions link in the Publisher](/Developer-Beginner/Salesforce-Mobile-App-Customization/Create-Global-Quick-Actions/assets/override-predefined-actions.png)

4. Select `Mobile & Lightning Actions` in the upper palette of the layout editor, then drag the New Prospect quick action into the mobile section. Make sure it’s the first item.

    ![A screenshot of the New Prospect action in the Global Publisher Layout](/Developer-Beginner/Salesforce-Mobile-App-Customization/Create-Global-Quick-Actions/assets/global-publisher-layout-new-prospect-action.png)

    - The order of the actions here determines their order in the mobile app. Reorganize them so the most frequently used actions are first, and remove any unused actions.

5. Click `Save`.

## Test the Global Action in the Salesforce Mobile App

Congratulations! You successfully created your first global action. Why don’t we launch the Salesforce mobile app and take the action for a test drive?

1. Open Salesforce on your mobile device.
2. Tap the `Navigation Menu Icon` to open the navigation menu, then pull down to refresh.
    - (Sometimes you need to refresh pages in the mobile app after making changes in Setup.)

3. Select `Chatter` in the menu to navigate to the feed.
4. Tap New Prospect in the action bar.

    ![The New Prospect action in the Salesforce mobile app action bar](/Developer-Beginner/Salesforce-Mobile-App-Customization/Create-Global-Quick-Actions/assets/new-prospect-action-button.png)

5. Enter the required data. The Stage field should default to “Prospect.”

    ![A screenshot of the prospect's details in the Salesforce mobile app](/Developer-Beginner/Salesforce-Mobile-App-Customization/Create-Global-Quick-Actions/assets/new-prospects-details-example.png)

6. Tap Save.

High five! The new global action works as expected.

Now that you’ve mastered the global action, let’s turn our attention to object-specific actions. In the next unit, you help D’Angelo improve the Salesforce mobile app even more by implementing his second mobile use case.

## Resources

- Salesforce Help: [Global Quick Actions](https://help.salesforce.com/HTViewHelpDoc?id=actions_overview_global.htm&language=en_US)
- Salesforce Help: [Notes on Predefined Values for Quick Actions](https://help.salesforce.com/HTViewHelpDoc?id=predefined_field_values_notes.htm&language=en_US)
- Salesforce Help: [Assign Global Publisher Layouts to User Profiles](https://help.salesforce.com/HTViewHelpDoc?id=assigning_global_publisher_layouts_to_profiles.htm&language=en_US)
