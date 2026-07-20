# Lab 4: Insert Realistic Data

## Introduction

Create enough data to develop and test the APEX app. 

Estimated Time: 5 minutes

### Objectives

In this lab, you will:

- Upload the DML script into SQL scripts.
- Run the script to innsert TMS data into the relevant tables.

## Task 1: Upload the SQL script to Insert Data

1. In the SQL Workshop, navigate to **SQL Scripts**.

    ![SQL script](images/nav-sql-script.png ' ')

2. Click **Upload**.

    ![SQL script](images/upload.png ' ')

3. Select the [tms_sample_data.sql](files/tms_sample_data.sql) file. For Script Name, enter **tms_sample_data** and click **Upload**.

    ![SQL script](images/tms_sample_upload.png ' ')

## Task 2: Run the SQL script

1. Run the **tms_sample_data** script.

    ![SQL script](images/run-script.png ' ')   

2. Click **Run**.

    ![SQL script](images/run-again.png ' ')

3. Verify that the script ran without ay errors.

    ![SQL script run result](images/run-result.png ' ')

<!--## Task 1: Open Data Generator

1. In SQL Workshop, select **Utilities**, then select **Data Generator**.

    ![Data Generator](images/select-data-generator.png ' ')

2. Click **Create Blueprint**.
    ![Create Blueprint](images/create-blueprint.png ' ')

3. Select **Use Existing Tables**.
    ![Create Tables Blueprint](images/use-existing-tables.png ' ')

4. For Blueprint Name, enter **TMS Blueprint**. Select all the tables that begin with `TMS_`. Then, click **Create Blueprint**.

    ![Data Generator with TMS tables selected.](images/data-generator-tms-tables.png ' ')

## Task 2: Set row counts

1. Use these approximate row counts for the initial data set.

    - `TMS_DEPARTMENTS`: Number of Rows: 8
    - `TMS_JOBS`: Number of Rows: 10
    - `TMS_JOB_REQUISITIONS`: Number of Rows: 15
    - `TMS_CANDIDATES`: Number of Rows: 60
    - `TMS_INTERVIEW_STAGES`: Number of Rows: 25
    - `TMS_OFFERS`: Number of Rows: 10
    - `TMS_EMPLOYEES`: Number of Rows: 20

    The screenshot shows setting the Number of Rows for one of the tables: **TMS_CANDIDATES**. 

    Click **Save**.

    ![number of rows](images/num-of-rows.png ' ')


## Task 3: Generate data

1. Click **Generate Data**. 
    ![generate data](images/generate-data.png ' ')

2. In the Generate Blueprint Data dialog, for Action select **Insert into Database**. Then, click **Insert Data**.

    ![insert data](images/insert-data.png ' ')

2. Review the success message before closing the dialog.

    ![review success message](images/success-message.png ' ')

3. Navigate to the Object Browser and select a table such as `TMS_CANDIDATES`. Switch to the **Data** tab and review the inserted data.

    ![Object Browser](images/review-data.png ' ') -->

## Acknowledgements

* **Author** - Apoorva Srinivas, Principal Product Manager; Roopesh Thokala, Principal Product Manager
* **Last Updated By/Date** - Apoorva Srinivas, Principal Product Manager, July 2026
