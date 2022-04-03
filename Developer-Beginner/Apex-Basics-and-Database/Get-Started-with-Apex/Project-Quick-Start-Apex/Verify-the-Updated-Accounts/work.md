# Salesforce -> Developer Beginner -> Apex Basics & Database -> Get Started with Apex -> Project: Quick Start: Apex -> Verify the Updated Accounts

## Check the Updated Field

Now let’s make sure that the code you executed made the changes you want. Find an older account, and check the description field to see if it was updated.

1. In your Trailhead Playground, click the `App Launcher` icon. and select `Sales` under All Apps.
2. Click the `Accounts` tab.
3. Click `Recently Viewed` to show the list of views, and then select `All Accounts`.

    ![The Accounts tab is in the Sales app. It includes a number of list views including the All Accounts list view.](/Developer-Beginner/Apex-Basics-and-Database/Get-Started-with-Apex/Project-Quick-Start-Apex/Verify-the-Updated-Accounts/assets/all-accounts-list-view.png)

4. Click the `gear icon` and select `Select Fields to Display`. Move `Last Modified Date` to the Visible Fields column, and then click `Save`.
5. Click one of the five most recently modified account records (use the Last Modified Date to find these accounts).
6. Click `Details`.
7. Look for the Description field. The value should be: `Heritage Account`

### Summary

Congratulations! You've created your first Apex class that has code to retrieve Account records and logic to iterate over a list of Account records and update the Description field. As you can see, it's easy to manipulate records and data using Apex. To learn more, check out the Trailhead module on [Apex Basics & Database](https://developer.salesforce.com/trailhead/module/apex_database).
