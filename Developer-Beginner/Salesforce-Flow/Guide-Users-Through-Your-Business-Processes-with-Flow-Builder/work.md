# Salesforce -> Developer Beginner -> Salesforce Flow -> Guide Users Through Your Business Processes with Flow Builder

## Learning Objectives

- Define a flow and list its key components.
- Describe the types of flow elements.
- Build a flow that creates a record and uploads files.

## Get Started with Flow Builder

You may have heard several terms used interchangeably when referring to flows. As a reminder, the official terms are:

- `Salesforce Flow` — t he product that encompasses building, managing, and running flows and processes.
- `Flow Builder` — a point-and-click tool for building flows.
- `Flow` — an application that automates a business process by collecting data and doing something in your Salesforce org or an external system.

In short, the Salesforce Flow product includes a couple of tools. One of them, Flow Builder, lets you create flows.

## Flow Building Blocks

Every flow is made up of three building blocks.

- Elements
- connectors
- resources in a flow

![Elements, connectors, and resources in a flow](/assets/flow-building-blocks.png)

- `Elements (1)` appear on the canvas. To add an element to the canvas, click `Add Element` where you want it to go.
- `Connectors (2)` define the path that the flow takes at run time. They tell the flow which element to execute next.
- `Resources (3)` are containers that represent a given value, such as field values or formulas. You can reference resources throughout your flow. For example, look up an account’s ID, store that ID in a variable, and later reference that ID to update the account.

Flow elements fit into four different categories.

### `Screen`

Display data to your users or collect information from them with Screen elements. You can add simple fields to your screens, like input fields and radio buttons as well as out-of-the-box Lightning components like File Upload.

![A flow screen that's built with out-of-the-box fields and components](/assets/flow-screen-out-of-the-box.png)

If you need more out of your flow screens, like custom navigation or information displayed in table format, build or install custom Lightning components.

![A flow screen built with custom components. YES](/assets/flow-screen-custom-components-yes.png)

![A flow screen built with custom components. NO](/assets/flow-screen-custom-components-no.png)

### `Logic`

Control the flow of... well, your flow.

- Create branches
- update data
- loop over sets of data
- wait for a particular time

### `Actions`

Do something in Salesforce when you have the necessary information (perhaps collected from the user via a screen).

Flows can:

- look up
- create
- update
- delete Salesforce records.

They can also:

- create Chatter posts
- submit records for approval
- send emails.

If your action isn’t possible out of the box, call `Apex code from the flow`.

### `Integrations`

Connect your flow to an external database by using:

- core actions
- Apex actions

Core actions let you make requests without going through the Salesforce server. Flow Builder also has a couple of tie-ins to platform events. Publish platform event messages with a Create Records element. Subscribe to platform events with a Pause element.

## Take a Tour

When you build flows, you work from `Flow Builder`.

![Screenshot of Flow Builder's user interface with numbers pointing at the toolbox, canvas, and button bar](/assets/flow-builder-diagram.png)

### **`Toolbox (1)`**

The toolbox contains the elements and resources you use to build your flow. From the Manager tab, create resources, such as variables, stages, and choices, to use in your flow. Or view a list of all elements and resources that you’ve added to the flow.

### **`Canvas (2)`**

The canvas is the working area, where you build a flow by adding elements. As you add elements to the canvas and connect them together, you see a visual diagram of your flow.

### **`Button Bar (3)`**

The button bar provides information about the flow, such as:

- Whether the flow is active or not.
- How long ago the flow was saved.
- Whether the flow has any warnings or errors. To see the warnings or errors, click the respective icon.

#### `Keyboard Shortcuts`

Use these handy keyboard shortcuts to quickly navigate your flow. In Windows...

- To **zoom in**, press `CTRL + =`.
- To **zoom out**, press `CTRL + -`.
- To **zoom to fit**, press `CTRL + Alt + 1`.
- To **zoom to view**, press `CTRL + Alt + 0`.

For Mac...

- To **zoom in**, press `Command + =`.
- To **zoom out**, press `Command + -`.
- To **zoom to fit**, press `Command + Option + 1`.
- To **zoom to view**, press `Command + Option + 0`.

## Build a Flow

Depending on your page layouts, objects can have lots of fields, which can overwhelm users who just want to create a record quickly. Let’s build a flow to streamline account creation. When it runs, our flow collects user input about a new account, creates an account record, and lets the user upload files to the account record.

### `Note`

Plan out your business process before you try to automate it. Doing so makes it easier to configure when you use one of our automation tools.

From Setup, enter Flows in the Quick Find box, then select `Flows`, click `New Flow`, then select `Screen Flow` and click `Create`.

## Add a Screen to Collect User Input

1. From the canvas, click `Add Element` `+`.
2. Click `Screen`.
3. In the Label field, enter `New Account`.
4. In Components, click `Text`.
5. Select the first Text screen component and enter Account Name in the Label field. Select the `Require` checkbox.
6. In Components, click `Phone`.
7. Select the Phone Number screen component. Enter Phone Number in the Label field and Phone_Number in the API Name field.
8. Select the footer under the screen components. On the right, expand `Configure Footer`. Under Previous Button, select `Hide Previous`. Under Pause Button, select `Hide Pause`.

    ![Screenshot of the Screen Components screen](/assets/screen-components-screen.png)

9. Click `Done`.

## Add a Create Records Element to Create Records

The Create Records element uses the values from New Account to create an account record.

1. After the New Account element, click `Add Element || +`.
2. Click `Create Records`.
3. For Label, enter *Create Account*.
4. For How to Set the Record Fields, select `Use separate resources, and literal values`.
5. In Create a Record of This Object, in Object, select `Account`.
6. In Field, select `Name`.
7. In Value, under SCREEN COMPONENTS select `Account_Name`.
8. Click `Add Field`.
9. In Field, select Phone.
10. In Value, under SCREEN COMPONENTS select `Phone_Number`, then click `Value`. Make sure that your Create Records element looks like this.

    ![Screenshot of the New Create Records screen](/assets/new-create-records-screen.png)

11. Click `Done`.

## Create the Screen That Enables File Uploads

The second screen element lets users upload files for the account that they created.

1. After the Create Account element, click `Add Element` and add another `Screen` element onto the canvas.
2. In Screen Properties, configure these settings.
    - Name the screen Upload Files in the Label field.
    - On the right, expand Configure Footer. Under Previous Button, select Hide Previous. Under Pause Button, select Hide Pause. If you don't make that selection, users will be able to navigate back to the first screen and multiple accounts could accidentally be created.

3. On the left in Screen Components, click File Upload.
    - For API Name, enter accountFiles.
    - For File Upload Label, enter Upload Related Files.
    - For Allow Multiple Files, select $GlobalConstant.True.
    - For Related Record ID, under VARIABLES select AccountId from Create_Account. The resulting value should be {!Create_Account}.

    ![The field settings for the file upload component field](/assets/file-upload-field-settings.png)

4. Click `Done`.
5. Save the flow. In Flow Label, enter Quick Account.
6. Click `Save`.

As configured, this File Upload component lets users upload more than one file at a time to the created account.

## Distribute Your Flow

Now it's time to distribute our flow to the right users. To do so, we `add it to the Home page`.
To learn about more ways to distribute a flow, check out the ***`Screen Flow Distribution`*** module.

## Activate Your Flow

Only active flows are available in the Lightning App Builder, so first activate the flow. If you’re still viewing the Quick Account flow in Flow Builder, click `Activate`. If not, follow these steps.

1. from Setup, enter Flows in the Quick Find box, then select `Flows`.
2. Click `Quick Account`.
3. From the button bar in Flow Builder, click `Activate`.

## Add Your Flow to the Home Page

1. Create a home page.
    - From Setup, enter Builder in the Quick Find checkbox, and then select `Lightning App Builder`.
    - Click `New`.
    - Select `Home Page` and click `Next`.
    - Give the page a name and click `Next`.
    - Click **`CLONE SALESFORCE DEFAULT PAGE`**, select `Home Page Default` if necessary, and click `Finish`.

2. Drag the Flow component to the top of the right column.

    ![Dragging the Flow component onto a home page](/assets/flow-component.png)

3. For Flow, select `Quick Account`.
4. Click `Save` and `Activate` to save your changes and activate the page.
5. Click `Assign as Org Default` and `Save` to assign this page as the org default home page.
6. To see your flow in action, go to your Home page.
    a. Click `Back` to return to Setup.
    b. Click `App Launcher` icon, click `Sales`, then click `Home`.

![Resulting home page](/assets/quick-account-home-page.png)

## Make Sure Your Users Can Run the Flow

To make sure that your users can run the flow, add the `Run Flows` user permission to a permission set or profile, and assign it to the right users. If **`Override default behavior and restrict access to enabled profiles or permission sets`** is selected for the flow, add the flow to a permission set or profile, and assign it to the right users.

### Note

Only flow admins (users with the Manage Flow user permission) can run inactive flows.

## Tell Me More

- A `flow interview` is a running instance of a flow. When you distribute a flow, users interact with individual interviews of that flow.
- This unit walked you through a simple example of a flow. You can customize that flow to do much more. For example:
  - enhance the Quick Account flow so that it provides values for more account fields, like Account Number or Ownership
  - Or use the same inputs to also create a contact and an opportunity.

## Resources

- [Salesforce Help: Flows](https://help.salesforce.com/articleView?id=flow.htm&language=en_US)
- [Trailblazer Community: Salesforce Automation](https://success.salesforce.com/_ui/core/chatter/groups/GroupProfilePage?g=0F9300000001rzc)
- [Trailhead Module: Screen Flow Distribution](https://trailhead.salesforce.com/modules/screen_flow_distribution)
