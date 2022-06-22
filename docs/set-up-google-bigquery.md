## Overview

This page is a guide to setting up your Google Cloud Platform (GCP) account to use [Google BigQuery](https://cloud.google.com/bigquery/docs/introduction#get-started-with-bigquery) as a destination within Matillion Data Loader.

---

## Prerequisites

- For security purposes, you may wish to set up a new Google Cloud Platform (GCP) account and project for use with Matillion Data Loader.
- Make sure you have access to a GCP project. You need permissions in the GCP project to create [Identity Access Management (IAM)](https://cloud.google.com/iam/docs/overview) services accounts.
- Make sure you have access to a Google Cloud Platform project within Google BigQuery.
- You need to connect to an IAM service account that has access to BigQuery, Cloud Storage, and your project.
- You need permissions to create a Cloud Storage bucket and a BigQuery dataset.
- You need administrative permission to a Matillion ETL for BigQuery instance that has billing enabled. It's recommended to have billing enabled while performing data loading processes even if you're using the free trial option.

---

## Enable the GCP project API
  
If you have sufficient access to enable the API, follow the steps below to enable the API in your own Google Cloud project:

1. Navigate to [APIs & Services](https://console.cloud.google.com/apis) in the Google Cloud console.
2. Click **Library** → **Private**. If you don't see an API listed, you don't have access to enable it.
3. Click the API you want to enable. Use the search field to filter out unwanted objects.
4. Enable the following APIs:
    - BigQuery API
    - Cloud Key Management Service (KMS) API (optional)
    - Cloud Pub Sub API (optional)
    - Cloud Resource Manager API
    - Cloud Storage API
    - Google Sheets API (if you want to use a Google Sheets data source).
5. In the page that displays information about the API, click **Enable**.

---

## Create a BigQuery dataset

To create a dataset:

1. Navigate to [Google BigQuery](https://console.cloud.google.com/bigquery).
2. In the **Explorer** panel, select the more button (three vertical dots) on your project and click **Create data set**.
3. Name the dataset in the **Data set ID** field.
4. Set a [dataset location](https://cloud.google.com/bigquery/docs/locations?_ga=2.169100577.-1068399664.1643908482). You can't change the dataset location once set.
5. Select **Enable table expiry** if you wish to set a maximum age of a table in days.
6. Click **Create DATA SET**.

You can now choose this data set in the dropdown list within the project, and the Dataset ID can be used in Matillion ETL and Data Loader.

---

## Creating Service Accounts

Matillion Data Loader requires you to set up an existing GCP project with Google BigQuery and GCP authentication. Authentication is achieved via service accounts in Google—an account within your GCP project used by virtual machines (VMs). A service account has assigned roles and permissions, and access keys.

To create a service account:

1. Make sure you have the BigQuery API enabled.
2. Navigate to [IAM & Admin: Service Accounts](https://console.cloud.google.com/iam-admin/serviceaccounts) in the Google Cloud console.
3. Click **+ Create service account**
4. Enter a service account name to display in the Google Cloud console.
5. The Google Cloud console generates a service account ID based on this name. Edit the ID if necessary. You can't change the ID later.
6. Optional: Enter a description of the service account.
7. Click **Continue** to progress to part 2, **Grant this service account access to the project (optional)**.
8. Optional: Choose one or more IAM roles to grant to the service account on the project.
9. Click **Continue** to progress to part 3, **Grant users access to this service account (optional)**.
10. Optional: In the **Service account users role** field, add members that can impersonate the service account.
11. Optional: In the **Service account admins role** field, add members that can manage the service account.
12. Click **Done** to create the service account. 

Locate your new service account in **Service accounts**.

---

## Add roles to a service account

1. Navigate to [IAM & Admin: IAM](https://console.cloud.google.com/iam-admin) in the Google Cloud console.
2. Click the current project, and then click **Open**.
3. In the **Permission** tab, locate your service account (Principal) and click the edit button (pencil).
4. Add a role.
5. Click **+ ADD ANOTHER ROLE** if applicable.
6. Click **SAVE**.

Ensure these roles are present:

* BigQuery Admin
* Project Viewer
* Storage Admin

---

## Link a service account to a Cloud Billing account

Your GCP project must have billing enabled. You must define a [Cloud Billing account](https://cloud.google.com/billing/docs/concepts) outside a project and then you must apply the Cloud Billing account to a project at your discretion. 

1. Navigate to [Billing](https://console.cloud.google.com/billing) in the Google Cloud console.
2. Select a Cloud Billing account for your chosen project in the list.
   - To learn more about changing a Cloud Billing account for projects, read [_Enable, disable, or change billing for a project _](https://cloud.google.com/billing/docs/how-to/modify-project).
   - To learn how to create a Cloud Billing account, [_Create, modify, or close your self-serve Cloud Billing account _](https://cloud.google.com/billing/docs/how-to/manage-billing-account).

---

## Access keys

Service accounts use keys to access services. You need a key to configure your Matillion ETL and Data Loader instances.

The access key format is below:

```JSON
{
 "type": "service_account",
 "project_id": "abcde",
 "private_key_id": "",
 "private_key": "",
 "client_email": "abcde@appspot.gserviceaccount.com",
 "client_id": "XXXXXXXXXXXXX",
 "auth_uri": "https://accounts.google.com/o/oauth2/auth",
 "token_uri": "https://accounts.google.com/o/oauth2/token",
 "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
 "client_x509_cert_url": "https://www.googleapis.com/robot/v1/metadata/x509/abcde%40appspot.gserviceaccount.com"
}
```

To add an access key in GCP:

1. Navigate to [IAM & Admin: Service Accounts](https://console.cloud.google.com/iam-admin/serviceaccounts) in the Google Cloud console.
2. Locate your service account and in the **Actions** column, click the more button (three vertical dots).
3. Click **Manage keys**
4. Click **ADD KEY** → **Create new key** → set the radio button to **JSON** and click **CREATE**.
5. Your browser begins the downloading of the key to your computer.

---

## Cloud Storage bucket

To create a new Cloud Storage bucket:

1. Log in to the [Google Cloud console](https://console.cloud.google.com/storage/) at the Cloud Storage product.
2. Click **CREATE BUCKET**
3. Read Google's [_Create storage buckets_](https://cloud.google.com/storage/docs/creating-buckets) to learn how to set up your new bucket.
