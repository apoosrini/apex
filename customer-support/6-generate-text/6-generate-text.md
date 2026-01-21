# Generate Ticket Summary with AI

## Introduction

In this lab, you will enhance your Oracle APEX application by creating a modal dialog page that displays AI-generated ticket summaries. You will create a modal dialog page with page items for ticket ID and summary text, configure a RAG source to fetch comprehensive ticket details including interaction counts, and implement a close button with dynamic action to close the dialog.

Estimated Time: 5 minutes

### Objectives

- Create a modal dialog page for ticket summary display.

- Add hidden page items for ticket ID and summary text.

- Create a dynamic content region to display formatted summary.

- Configure a RAG Source to fetch comprehensive ticket details.

- Implement a close button with dynamic action to close the dialog.

- Create a dynamic action to automatically generate ticket summary on page load.

- Add a button to the ticket finder page to launch the summary modal.

## Task 1: Create Modal Dialog Page - Ticket Summary

1. Click on **App#ID** in the runtime developer toolbar to navigate to the App Builder.

    !["Runtime Dev toolbar"](images/nav-app-builder.png "")

2. Click **Create Page**.

    !["Create Modal Dialog"](images/create-page.png "")

3. Select **Blank Page** and click **Next**.

    !["Create Modal Dialog"](images/create-blank.png "")

4. Enter the following:

    - Page Number: **13**

    - Name: **Ticket Summary**

    - Page Mode: **Modal Dialog**

5. Click **Create**.

    !["Create Modal Dialog"](images/create-modal.png "")

## Task 2: Create Page Items

1. In the Page Designer for Page 13, go to the **Rendering** tab.

2. Right-click **Page Items** and select **Create Page Item**.

    !["Create Page item"](images/create-page-item1.png "")

3. In the Property Editor, enter/select the following:

    - Name: **P13_TICKET\_ID**

    - Type: **Hidden**

    !["Create Page item"](images/page-item1-details.png "")


4. Similarly, create a second page item. Right-click **Page Items** and select **Create Page Item**. 

    !["Create Page item"](images/create-page-item2.png "")


5. In the Property Editor, enter/select the following:

    - Name: **P13\_TICKET\_SUMMARY**

    - Type: **Hidden**

    !["Create Page item"](images/page-item2-details.png "")

5. Click **Save**.

## Task 2.5: Create Dynamic Content Region


1. In the Rendering Pane, right-click **Content Body** region and select **Create Region**.

    !["Create Region"](images/create-region.png "")

3. In the Property Editor, enter/select the following:

    - Identification > Title: **Ticket Summary**

    - Type: **Dynamic Content**

    - Source > PL/SQL Code:

        ```
        <copy>
        IF :P13_TICKET_SUMMARY is null then
            return '<span aria-hidden="true" class="fa fa-spinner fa-anim-spin"></span><span> Generating Summary ...</span>';
        else
            return apex_markdown.to_html(:P13_TICKET_SUMMARY);
        END IF;
        </copy>
        ```

    - Source > Page Items to Submit: **P13\_TICKET\_SUMMARY**

    !["Region details in page designer"](images/region-details.png "")

4. Click **Save**.

## Task 3: Add Close Button with Dynamic Action

1. In the Page Designer for Page 13, go to the **Rendering** tab. Right-click **Dialog Footer** region and select **Create Button**.

    !["Create Button"](images/create-button.png "")

3. In the Property Editor, enter/select the following:

    - Identification > Button Name: **CLOSE\_DIALOG**

    - Label: **Close**

    - Appearance > Button Template: **Text**

    !["Create Button"](images/button-details.png "")

4. Right-click the **CLOSE\_DIALOG** button and select **Create Dynamic Action**.

    !["Create dynamic action"](images/create-da.png "")

5. In the Property Editor, enter the following:

    - Identification > Name: **Close Dialog**

    !["Create dynamic action"](images/da-name.png "")

6. Under **True** Action, click **Show**. In the Property Editor, enter/select the following:

    - Identification > Action: **Close Dialog**

    !["Create dynamic action"](images/true-action.png "")

7. Click **Save**.

## Task 4: Generate Text Using AI Dynamic Action

1. In Page Designer for Page 13, switch to the **Dynamic Actions** tab.

    !["Page designer"](images/da-tab.png "")

2. Right-click **Page Load** and select **Create Dynamic Action**.

    !["Create dynamic action"](images/create-da2.png "")

3. In the Property Editor, enter the following:

    - Identification > Name: **Generate Ticket Summary**

    !["Create dynamic action"](images/da2-name.png "")

4. Under **True** Action, click **Show**. In the Property Editor, enter/select the following:

    - Identification > Action: **Generate Text with AI**

    - Generative AI > Configuration: **Ticket AI Configuration**

    - Input Value > Type: **Only System Prompt**

    - Use Response > Type: **Item**

    - Use Response > Item: **P13\_TICKET\_SUMMARY**

   !["Create dynamic action"](images/da2-true-action.png "")

5. Right-click the **Generate Text with AI** action and select **Create Action**.

    !["Create dynamic action"](images/create-action.png "")

6. Under the new action, click **Show**. In the Property Editor, enter/select the following:

    - Identification > Action: **Refresh**

    - Selection Type: **Region**

    - Region: **Ticket Summary** (the Dynamic Content region you created)

    !["Create action"](images/action-details.png "")    

7. Click **Save**.

## Task 5: Add Generate Ticket Summary Action to Tickets Report

1. Click the page finder on the toolbar. Navigate to **Page 5** (Faceted Search page).

    !["Switch page"](images/switch-page.png "")  

2. In the **Rendering** tab, locate the **Tickets** report region.

    !["create action"](images/create-action-2.png "")

3. Right-click **Actions** under the **Tickets** region and click **Create Action**.

4. In the Action properties:

    - **Position**: **Primary Actions**

    - **Template**: **Button**

    - **Label**: **Generate Ticket Summary**

    - **Type**: **Redirect to Page**

    !["create action"](images/action2-details.png "")

    - **Target**:

        - **Page**: **13**

        - **Set Items**:

            - **Name**: **P13\_TICKET\_ID**

            - **Value**: **&TICKET\_ID.**

    !["create action"](images/target-link-details.png "")

    - **Icon**: **fa-info-circle**

    !["create action"](images/icon.png "")

5. Click **Save**.

## Task 6: Define RAG Source

1. Navigate to **Shared Components**.

    !["Click App Builder"](images/nav-sc.png "")

2. Under Generative AI, click **AI Configurations**.

    !["Click App Builder"](images/ai-conf3.png "")

3. Select **Ticket AI Configuration** (created in the previous lab). If you haven't created it yet, follow Lab 5 to set it up first.

    !["Click App Builder"](images/select-ticket-config.png "")

4. Under RAG Sources, click **Create RAG Source**.

    !["Click App Builder"](images/create-rag2.png "")

5. In the RAG Source page, enter/select the following:

    - Identification > Name: **Ticket Summary Details**

    - Description: **Retrieve comprehensive ticket details for summary generation**

    - Source > SQL Query: Copy and paste the following SQL into the code editor.

        ```
        <copy>
        select t.ticket_number,
               t.subject,
               t.description,
               t.status,
               t.priority,
               t.channel,
               ag.agent_name,
               c.customer_name,
               a.account_type,
               (select count(*) from cs_interactions i where i.ticket_id = t.ticket_id) as interaction_count
          from cs_tickets t
          join cs_customers c on c.customer_id = t.customer_id
          left join cs_accounts a on a.account_id = t.account_id
          left join cs_agents ag on ag.agent_id = t.assigned_agent_id
         where t.ticket_id = :P13_TICKET_ID
        </copy>
        ```

        !["Click App Builder"](images/rag2-details.png "")

    - Server-side Condition > Type: **PL/SQL Function Body returning Boolean**

    - Server-side Condition > PL/SQL Function Body returning Boolean: **RETURN :APP_PAGE\_ID = 13;**

    Click **Create**.

    !["Click App Builder"](images/rag2-server-side.png "")

6. Once the RAG Source is created, click **Apply Changes**.
    !["apply changes"](images/apply-changes.png "")


7. **Save and Run** the app.

    !["save and run app"](images/save-run6.png.png "")

## Summary

In this lab, you created a complete AI-powered ticket summary system in Oracle APEX. You built a modal dialog page that displays formatted ticket summaries with loading indicators, configured RAG sources for data retrieval, implemented automatic text generation on page load, and added a button to the ticket finder page to launch the summary modal. The system provides a seamless user experience for generating and viewing AI-powered ticket summaries with proper loading states and formatted display.

## Acknowledgments

- **Authors** - Toufiq Mohammed, Principal Product Manager; Apoorva Srinivas, Principal Product Manager
- **Last Updated By/Date** - Apoorva Srinivas, Principal Product Manager, January 2026
