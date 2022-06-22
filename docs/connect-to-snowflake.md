## Overview

Connect to Snowflake via Matillion Data Loader and use it as your destination for batch-loading a pipeline.

---

## Prerequisites

- `ACCOUNTADMIN` role privileges in Snowflake, or privileges equivalent to the `SECURITYADMIN` and `SYSADMIN` roles.

---

## Connect to Snowflake

|Property|Description|
|---|---|
|Destination label|A name for the destination.|
|Account|Your Snowflake account. Your account might contain the name, region, and cloud provider.|
|Username|Your Snowflake username.|
|Password/Private key|A managed entry representing your Snowflake login password. Choose an existing password from the dropdown menu or click **Manage** and then click **Add new password** to configure a new managed password entry. Give the password a label, which is what you can see in the password dropdown menu, and then input the value of the password. Read [_Manage Passwords_](/mdl/docs/2054960) to learn more.|
|Advanced settings|Additional JDBC parameters or connection settings. Click **Advanced settings** and then choose a parameter from the dropdown menu and enter a value for the parameter. Click **Add parameter** for each extra parameter you want to add. Read [_Configuration Properties_](https://docs.snowflake.com/en/user-guide/jdbc-configure.html) for reference of Snowflake connection options.|

Click **Test and continue** to test your settings and move forward. You can't continue if the test fails for any reason.

---

## Configure Snowflake

Set up the Snowflake destination. Your login connection to Snowflake affects which roles, warehouses, databases, and schemas you can choose.

|Property|Description|
|---|---|
|Role|An entity with privileges. Read [_Overview of Access Control_](https://docs.snowflake.com/en/user-guide/security-access-control-overview.html) to learn more.|
|Warehouse|A Snowflake warehouse. Read [_Overview of Warehouses_](https://docs.snowflake.com/en/user-guide/warehouses-overview.html) to learn more.|
|Target database|A Snowflake database. Read [_Database, Schema, and Share DDL_](https://docs.snowflake.com/en/sql-reference/ddl-database.html) to learn more.|
|Target schema|A Snowflake schema to load the table into. Read [_Database, Schema, and Share DDL_](https://docs.snowflake.com/en/sql-reference/ddl-database.html) to learn more.|
|Table prefix|Add an optional prefix to your destination table. This field is empty by default.|
