# Salesforce -> Developer Beginner -> Salesforce Mobile App Customization -> Create Object-Specific Quick Actions

## Learning Objectives

- Create an object-specific action.
- Add an action to an object’s page layout.
- Test an object-specific action in the Salesforce mobile app.

## Quick Actions: The Sequel

At this point, you can feel pretty proud of your mobile customization skills. You’re an expert at creating global actions, and you’re ready to face your next challenge: `object-specific actions`. Never fear—the process of creating an object-specific action is very similar to creating a global action, so this unit will be a breeze.

## Object-Specific Actions in the Salesforce Mobile App

To kick off our discussion of object-specific actions, let’s talk about what makes them different than global actions.

- ***`Object-specific actions can update records.`***
- Object-specific actions can create records that are automatically associated with related information. For example, a user could initiate an action that simultaneously creates a contact and associates it with an account.

There’s one more big difference. To expose object-specific actions in the mobile app, you don’t add them to the global publisher layout like we did in the last unit. Instead, you make them available to users by editing the object’s page layout. You’ll see all these differences in action—pun intended!—as you walk through the steps in this unit.

Let’s check out D’Angelo’s use case for object-specific actions so we can start building some cool stuff.

## The DreamHouse Scenario

When D’Angelo did his ride-alongs with a few DreamHouse Realty brokers, he noticed they spent a lot of time showing properties to prospective buyers and managing their schedule. He wants to give the brokers a fast way to schedule a new showing in the Salesforce mobile app, so he’ll create an action that will appear on the contact detail page.

![A broker who is looking at her phone while standing in front of a For Sale sign](/assets/broker-for-sale.png)

## Lay the Groundwork

To simulate the DreamHouse use case, you need to build a few things in your own org first. Now, now...no grumbling. We promise it’ll be worth it. You’ll get to witness the power of object-specific actions in a real-world scenario, plus you can practice your wicked platform-building skills.

### **`Create the Property Custom Object`**

It would be hard for brokers to schedule a new showing without being able to associate it with a specific property. How would they know which home to show? So let’s create a custom object called Property.

If you created the Property object in your org when you earned the Data Modeling badge on Trailhead, you can skip this step, but you'll need to make sure that the Allow Activities option is selected.

1. From the Object Manager, select `Create` | `Custom Object`.
2. In the Label field, enter `Property`.
3. In the Plural Label field, enter `Properties`.

    ![A screenshot of the custom object's details](/assets/custom-object-details-example.png)

4. In the Optional Features section, select `Allow Activities`.
5. Click `Save`.

Now we’ll create a custom tab for the Property object.

1. Enter `Tab` in the Quick Find box, then select `Tabs`.
2. In the Custom Object Tabs list, click `New`.
3. In the Object dropdown list, select `Property`.
4. For the Tab Style, select `Real Estate Sign`.
5. Click `Next`. Accept the defaults, then click `Next` again.
6. Click `Save`.

### **`Customize the Event Object for Showings`**

You’re a savvy admin, so you probably guessed that a showing is a type of event. But D’Angelo doesn’t want to use standard events for showings because users need to enter extra information about them, like the related property and the buyer’s feedback.

The best way to handle this customization challenge is with a new event record type that has its own page layout. Let’s create a page layout specifically for showings, then create an event record type and link it to the new page layout.

1. From the Object Manager, enter `Event` in the Quick Find box, then select `Event`.
2. From the Event object management settings, go to Page Layouts and click `New`.
3. Select `Event Layout` from the Existing Page Layout dropdown list.
4. In the Page Layout Name field, enter `Showing Layout`.

    ![A screenshot of the new page layout's details](/assets/new-page-layout.png)

5. Click `Save`.
6. From the Event object management settings, go to Record Types and click `New`.
7. Enter `Showing` in both the Record Type Label and Record Type Name fields.

    ![A screenshot of the new record type's details](/assets/new-record-type-details.png)

8. Click `Next`.
9. Select `Showing Layout` in the Apply one layout to all profiles dropdown list.

    ![A screenshot of the page layout assignment for the new record type ](/assets/new-layout-assignment.png)

    - This layout only applies to the Showing record type. The standard event record type continues to use the Event Layout.

10. Click `Save`.

### **`Create a Lookup Field for Showings`**

Hang in there! This is the last step. We just need to create a custom Property field so brokers can associate showings with properties. We do that with a lookup from the activities object to the property object.

1. From the Object Manager, enter `Activity` in the Quick Find box, then select `Activity`.
2. From the Activity object management settings, go to Fields and Relationships and click `New`.
3. Select `Lookup Relationship`, then click `Next`.
4. In the Related To dropdown list, select `Property`, then click `Next`.
5. Enter `Property` in the Field Name and Field Label fields, then click `Next`.
6. Select the `Visible` checkbox so the field is available to all profiles, then click `Next`.
7. Deselect the Event Layout and Task Layout. We only want this field to appear on the Showing Layout.

    ![A screenshot of the Showing Layout as the only selected layout for the new field](/assets/showing-layout.png)

8. Click `Next`.
9. Enter Showings in the Related List Label field.

    ![A screenshot of the related list label for the Property field](/assets/related-list-label.png)

10. Click `Save`.

## Create an Object-Specific Action

Whew, you made it through your homework assignment. Now that all the pieces are in place, you can enjoy your reward—helping D’Angelo create an awesome `object-specific action`.

Here’s what we need to do. D’Angelo wants to create a `New Showing` quick action and make it available on the `contact detail page` in the Salesforce mobile app. That way, when a broker schedules a new showing, it’s automatically associated with the record for the prospective buyer. So in this step, we `create an object-specific action for contacts`.

1. From the Object Manager, enter `Contact` in the Quick Find box, then select `Contact`.
2. From the Contact object management settings, go to Buttons, Links, and Actions and click `New Action`.
3. Verify that the action type is `Create a Record`. Actions can do more than just create records. To learn more about the other options, read the [Object-Specific Actions](https://help.salesforce.com/articleView?id=actions_overview_object_specific.htm&language=en_US) article in Salesforce Help.
4. In the Target Object dropdown list, select `Event`.
5. In the Record Type dropdown, click `Showing`.
6. Enter `New Showing` in the Label field.

    ![A screenshot of the new action's details](/assets/new-action-details-example-2.png)

7. Click `Save`.
8. In the layout editor, remove the following fields:
    - Related To
    - Assigned To
    - and Name

9. Add the Property field to the layout and make it required. You can double-click the field to edit its settings.
10. Remove any extra spaces and arrange the fields in a single column.

    ![A screenshot of the new action's layout with 5 fields in a single column](/assets/new-action-with-5-fields.png)

11. Click `Save`.
12. Click `Yes` to acknowledge the warning. Even though it’s required, it’s fine to remove the Assigned To field from the layout because it defaults to the current user.
    - Note
        - Don’t remove a required field from the layout unless:
            - The field has a default value.
            - You specify a predefined field value for the action.
            - The field already contains data. For example, if the action updates a record, the user entered the required information when they initially created the record.

13. Now let’s save the brokers some time by prepopulating the Subject field. In the Predefined Values related list, click `New`.
14. In the Field Name dropdown list, select `Subject`.
15. In the Specify New Field Value field, enter "`Showing"`. Be sure to put the quotation marks around the word.

    ![A screenshot of the predefined value for the Subject field](/assets/predefined-value-subject-field.png)

16. Click `Save`.

## Add an Action to an Object’s Page Layout

We’re in the home stretch! Now we just need to add the new action to the page layout for contacts. Then it will be available in the action bar in the mobile app when a broker is viewing a prospective buyer’s record. (Don’t forget—when you create an object-specific action, it belongs on the page layout for that object.)

1. From the Object Manager, enter `Contact` in the Quick Find box, then select `Contact`.
2. From the Contact object management settings, go to Page Layouts and click `Contact Layout`.
3. In the Salesforce Mobile and Lightning Experience Actions, if you see a link to `override the predefined actions`, click the link to override.
4. Select `Mobile & Lightning Actions` in the palette, then drag the New Showing quick action into the mobile section. Make sure it’s the first item.

    ![A screenshot of the New Showing action in the Salesforce1 section of the contact page layout](/assets/new-showing-action-example.png)

5. Reorganize the actions so the most frequently used ones are first, and remove any unnecessary actions.

    ![A screenshot of the reorganized actions in the Salesforce1 section of the contact page layout](/assets/reorganized-actions.png)

6. Click `Save`.

And we’re done! Now DreamHouse brokers can quickly schedule a new showing with a prospective buyer.

## Test the Action in the Salesforce Mobile App

### *** ***THE APP IS CRASHING WHEN I TRY THIS STEP - Sat, Mar 19, 11:34pm PDT*** ***

Here comes the really satisfying part—it’s time to test your beautiful new action in the mobile app. So fire up Salesforce on your device, and let’s walk through this use case together.

1. Tap the `Navigation Menu Icon` to open the navigation menu. If you’re already in the Sales Lightning app, pull down to refresh the navigation menu. If you’re not in the Sales Lightning app, tap `App Launcher`, then tap the `Sales Lightning` app to open it.
2. Let’s first create a new property so we can associate it with a showing. In the navigation menu, tap `Properties`. If you don’t see Properties in the navigation menu, tap `All Items` to find it in alphabetical order.
3. Tap `New`.
4. For the property name, enter a street address.

    ![A screenshot of the property detail page in the Salesforce mobile app](/assets/mobile-app-property-detail-page.png)

5. Fill out other required fields, if any, then tap Save. Now we can look up a prospective buyer and schedule a showing with them.
6. Open the navigation menu, then tap Contacts.
7. Select the contact you created in the previous unit, or create a new one.
8. Pull down to refresh the action bar.
9. Tap New Showing.

    ![The New Showing action in the Salesforce mobile app action bar](/assets/new-showing-button.png)

10. Complete the fields.

    ![Details about the new showing](/assets/new-showing-details.png)

    - Tip
      - Dictation is much faster than typing. When you get to the Description field, activate voice input by selecting the Microphone icon on the keyboard. This native OS feature can be a real time-saver for busy mobile users, so be sure to tell them about it.

11. Tap `Save`.
12. Let’s go back to the Property record so you can see that the new event appears in the Showings related list. Open the navigation menu, tap `Properties`, then select the property you just created.
13. Tap `Related`.
14. Tap `Showings` to see all the showings scheduled for that property.

Pretty cool, huh? You’re really getting the hang of this mobile stuff. (Feel free to pat yourself on the back...you deserve it.)

After racking up your points, head over to the next unit where you learn how to streamline your record detail pages in the Salesforce mobile app using compact layouts.

## Resources

- Salesforce Help: [Quick Actions](https://help.salesforce.com/HTViewHelpDoc?id=actions_overview.htm&language=en_US)
- Salesforce Help: [Object-Specific Actions](https://help.salesforce.com/HTViewHelpDoc?id=actions_overview_object_specific.htm&language=en_US)
