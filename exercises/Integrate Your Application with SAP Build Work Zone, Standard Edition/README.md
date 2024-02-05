# Exercise 9 - Integrate Your Application with SAP Build Work Zone, Standard Edition

In this exercise you will learn
- How to integrate with SAP Build Work Zone, standard edition to your application

##  Integrate with SAP Build Work Zone, standard edition

### Update content

1. Open your subaccount and search for **Instances and Subscriptions**.

2. Search for the application **SAP Build Work Zone, standard edition** and choose the icon to open it.

3. In the menu on the left side choose the icon for **Channel Manager**.

4. Choose the refresh icon to fetch the updated content.

> Check the status and if errors exist, view the logs. If you have used the `-` character in your Semantic Object name it will cause an error (as an example).

   ![WorkZone1](./images/integrate_launchpad_1.png)

#### Add application to Content Explorer

5. Choose **Content Manager** in the menu on the left and Click on **Content Explorer** button.

6. Select the tile **HTML5 Apps** with your respective subdomain name.

    ![WorkZone2](./images/integrate_launchpad_2.png)

7. In the items table, set checkmark for the app **Incidents** and choose the button **Add**.

    ![WorkZone3](./images/integrate_launchpad_3.png)

#### Create a group

8. Go to the **Content Manager** tab, choose **Create** and select **Group** from dropdown.

    ![WorkZone4](./images/integrate_launchpad_4.png)

9. Add the title **Incident Management xxx Group**.
> Use your teched user number for `xxx`. Eg., If your user name is XP260-001, use 001 as the `xxx`.

10. Assign items in the Assignment Status. Search for **Incident** and choose the slider icon to assign the app.

11. Choose **Save**.

    ![WorkZone5](./images/integrate_launchpad_5.png)

#### Add application to the Everyone Role

12. Back in the **Content Manager**, choose role **Everyone** and **Edit**.

13. Assign items in the Assignment Status. Search for **Incident** and choose the Slider icon to assign the app.

14. Choose **Save**.

    ![WorkZone6](./images/integrate_launchpad_6.png)

#### Create site

15. In the menu on the left side navigate to **Site Directory**.

16. Choose button **Create Site**.

     ![WorkZone7](./images/integrate_launchpad_7.png)

17. Enter the site name as **IncidentManagement xxx Site** and choose **Create**.
> Use your teched user number for `xxx`. Eg., If your user name is XP260-001, use 001 as the `xxx`.

18. Now, you are forwarded to your created site.

#### Test your site

19. Navigate to **Site Directory**.

20. Find your created site.

    ![WorkZone8](./images/integrate_launchpad_8.png)

21. Open it by choosing **Go to site**.

    ![WorkZone9](./images/integrate_launchpad_9.png)
 
## Summary

Your application is now integrated with the SAP Build Work Zone, standard edition service, giving you one central entry point to show all of your SAP BTP applications.

> Note: You can also run your application directly from the BTP cockpit. In the BTP cockpit, subaccount page, there is an **HTML5 Applications** menu, which list all applications deployed to the HTML repo and using the managed-approuter (as provided by Work Zone).

Continue to - [Exercise 10 - Logging, Tuning & Hybrid Development](../Hybrid%20Development/README.md)
