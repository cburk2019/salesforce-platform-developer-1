# Salesforce -> Developer Beginner -> Salesforce Flow -> Choose the Right Automation Tool

## Learning Objectives

- List the tools included in Salesforce Flow.
- Describe the tools available for automating guided visual experiences.
- Describe and compare the tools available for behind-the-scenes automation.
- Describe the tools available for approval automation.

## People Expect Automation

No matter whether they’re buying movie tickets, paying bills, or changing restaurant reservations, if a customer is interacting with a company, they expect a seamless, personalized experience.

For example, when a customer needs to replace her credit card, the average service agent needs to know a bunch of things. Is it damaged, lost, or stolen? If it’s stolen, is she worried about recent transactions? Where should we send the new card? Serving a customer in this situation and gathering and maintaining related data can involve separate systems with varying degrees of complexity.

## Automation Used to Be Hard

Providing a seamless, automated customer experience has historically been challenging, time-consuming, and code-heavy. Depending on the precise nature of your business processes, you may have had to:

- Integrate various systems.
- Configure process logic.
- Design and build an end-user experience.
- Make the experience available from anywhere: desktop or mobile devices, internal apps, or external portals.

## Meet Salesforce Flow

Salesforce Flow provides declarative process automation for every Salesforce app, experience, and portal.

Included in Salesforce Flow are two point-and-click automation tools:

- Flow Builder, which lets you build flows
- Process Builder, which lets you edit existing processes

To sum up the differences:

- Salesforce Flow is the name of the product.
- Flow Builder and Process Builder are the names of the tools.
- Use Flow Builder to make flows; use Process Builder to refine existing processes.

Later, we talk about when to use each tool, but for now here’s a sneak peek at what business processes look like in each tool.

### Flow Builder

![A sample business process configured in Flow Builder](/assets/flow-builder.png)

### Process Builder 

![A sample business process configured in Process Builder](/assets/process-builder.png)

Salesforce Flow makes it easy for you to do the following.

| Use Case | Salesforce Flow Functionality |
| -------- | ----------------------------- |
| Create a guided tutorial or wizard with screens. | Flow Builder includes several out-of-the-box screen components, like text boxes, radio buttons, and file-uploads. If you need more than what’s offered, add custom Lightning components to your screens. |
| Set up automated tasks and processes. | Declaratively configure logic and actions for your business process with Flow Builder. If needed, you can build custom Apex code to fill any functional gaps. |
| Connect to external systems. | Communicate changes between your Salesforce org and your external systems with platform events. Flow Builder lets you respond to and send platform event messages. Flow Builder can also retrieve data from third-party systems with External Services. |
| Add automation to your pages and apps. | Make sure your behind-the-scenes processes start when the right action happens, whether that’s when records change or when users click a particular button. Once you build guided visual experiences, add them to Lightning pages, Experience Builder pages, the utility bar in your Lightning apps, and more. |
| Reuse what you build. | In Flow Builder, break down process logic or actions into a flow that's referenced by a Subflow element. You can reuse or reference this flow in other business processes. In Process Builder, call an autolaunched flow from a process to automate complex business processes. |

## Which Automation Tool Is Right for My Use Case?

When it’s all said and done, a process-driven experience isn’t backed by only one process. It’s a combination of all the business processes in your org that can impact your customer. Each business process typically falls into one of these camps.

| Type of Business Process | Description | Available Tools |
| ------------------------ | ----------- | --------------- |
| Guided visual experience | Business processes that need input from users, whether they’re employees or customers. | Flow Builder |
| Behind-the-scenes automation | Business processes that get all the necessary data from your Salesforce org or a connected system. In other words, user input isn’t needed. | Flow Builder (Recommended), Process Builder (Use for existing processes), Apex |
| Approval automation | Business processes that determine how a record, like a time-off request, gets approved by the right stakeholders. | Approvals |

## Flows and Processes and Apex

One of the hardest things for an admin or a developer to figure out is when to use what tool for the job at hand. In general, it’s best to start with declarative, no-code tools and work your way up to code solutions.

### Flow Builder

Use Flow Builder to:

- Automate a guided visual experience.
- Start a behind-the-scenes business process:
- When a user clicks something, like a button
- When a record is created
- When a record is updated
- When a record is deleted
- When a platform event occurs
- At a specified time and frequency

For example, when an opportunity is won, your company wants a renewal opportunity to be created automatically.

### Process Builder

For all behind-the-scenes automation needs, we recommend that you use Flow Builder. Use Process Builder only if you’re already familiar with using it and you need to edit an existing process. To create a new automated process, use Flow Builder instead.

Process Builder contains some of the same functionality that Flow Builder does. Processes can start when:

- A record is created
- A record is updated
- A platform event occurs

### Apex

Use Apex when you need more functionality than is available in Flow Builder. Build the more complex functionality as ***`invocable Apex methods`***. Then call the resulting Apex as an Apex action in the process or as an Apex action element in the flow.

Now, let’s see these principles in practice with a few sample scenarios.

## Sample Scenarios

Build flows in Flow Builder for the following scenarios.

- Guide a site member through requesting a new credit card with a step-by-step wizard.
- A sales rep clicks a button on an opportunity, which launches a discount calculator.
- When an account is updated, update all of the contacts related to that account.
- When an opportunity stage is updated, also update a custom checkbox field.
- Create a task when a platform event occurs.
- Update a lead record in Salesforce after a certain amount of time passes, or when a specified time is reached.
- When an opportunity closes, automatically create a renewal opportunity.

***`Use Process Builder only to edit an existing process.`***

Build an approval process in Approvals to route an employee’s time-off request to a manager for approval.

## Wait. What’s an Approval Process?

Surprise! We snuck another tool in here. Approvals isn’t included in Salesforce Flow, but it offers a declarative way to automate something that Salesforce Flow doesn’t cover. That said, Salesforce Flow does support automating how a record gets submitted for approval. You’ll learn more about Approvals later in this module.

## Resources

- [Salesforce Help: Which Automation Tool Do I Use?](https://help.salesforce.com/HTViewHelpDoc?id=process_which_tool.htm&language=en_US)
