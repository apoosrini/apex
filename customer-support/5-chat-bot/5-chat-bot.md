# Create a Ticket Chat Assistant

## Introduction

In this lab, you will learn how to enhance an Oracle APEX application by creating a Ticket Chat Assistant. Using the Show AI Assistant dynamic action, you will build a chatbot that can respond to user queries about support tickets. You will first configure the chatbot without a RAG (Retrieval-Augmented Generation) source to see how it works with generic responses, and then enhance it by creating an AI Configuration and RAG source so the chatbot fetches information directly from your customer support data. This approach demonstrates how to combine low-code development with AI-driven capabilities to deliver smarter, data-aware user experiences.

Estimated Time: 5 minutes

### Objectives

By the end of this lab, you will be able to:

- Create a Ticket Assistant button in your APEX application.

- Configure a Show AI Assistant dynamic action without using a RAG source.

- Create an AI Configuration and define a RAG Source to query customer, account, and ticket data.

- Connect the AI Configuration to the Show AI Assistant dynamic action so the chatbot fetches results exclusively from your ticket data source.

## Task 1: Set Up Ticket Chat Assistant without a RAG Source

1. Close the dialog box. From the runtime developer toolbar, navigate to **Page 5**.

    >Note: Page number may vary depending on your application. 

    !["Click App Builder"](images/navigate-to-page5.png "")

2. In the left pane, right-click **Breadcrumb** and click **Create Button**.

    !["Click App Builder"](images/chatbot-btn.png "")

3. In the Property Editor, enter/select the following:

    - Under Identification:

        - Button Name: **TICKET_ASSISTANT**

        - Label: **Ticket Assistant**

    - Layout > Slot: **Next**

    - Under Appearance:

        - Button Template: **Text with Icon**

        - Hot: Toggle **On**

        - Icon: **fa-headset**

    !["Click App Builder"](images/ticket-assist-btn.png "")

4. In the left pane, right-click **TICKET_ASSISTANT** button and click **Create Dynamic Action**.

    !["Click App Builder"](images/create-dy-chatbot.png "")

5. In the Property Editor, enter the following:

    - Identification > Name : **Ticket Assistant**

    !["Click App Builder"](images/ticket-dy.png "")

6. Under **True** Action, click **Show**. In the Property Editor, enter/select the following:

    - Identification > Action: **Show AI Assistant**

    - Generative AI > Service: Select **YOUR\_GEN\_AI\_SERVICE**

    - Welcome Message: **Hi! How can I help you with your tickets today?**

    - Appearance > Title: **Ticket Assistant**

    Click **Save and Run**.

    !["Show AI assistant"](images/show-ai-details.png "")


8. In the app, click the **Ticket Assistant** button and enter a prompt such as **List high priority tickets**.

   The chat assistant currently returns results from a web search, not from our database. To fix this, we will create an AI configuration with a RAG (Retrieval-Augmented Generation) source so that the Ticket Assistant fetches details only from the specified data source.

    !["Click App Builder"](images/view-chat.png "")

## Task 2: Create AI Configuration and RAG Source

1. Switch your browser window to App Builder. Navigate to **Shared Components**.

    !["Click App Builder"](images/naviagte-sc.png "")

2. Under Generative AI, click **AI Configurations**.

    !["Click App Builder"](images/ai-conf.png "")

3. In the Generative AI Configurations page, click **Create**.

    !["Click App Builder"](images/create-conf.png "")

4. In the Generative AI Configuration page, enter the following:

    - Identification > Name : **Ticket AI Configuration**

    - Under Generative AI:

        - Service: *Select the AI service you configured in Lab 1.*

        - System Prompt:

            ```
            <copy>
            You are a customer support assistant. Answer questions using the provided ticket data.
            Include customer name, account type, agent name, channel, and status when relevant.
            ```
            </copy>

        - Welcome Message: **Hi! I'm your Ticket Assistant. How can I help you today?**

5. Click **Create**.

    !["Click App Builder"](images/ticket-ai-conf1.png "")


6. Scroll down to locate RAG Sources. Click **Create RAG Source**.

    !["Click App Builder"](images/create-rag-source.png "")

7. In the RAG Source page, enter/select the following:

    - Identification > Name: **Ticket Assistant Source**

    - Description: **RAG source for customer tickets**

    - Source > SQL Query: Click **APEX Assistant**

8. In the APEX Assistant box, enter the following prompt and press enter:

        Prompt 1:
        ```
        <copy>
        Fetch customer support ticket details such as ticket number, subject, description, status, priority, channel, agent name, customer name, and account type.
        </copy>
        ```

    !["Click App Builder"](images/ticket-rag-1.png "")

9. Click **Insert** and review the generated SQL. The generated SQL looks similar to this:

    ```
    <copy>
    select tt.ticket_number,
           tt.subject,
           tt.description,
           tt.status,
           tt.priority,
           tt.channel,
           ag.agent_name,
           cu.customer_name,
           ac.account_type
      from cs_tickets        tt
      left join cs_agents    ag
        on tt.assigned_agent_id = ag.agent_id
      left join cs_customers cu
        on tt.customer_id = cu.customer_id
      left join cs_accounts  ac
        on tt.account_id = ac.account_id
    </copy>
    ```

    Modify the code if needed.

    !["Click App Builder"](images/insert-rag.png "")

10. Verify the RAG Source shows **Success** under the Validation column.

    !["Click App Builder"](images/rag-func1.png "")

11. Under Server-Side Condition, enter/select the following:   
    - Server-side Condition > Type: **PL/SQL Function Body returning Boolean**

    - Server-side Condition > PL/SQL Function Body returning Boolean: **RETURN :APP\_PAGE\_ID = 5;**

    Click **Create**.

    !["Click App Builder"](images/ticket-rag-2.png "")



## Task 3: Enable Ticket Chat Assistant with RAG Source

1. From the top-right corner, click **Edit Page 3**.

    >Note: Page number may vary depending on your application.

    !["Click App Builder"](images/edit-page5.png "")

2. In the Dynamic Action tab, select True Action **Show AI Assistant** and update the following:

    - Generative AI > Configuration: **Ticket AI Configuration**

    - Under Quick Actions:

        - Message 1: **List open high priority tickets**

        - Message 2: **Show tickets assigned to Agent Rita**

    Click **Save and Run**.

    !["Click App Builder"](images/ticket-conf-msg.png "")


4. In the app, click the **Ticket Assistant** button and click **List open high priority tickets**. The chat assistant will now return results using a RAG (Retrieval-Augmented Generation) source, ensuring that details are fetched only from the specified data source.

    !["App running"](images/view-ai-chat1.png "")

    !["chatbox example"](images/view-ai-chat2.png "")

## Summary

In this lab, you created a Ticket Chat Assistant by adding a button, configuring AI settings, and setting up a dynamic action, allowing users to interactively ask questions about customer support tickets.

## Acknowledgments

- **Authors** - Toufiq Mohammed, Principal Product Manager; Apoorva Srinivas, Principal Product Manager
- **Last Updated By/Date** - Apoorva Srinivas, Principal Product Manager, January 2026
