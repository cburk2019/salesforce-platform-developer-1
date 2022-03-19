# Salesforce -> Developer Beginner -> Salesforce Flow -> Customize How Records Get Approved with Approvals

## Learning Objectives

- Define an approval process, and list its key components.
- Describe a business process that can be automated using an approval process.
- Set up an approval process to automatically manage when an account changes from a prospect to a new customer.

## Get Started with Approvals

An approval process automates how Salesforce records are approved in your org. In an approval process, you specify:

- The steps necessary for a record to be approved and who approves it at each step. For example, when an employee creates a time-off request, have Salesforce automatically send an approval request to the employee’s manager.
- The actions to take based on what happens during the approval process. For example, if a time-off request is approved, update fields on the employee’s record. But if the request is rejected, send a notification to the employee.

Let’s look at an example approval process to see how a record moves through various steps of the process. In this example, a user submits a request for a new position in a company.

![Chart that shows an example approval process](/assets/approval-process.png)

When a user first requests approval for a new position, initial submission actions occur. The default initial submission action locks the record. This action ensures that other users (except for approvers and admins) can’t change the record while it's pending approval. Other possible submission actions include sending an email alert, updating a field on a record, creating a task, and sending an outbound message.

Approval steps assign approval requests to various users and define the chain of approval for a particular approval process. In this example, the first step assigns the approval request to the submitter's direct manager.

If the direct manager rejects the request, the final rejection actions are executed, setting the position’s approval status to `Rejected`.

If the direct manager approves the request, the record moves to the next step—approval from the CEO. If the CEO rejects the position, the same final rejection actions occur.

If the CEO approves the position, final approval actions are executed. They set the approval status to `Approved`, unlock the record for future updates, and notify the employee who requested the new position.

Final approval actions occur only when a record is approved and there are no further approval steps.

## Build an Approval Process

Now that you’ve seen the basic outline of an approval process, let’s get your hands dirty. You need to make sure that a manager approves opportunities that are discounted more than 40%. The opportunity should reflect its approval status: Approved or Not Approved.

### Note

Plan out your business process before you try to automate it. Doing so makes it much easier to configure when using one of our automation tools.

## Preplanning

Before we dive in, let’s come up with a plan.

| In Order to... | We Need... |
| -------------- | ---------- |
| Track each opportunity’s discount percent | Custom field (Opportunity) |
| Track each opportunity’s approval status | Custom field (Opportunity) |
| Request approval from managers when an opportunity discount is more than 40% | Approval process (Opportunity) |
| Notify managers when an opportunity discount needs approval | Email template |
| When managers respond, update the opportunity’s approval status | Approval actions (Field Update) |

### Note

We're simplifying this scenario for the purposes of this challenge. In the real world, one can use the standard discount field on an opportunity product and then use a [roll-up summary field](https://help.salesforce.com/HTViewHelpDoc?id=fields_about_roll_up_summary_fields.htm&language=en_US) to add that value to the opportunity record.

## Create an Email Template

First create your email template to notify the record owner’s manager that an opportunity has been discounted more than 40%.

1. From Setup, enter Templates in the Quick Find box, and then select `Classic Email Templates`.
2. Click `New Template`.
3. Select `Text` as the template type, and click `Next`.
4. Configure the email template.

    | Field | Value |
    | ----- | ----- |
    | Folder | Unfiled Public Classic Email Templates |
    | Available for Use | Selected |
    | Email Template Name | Approve Opportunity Discount |
    | Encoding | General US & Western Europe |
    | Subject | Please approve this discounted opportunity |
    | Email Body | {!User.Manager}, The {!Opportunity.Name} has been discounted. Please approve this discount. Thank you. |

    - Including the merge field {!Opportunity.Name} helps the approver by providing a link to the opportunity record. This allows them to review the record before responding to the request.

5. Click `Save`.

## Add Custom Fields

Now let’s create custom fields so that we can track the discount percentage and approval status for each opportunity.

1. From Setup, enter Object Manager in the Quick Find box, and then select `Object Manager`.
2. Click `Opportunity`.
3. Select `Fields & Relationships` and click `New`.
4. In the Data Type column, select `Percent` and then click `Next`.
5. Add a Percent field with these values.

    | Field | Value |
    | ----- | ----- |
    | Field Label | Discount Percent |
    | Length | Leave default |
    | Decimal Places | Leave default |
    | Required | Selected |

6. Click `Next`.
7. Click `Next`.
8. Click `Save & New.`
9. In the Data Type column, select `Picklist` and then click `Next`.
10. Add a Picklist field with these values.

    | Field | Value |
    | ----- | ----- |
    | Field Label | Discount Percent Status |
    | Values | Enter values, with each separated by a new line |
    | Picklist Values | Approved / Not Approved |

11. Click `Next`.
12. Click `Next`.
13. Click Save.

Great! You’ve created an email template to notify approvers and you’ve set up an object with the required fields to support your approval process.

## Create an Approval Process

Now that our org is ready, let’s create the approval process.

1. From Setup, enter Approval in the Quick Find box, and then select `Approval Processes`.
2. In Manage Approval Processes For, select `Opportunity`.
3. Click `Create New Approval Process | Use Jump Start Wizard`. The Jump Start Wizard helps you create a simple approval process by making some decisions for you.
4. Configure the approval process.

    | Field | Value |
    | ----- | ----- |
    | Name | Approve Opportunity Discount |
    | Approval Assignment Email Template | Approve Opportunity Discount |
    | Specify Entry Criteria | Opportunity: Discount Percent greater than 0.4 |
    | Select Approver | Let the submitter choose the approver manually |

5. Save the approval process.
6. Click `View Approval Process Detail Page`.
7. Under Final Approval Actions, click `Add New | Field Update`, and configure it with these values.

    | Field | Value |
    | ----- | ----- |
    | Name | Approved |
    | Field to Update | Discount Percent Status |
    | A Specific value | Approved |

8. Click `Save`.
9. Under Final Rejection Actions, click `Add New | Field Update`, and configure it with these values.

    | Field | Value |
    | ----- | ----- |
    | Name | Not Approved |
    | Field to Update | Discount Percent Status |
    | A Specific value | Not Approved |

10. Click `Save`.

Great job! To start evaluating discounted opportunities, simply activate the approval process.

## Make Sure That Records Are Submitted

You've done a bunch of work to automate what happens when a record gets submitted for approval. Now, when users click `Submit for Approval` on an opportunity, it goes through your approval process. But what if—the horror—users forget to click the button?

Enter Flow Builder. One of the available actions in the Action element is Submit for Approval, which means you can build a flow that automatically submits a record for approval. And that means your users don’t have to remember to submit opportunities for approval. For example, in a flow that runs when an opportunity is created or edited:

- Add a Decision element that checks whether Discount Percent is greater than 0.4.
- Add an Action element, set to Submit for Approval, that submits the opportunity for approval.

## Tell Me More

Help your users view open approval requests by adding the Items to Approve component to their Home page. Also, let users respond to approval requests directly from email or Chatter. For more details, see [Prepare Your Org for Approvals](https://help.salesforce.com/articleView?id=approvals_prep_org.htm&language=en_US).

## Resources

- [Salesforce Help: Create an Approval Process with the Standard Wizard](https://help.salesforce.com/HTViewHelpDoc?id=approvals_creating_approval_processes.htm&language=en_US)
- [Salesforce Help: Limits and Considerations for Approvals](https://help.salesforce.com/apex/HTViewHelpDoc?id=approvals_considerations.htm&language=en_US)
- [Salesforce Help: Prepare to Create an Approval Process](https://help.salesforce.com/HTViewHelpDoc?id=approvals_checklist.htm&language=en_US)
- [Salesforce Help: Flow Core Action: Submit for Approval](https://help.salesforce.com/s/articleView?id=sf.flow_ref_elements_actions_approval.htm&type=5)
- [Trailhead Project: Build a Discount Approval Process](https://trailhead.salesforce.com/projects/build-a-discount-approval-process)
