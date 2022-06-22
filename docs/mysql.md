## Overview

MySQL is an open-source relational database used to store custom data in-house. With Matillion Data Loader, you can replicate and load your source data into your target destination.

**Schema Drift Support**: yes—read [_Schema Drift_](/mdl/docs/3118484) to learn more.

Return to any page of this wizard by clicking **Previous**.

Click **X** in the upper-right of the UI and then click **Yes, discard** to close the pipeline creation wizard.

___

## Prerequisites

- Your MySQL database server must be running.
- Enable TCP/IP protocols with the TCP port set to `3306`.
- You must have access to your MySQL database host's IP address or domain.
- Make sure the MySQL database users has `SELECT` privileges.

:::info
You must have permission to access your MySQL database resources.
:::

___

## Create pipeline

1. In Matillion Data Loader, click **Add pipeline**.
2. Choose **MySQL** from the grid of data sources.
3. Choose **Batch Loading**.

___

## Connect to MySQL

Configure the MySQL database connection settings, specifying the following:

| Property | Description |
|---|---|
|Server address| The URL required to connect to the MySQL database server.|
|Port|The required port number to connect to the MySQL database server. The default value is `3306`.|
|Database name| The name of the MySQL database you want to connect to.|
|Username| A valid login username for the MySQL database server.|
|Password| A managed entry representing your MySQL database login password. Choose an existing password from the dropdown menu or click **Manage** and then click **Add new password** to configure a new managed password entry. Give the password a label, which is what you can see in the password dropdown menu, and then input the value of the password. Read [_Manage Passwords_](/mdl/docs/2054960) to learn more.|
|Advanced settings|Additional JDBC parameters or connection settings. Click **Advanced settings** and then choose a parameter from the dropdown menu and enter a value for the parameter. Click **Add parameter** for each extra parameter you want to add. Read [_Configuration Properties_](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-reference-configuration-properties.html) for reference of MySQL connection options.|

Click **Test and Continue** to test your settings and move forward. You can't continue if the test fails for any reason.
___

:::error
If you encounter an error where zeroed dates are causing pipelines to fail with an error such as below:

`Value '0000-00-00' can not be represented as java.sql.Date`

or:

`Value '0000-00-00 00:00:00' can not be represented as java.sql.Timestamp`

You can solve this error by selecting the `zeroDateTimeBehaviour` parameter and assigning a value of `convertToNull`.
:::

___

## Choose tables

Choose any tables you wish to include in the pipeline. Use the arrow buttons to move tables to the **Tables to extract and load** listbox and then reorder any tables with click-and-drag. Additionally, select multiple tables using the `SHIFT` key.

Click **Continue with X tables** to move forward.
___

## Configure columns

Choose the columns from each table to include in the pipeline. By default, Matillion Data Loader selects all columns from a table.

Click **Configure** on a table to open **Configure table**. This dialog lists columns in a table and the data type of each column. Additionally, you can set a primary key and assign an incremental column state to a column.

:::info
- **Primary Key** columns should represent a true `PRIMARY KEY` that uniquely identifies each record in a table. Composite keys work, but you must specify all columns that compose the key. Based on the primary key, this won't permit duplicate records. Jobs in Matillion ETL may fail or replicate data incorrectly if these rules aren't applied.
- Make sure an **Incremental column** is a true change data capture (CDC) column that can identify whether there has been a change for reach record in the table. This column should be a **TIMESTAMP/DATE/DATETIME** type or an **INTEGER** type representing a date key or **UNIX** timestamp.
:::

Click **Add and remove columns** to modify a table before a load. Use the arrow buttons to move columns _out of_ the **Columns to extract and load** listbox. Order columns with click-and-drag. Select multiple columns using `SHIFT`.

Click **Done adding and removing** to continue and then click **Done**.

Click **Continue** once you have configured each table.

___

## Choose destination

1. Choose an existing destination or click **Add a new destination**.
2. Select a destination from Snowflake, Amazon Redshift, or Google BigQuery.

___

## Set frequency

|Property|Description|
|---|---|
|Pipeline name|A descriptive label for your pipeline. This is how the pipeline appears on the pipeline dashboard and how Matillion Data Loader refers to the pipeline.|
|Sync every|The frequency at which the pipeline should sync. Day values include 1—7. Hour values include 1—23. Minute values include 5—59. The input is also the length of delay before the first sync.|

Currently, you can't specify a start time.

Once you are happy with your pipeline configuration, click **Create pipeline** to complete the process and add the pipeline to your dashboard.
