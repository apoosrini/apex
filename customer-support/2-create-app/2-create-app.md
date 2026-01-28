# Build the Customer Support Application using Generative AI

## Introduction

In this lab, you will build an interactive Customer Support portal using the **Create Application with Generative AI** feature in Oracle APEX. The application builds on the comprehensive Customer Support data model created in the previous lab, enabling you to rapidly prototype end-to-end support operations.

Estimated Time: 5 minutes

### Objectives

- Create a customer-support-focused application leveraging the AI-assisted Create Application wizard based on the previously generated Customer Support data model.

### Prerequisites

- All previous labs are completed.

## Task 1: Refresh Data Dictionary

When we generate a data model, the database updates instantly but APEX’s schema metadata is not yet updated. Refreshing the Data Dictionary ensures APEX reads the latest tables and makes them available in wizards and builders. In this task, we refresh the Data Dictionary to synchronize APEX with the updated customer-support schema.

1. To refresh the database objects, navigate to APEX Administration from the top-right corner of the navigation bar. Select **Manage Service > Manage Service**.

    !["Click App Builder"](images/manage-service.png "")

2. On the right hand side, under **Manage Meta Data**, select **Data Dictionary Cache**.

    !["Click App Builder"](images/data-dictionary-cache.png "")

3. To refresh the cache manually, click **Refresh Cache Only**.

    !["Click App Builder"](images/refresh-cache-only.png "")

4. Once the cache is refreshed, you can view the newly created database objects.

    !["Click App Builder"](images/review-tables.png "")

## Task 2: Create the Application using Generative AI

In this task, you will create an application using Generative AI and enter natural language.

1. From your APEX workspace top navigation bar, click **App Builder**.

    !["Click App Builder"](images/app-builder-2.png "")

2. Click **Create a New App**.

    !["Click create App"](images/create-new-app.png "")

3. In the 'Create an Application' page, select **Create App Using Generative AI**.

    !["Click create app using Gen AI"](images/create-app-using-gen-ai.png "")

    *Note*: If the AI Assistant does not detect the tables created using AI, refresh the Data Dictionary Cache to ensure the latest tables are available. Refer [Lab: Task 1](?lab=2-create-app#Task1:RefreshDataDictionary)

4. To create the Customer Support application, chat with the APEX Assistant wizard with the prompts below. Enter each prompt and hit **Enter**.

    Prompt 1:

    ```
    <copy>
    Create a Customer Support portal for a banking customer. Create pages to manage Customers, Accounts, and Tickets.
    </copy>
    ```

    !["first prompt"](images/app-prompt.png "")

    *Important Note:* The prompt may not always generate all pages or include every table. This behavior can vary depending on the AI service provider or the model used. If some pages are missing, you can ask the AI service to update your blueprint by specifying the additional pages you need.

5. We need to ensure that a user can filter support tickets efficiently in the application. Enter the following prompt and hit **Enter**.

    Prompt 2:
    ```
    <copy>
    Make Tickets searchable using faceted search.
    </copy>
    ```

    !["second prompt"](images/add-faceted-search.png "")

6. Finally, add a Form that allows Support Agents to edit tickets.

    Prompt 3:
    ```
    <copy>
    Add a Form page to edit Tickets.
    </copy>
    ```

    !["third prompt"](images/add-form.png "")

7. Verify if the blueprint already contains a dashboard page; if not, add a dashboard page to track Customer Support tickets.

    Prompt 4:
    ```
    <copy>
    Add a Dashboard page to track Customer Support tickets.
    </copy>
    ```
    !["enter prompt"](images/add-dashboard.png "")

8. Once you are satisfied with the AI generated application blueprint, click **Create Application**.

    !["sixth prompt"](images/create-app-blueprint.png "")

    *Important Note:* The pages might differ based on the prompt. Make sure the blueprint includes a **Support Dashboard** page that you can later set as the Home page, a **Faceted Search** page on **CS\_TICKETS**, and a **Form** page on **CS\_TICKETS**. If any page is missing, add additional natural-language prompts before generating the app.*

10. On the 'Create an Application' page, locate the **Dashboard** page (in this example, **Support Pulse**) and click **Edit**.

    ![select appearance](images/edit-dash.png " ")

11. In the **Add Dashboard Page** dialog, rename the page to **Support Dashboard**.

12. Under **Advanced**, enable **Set as Home Page**, so that the Support Dashboard page becomes the landing page. Then, click **Save Changes**.

    ![select appearance](images/update-dash.png " ")

13. Update the application name to **Customer Support Portal** and click on the app icon to upload a custom support icon.

    ![select appearance](images/set-icon.png " ")

14. Download a sample icon **[here](images/customer-support-portal.png)** (or substitute your organization’s own asset). Click **Upload your own icon**, choose the image, and click **Save Icon**.

    ![select appearance](images/save-icon.png " ")

15. Make sure that the **Progressive Web App** and **Feedback** features remain enabled so the support app is installable and gathers agent/customer input. Then, click **Create Application**.

    ![click create application](images/create-cs-app.png " ")


## Task 3: Run the Application

1. It is now time to see how the AI generated Customer Support app looks! Click **Run Application**.

    ![run the application](images/run-app-2.png " ")

2. The login page is displayed. Enter **Username** and **Password**, then click **Sign In** to launch the Customer Support Portal.

    ![input login credentials](images/login-detail.png " ")

3. Explore key experiences:

    - Review the **Support Dashboard** home page and verify top-level KPIs render correctly.
    - Navigate to the **Customers**, **Accounts**, and any other data-model pages (such as **Channels**, **Priorities**, or **Service Levels**) to ensure records and quick actions work as expected.
    - Open the **Ticket Explorer** faceted search page and try different filters to confirm the AI-generated facets align with your schema.
    - Use the **Ticket Details** maintenance form to view or edit a record and confirm the layout meets your agents’ needs.

    Records are pre-populated across these pages so you can validate layouts, filters, and forms without additional data entry. Update or extend the data to reflect your real Customer Support scenarios.

    ![display support dashboard page](images/cs-dashboard1.png " ")

    ![display faceted search page](images/ticket-facet.png " ")
   

## Summary

You now understand how to use Generative AI to create an initial version of a Customer Support application that manages your complete Customer Support data model end-to-end.

## Acknowledgments

- **Authors** - Toufiq Mohammed, Principal Product Manager; Apoorva Srinivas, Principal Product Manager
- **Last Updated By/Date** - Apoorva Srinivas, Principal Product Manager, January 2026
