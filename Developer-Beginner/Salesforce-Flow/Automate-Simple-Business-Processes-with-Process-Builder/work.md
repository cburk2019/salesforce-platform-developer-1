# Salesforce -> Developer Beginner -> Salesforce Flow -> Automate Simple Business Processes with Process Builder

## Use Flow Builder To Create a New Automated Process

- For all behind-the-scenes automation needs, we recommend that you use Flow Builder.
- Use Process Builder only if you’re already familiar with using it and you need to edit an existing process.
- To create a new automated process, use Flow Builder instead.

## Learning Objectives

- List the types of processes that you can build in Process Builder.
- Define the key components used to create a process.
- Build a process that updates the addresses for an account's contacts when the account’s address is updated.

## Get Started with Process Builder

Process Builder is a point-and-click tool that lets you easily automate if/then business processes and see a graphical representation of your process as you build.

## The Components of a Process

Every process consists of a trigger, at least one criteria node, and at least one action. You can configure immediate actions or schedule actions to be executed at a specific time.

Here’s an example of a simple process.

![An example of a process with one criteria node, one immediate action, and one scheduled action.](/assets/process-with-components.png)

## Trigger: Identify When the Process Should Run

The trigger identifies when the process should run. For record change processes, the trigger determines which object and which of the following changes the process should pay attention to.

- Only when a record is created
- Anytime a record is created or edited

## Criteria: Determine Whether or Not to Execute Actions

While a process gets one trigger, you can add as many criteria nodes as your heart desires. Each criteria node controls whether or not the process executes the associated actions. If the record doesn’t meet the criteria, the process skips those actions and moves on to the next criteria node in the process.

In each criteria node, you can:

- Set filter conditions.
- Enter a custom formula. Like in validation rules, the formula must resolve to true or false.
- Opt out of criteria and always execute the associated actions.

## Actions: What the Process Should Do

When a criteria node evaluates to true, the process executes the associated actions or waits to execute them at a scheduled time.

- Each immediate action is executed as soon as the criteria evaluates to true.
- Each scheduled action is executed at the specified time, such as 10 days before the record’s close date or 2 days from now. At the specified time, Salesforce makes sure that the associated criteria node still evaluates to true. If so, the scheduled action is executed. You can schedule actions based on either:
  - A specific date/time field on the record that started the process. For example, a month before an account's service contract expires.
  - The time that the process ran. For example, 3 days from now.

Regardless of when the actions execute, here are some of the things you can do with a process action.

- Create records.
- Update the record that started the process or any related record.
- Submit that record for approval.
- Update one or more related records.
- Send emails using a specified email template.
- Post to a Chatter feed.

## Process Types

Process Builder can automate a few kinds of business processes. The main difference is the trigger: when the process starts.

| Type | Process Starts When |
| ---- | ------------------- |
| `Record Change` | A record is created or edited |
| `Invocable` | It’s called by another process |
| `Platform Event` | A platform event message is received|

To keep things simple, this unit focuses on the most common process type: ***`Record Change`***.

## Process Builder

Before you dig into the Process Builder, let’s take a quick tour.

![Screenshot of the Process Builder user interface](/assets/process-builder-UI.png)

The button bar **`(1)`** lets you manage the process or view the list of all processes.

The canvas **`(2)`** is the main workspace for a process. On the canvas, you define:

- The trigger **`(3)`**
- One or more criteria nodes **`(4)`**

One or more actions **`(5)`** in an action group **`(6)`**

## Build a Process

Here’s a common use case: If an opportunity is created or updated (***trigger***) and it’s high-value and closed won (***criteria***), then create a draft contract (***immediate action***). Six days after the opportunity closes (***schedule***), create a follow–up task for the account owner (***scheduled action***).

### Note

Plan out your business process before you try to automate it. Doing so makes it easier to configure when using one of our automation tools.

1. From Setup, enter Process Builder in the Quick Find box, select `Process Builder`, and then click `New`.
2. Click `Continue in Process Builder`.
3. Name the process Closed Won Opportunities. The API name updates to Closed_Won_Opportunities when you tab out of the Name field.
4. For the description, enter If a high-value opportunity is closed and won, create a draft contract and a follow-up task for the account owner.
5. Configure the process to start when a record changes.
6. Click `Save`.

## Add a Trigger

1. Click `Add Object`.
2. For Object, enter Opp to filter the list of options and select `Opportunity`.
3. Select when a record is created or edited.

    ![Choose Object and Specify When to Start the Process panel](/assets/process-start-example.png)

4. Click `Save`.

## Add Criteria

Now let’s define the criteria. We check whether the opportunity is closed won and if it’s high-value. In this case, high-value means more than $250,000.

1. Click `Add Criteria`.
2. Name the criteria Closed Won and High-Value.
3. Leave `Conditions are met` selected.
4. Check whether the opportunity has been closed and won.
    a. For Field **`(1)`**, choose `Opportunity` | `Stage`, and click `Choose`.
    b. For Operator **`(2)`**, leave `Equals` selected.
    c. For Type **`(3)`**, leave `Picklist` selected.
    d. For Value **`(4)`**, select `Closed Won`.
5. With another condition, check whether the opportunity is high value.
    a. Click `Add Row`.
    b. For Field **`(1)`**, choose `Opportunity` | `Amount`, and click `Choose`.
    c. For Operator **`(2)`**, select `Greater than`.
    d. For Type **`(3)`**, leave `Currency` selected.
    e. For Value **`(4)`**, enter `250,000`.
    f. Be sure `All of the conditions are met` is selected.

    ![Define Criteria for this Action Group panel](/assets/action-group-example.png)

6. Click `Advanced` and select Yes. When you select this option, the process ignores record changes that aren’t relevant to your defined criteria. For example, if the opportunity’s description is updated, the process won’t execute the associated actions.
7. Click `Save`.

## Add a Schedule

Let’s have the owner follow up with the account 6 days after the opportunity closes.

1. Under Scheduled Actions, click `Set Schedule`.
2. Set the schedule for 6 days after the opportunity closes.

    ![Set a Schedule panel](/assets/set-schedule-example-1.png)

3. Click `Save`.

## Add Actions

Now let’s define the actions that execute when the criteria are met. We need an immediate action that creates a draft contract and a scheduled action that creates a task for the account’s owner.

## Immediate Action

1. Under Immediate Actions, click `Add Action`.
2. For the action type, select `Create a Record`.
3. Name the action Create Draft Contract.
4. For Record Type, select `Contract`. When you select the object that you want to create a record for, Process Builder displays rows for the required fields.
5. To associate the contract with the opportunity’s account, set Account ID.
    a. For Type, select `Field Reference`.
    b. For Value, select `Opportunity` | `Account ID` (with no arrow next to it) and then click `Choose`.
      - When you select a value without an arrow next to it, you're selecting a field. To use fields on related records, click a value with an arrow next to it.
     ![Select Opportunity > Account ID](/assets/select-account-id.png)
6. Make sure that the new contract is a draft. In the Value for Status, select `Draft` from the dropdown list.

    - [In the process action, the contract's Account ID is set to the opportunity account owner ID and the contract's status is set to Draft.](/assets/process-action-example-1.png)

7. Click `Save`.

## Scheduled Action

1. Under the schedule we created earlier (6 Days After Close Date), click `Add Action`.
2. For Action Type, select `Create a Record`.
3. Name it Follow-up Task.
4. For Record Type, select Task.
5. Set the task's field values.

    | Field | Type | Value |
    | ----- | ---- | ----- |
    | Assigned to ID | Field Reference | Opportunity > Account ID > Owner ID - (When you select Owner ID, make sure you select the second one.) |
    | Priority | Picklist | High |
    | Status | Picklist | Not Started |

6. Click Save.

Success! You’ve created a process that automatically manages your high-value business opportunities.

![Final process](/assets/final-process-example.png)

To start using this process, just activate it.

## Tell Me More

You can expand this process to include more criteria and actions. If the first criteria node that you defined doesn’t evaluate to true, the process can then check whether a high-value opportunity is closed and lost, or whether a quote was given, with more actions based on those conditions. 

## Resources

- [Salesforce Help: Process Builder](https://help.salesforce.com/HTViewHelpDoc?id=process_overview.htm&language=en_US)
