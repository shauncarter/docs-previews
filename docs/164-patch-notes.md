## Overview

Below, you can find release notes for Matillion ETL version 1.64.x

---

## Matillion ETL version 1.64.7 (major release)

June 21, 2022

### Tech notes

- [Tech note - Shopify Query versioning](tech-note-shopify-query-versioning-164)
- [Tech note - Splunk Query versioning](tech-note-splunk-query-versioning-164)

---

### New features and improvements

#### All platforms

- Versioned the [Shopify Query](/docs/2950308) component (deprecated the component and replaced with a new version of Shopify Query component).
- Versioned the [Splunk Query](/docs/2970256) component (deprecated the component and replaced it with a new version of the Splunk Query component).
- Updated the [Gmail Query](/docs/2887499) component to include a new parameter, **Data Schema**. Users can set this to either `IMAP` or `REST`.
- Updated the [Calculator](/docs/1991925) component to include a grid variable dialog as an alternative to the expression editor.
- Updated [Manage Schedules](/docs/2103629) dialog. When you click into a schedule's **Task Info**, a separate **Task Info** dialog opens. Click **OK** to close this **Task Info** dialog and return to **Manage Schedules**.
- NULL values in Matillion ETL now display as italicized, capitalized, and with a grey text color (#757575). This change is to avoid confusion where a non-NULL value is Null. For example, if a person's surname is literally Null, for example, Jane Null or Tom Null.
- Updated [Zero Copy Clone](/docs/2477766) in the following ways: 
    - Added **Run job in clone** functionality. You can run any transformation or orchestration job using a cloned database. This lets you to test the job on data that mirrors that in your production environment, without affecting your production data. 
    - Improved error messages in the **clone environment and database** dialog.
- New [Shared Job Git API endpoints](/docs/5971755#shared-jobs) are available including:
    - Switch commit
    - Delete branch
    - Get state (logs)
    - Create branch (on current commit)
    - Get remote (URL)
- The **Payload** field in **Manage Error Reporting** is no longer editable when using a payload template that isn't `[Custom]`. These payloads are now read-only. Use **Manage Webhook Payloads** to edit payloads.

#### Redshift

The Avro file format is now available for the following components for Matillion ETL for Redshift:

- [Create External Table](/docs/2827024)
- [External Table Output](/docs/2842286)
- [Rewrite External Table](/docs/2827049)

---

### Deprecation

#### All platforms

- The Google AdWords Query component is now disabled. This component was deprecated in version 1.62.7.

---

### Bug fixes

#### All platforms

- Fixed an issue where maliciously altered exported jobs could be used for a Cross-Site Scripting (XSS) attack on import.
- Fixed an issue to make sure that Excel Query components running in iterators are consistently associated with their files.
- Updated Snowflake JDBC driver to latest version (3.13.18). This corrects a proxy regression, among other improvements.
- Fixed an issue where the API Extract component and Manage Extract Profiles wizard didn't pass a correct bearer token when `Authentication Type = Bearer Token`.
- Fixed an issue where additional parameters didn't pass in the request to get the Access Token when configuring an API OAuth, when Grant Type = Client Credentials.

#### Redshift, Synapse

- Fixed an issue where the Create External Table component parameter Table Metadata didn't open successfully when the value of the data type in the dialog was `NULL`.

#### Delta Lake on Databricks

- Fixed an issue where row counts were reported as `0` when Query components had executed despite the actual number of staged rows displaying correctly during job execution.
- Fixed an issue where certain components would not present metadata in the correct casing when using aliasing on columns.

---

### Driver updates

- Bing Search API driver updated. 20.0.7662.0 → 21.0.8152.0
- Dynamics 365 API driver updated. 19.0.7156.0 → 21.0.8137.0
- Elasticsearch API driver updated. 20.0.7662.0 → 21.0.8137.0
- Email API driver updated. 19.0.7354.0 → 21.0.8137.0
- Excel API driver updated. 21.0.7829.0 → 21.0.8137.0
- HubSpot API driver updated. 21.0.7907.0 → 21.0.8130.0
- Google BigQuery API driver updated. 21.0.7930.0 → 21.0.8152.0
- LDAP API driver updated. 15.0.6121.0 → 21.0.8137.0
- Sage Intacct API driver updated. 19.0.7121.0 → 21.0.8137.0
- ServiceNow API driver updated. 21.0.7930.0 → 21.0.8137.0
- Shopify API driver updated. 19.0.7485.0 → 21.0.8137.0
- Splunk API driver updated. 19.0.7216.0 → 21.0.8137.0
- Square API driver updated. 21.0.7867.0 → 21.0.8137.0
- SurveyMonkey API driver updated. 20.0.7662.0 → 21.0.8137.0
- YouTube Analytics API driver updated. 20.0.7628.0 → 21.0.8137.0
- Zoho CRM API driver updated. 20.0.7662.0 → 21.0.8137.0
