## Overview

MongoDB is a source-available cross-platform document-oriented database program. With Matillion Data Loader, you can replicate and load your source data into your target destination.

**Schema Drift Support**: yes—read [_Schema Drift_](/mdl/docs/3118484) to learn more.

Return to any page of this wizard by clicking **Previous**.

Click **X** in the upper-right of the UI and then click **Yes, discard** to close the pipeline creation wizard.

---

## Create pipeline

1. In Matillion Data Loader, click **Add pipeline**.
2. Choose **MongoDB** from the grid of data sources.
3. Choose **Batch Loading**.

---

## Connect to MongoDB

Configure the MongoDB database connection settings, specifying the following:

|Property|Description|
|---|---|
|Connection URL|The server IP or DNS address of your MongoDB server endpoint.|
|Database|The name of your MongoDB database.|
|Username| A valid login username for your MongoDB database server.|
|Password| A managed entry representing your MongoDB database login password. Choose an existing password from the dropdown menu or click **Manage** and then click **Add new password** to configure a new managed password entry. Give the password a label, which is what you can see in the password dropdown menu, and then input the value of the password. Read [_Manage Passwords_](/mdl/docs/2054960) to learn more.|
|Advanced settings|Additional JDBC parameters or connection settings. Click **Advanced settings** and then choose a parameter from the dropdown menu and enter a value for the parameter. Click **Add parameter** for each extra parameter you want to add. Read [_Connection String URI Format_](https://www.mongodb.com/docs/manual/reference/connection-string/) for reference of MongoDB connection options.|

!!! Note

    - The advanced connection settings `AuthSchema:SCRAM-SHA-1` and `AuthDatabase:admin` will be defined by default.
    - If your source is an Atlas cluster, you must also specify the following advanced connection settings:
        - `UseSSL: true`
        - `SlaveOK: true`
    - You may also need to set `ReplicaSet` depending on your configuration: `ReplicaSet=<your replica set name>`. For example: `cluster0-shard-00-01-test.mongodb.net:27017`, `cluster0-shard-00-02-test.mongodb.net:27017`

Click **Test and Continue** to test your settings and move forward. You can't continue if the test fails for any reason.

---

## Flatten your objects

Set the **Flatten objects** dropdown field to either **Yes** or **No**. The default is **No**.

When **Yes**, Matillion Data Loader flattens and converts a nested data layer object into a new object with only one layer of key:value pairs.

---

## Choose tables

Choose any tables you wish to include in the pipeline. Use the arrow buttons to move tables to the **Tables to extract and load** listbox and then reorder any tables with click-and-drag. Additionally, select multiple tables using the `SHIFT` key.

Click **Continue with X tables** to move forward.

---

## Configure columns

Choose the columns from each table to include in the pipeline. By default, Matillion Data Loader selects all columns from a table.

Click **Configure** on a table to open **Configure table**. This dialog lists columns in a table and the data type of each column. Additionally, you can set a primary key and assign an incremental column state to a column.

!!! Note

    - **Primary Key** columns should represent a true `PRIMARY KEY` that uniquely identifies each record in a table. Composite keys work, but you must specify all columns that compose the key. Based on the primary key, this won't permit duplicate records. Jobs in Matillion ETL may fail or replicate data incorrectly if these rules aren't applied.
    - Make sure an **Incremental column** is a true change data capture (CDC) column that can identify whether there has been a change for reach record in the table. This column should be a **TIMESTAMP/DATE/DATETIME** type or an **INTEGER** type representing a date key or **UNIX** timestamp.

Click **Add and remove columns** to modify a table before a load. Use the arrow buttons to move columns _out of_ the **Columns to extract and load** listbox. Order columns with click-and-drag. Select multiple columns using `SHIFT`.

Click **Done adding and removing** to continue and then click **Done**.

Click **Continue** once you have configured each table.

---

## Choose destination

1. Choose an existing destination or click **Add a new destination**.
2. Select a destination from Snowflake, Amazon Redshift, or Google BigQuery.

---

## Set frequency

|Property|Description|
|---|---|
|Pipeline name|A descriptive label for your pipeline. This is how the pipeline appears on the pipeline dashboard and how Matillion Data Loader refers to the pipeline.|
|Sync every|The frequency at which the pipeline should sync. Day values include 1—7. Hour values include 1—23. Minute values include 5—59. The input is also the length of delay before the first sync.|

Currently, you can't specify a start time.

Once you are happy with your pipeline configuration, click **Create pipeline** to complete the process and add the pipeline to your dashboard.
