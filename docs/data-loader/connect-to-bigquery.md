## Overview

Connect to Google BigQuery via Matillion Data Loader and use it as your destination for batch-loading a pipeline.

---

## Prerequisites

Read [_Set up Google BigQuery_](/mdl/docs/set-up-google-bigquery) to make sure you are ready to connect to your Google BigQuery destination.

---

## Connect to Google BigQuery

Click **Add GCP credential** to add a new set of credentials to connect to Google Cloud Platform (GCP).

|Property|Description|
|---|---|
|GCP credential label|A name for the new GCP credentials.|
|Access key ID| A JSON file with a working GCP access key. Drag the JSON file into the box, or click anywhere in the box to upload.|

Click **Test and save** to confirm the credentials work, save them, and return to **Connect to Google BigQuery**.

|Property|Description|
|---|---|
|GCP credential|A working Google Cloud Platform credential.|
|Destination label|A descriptive name for the Google BigQuery destination.|

---

## Configure Google BigQuery

|Property|Description|
|---|---|
|Project|A working Google Cloud project. To learn more, read [_Creating and managing projects_](https://cloud.google.com/resource-manager/docs/creating-managing-projects).|
|Dataset|Datasets are top-level containers stored within projects for organizing and controlling access to your tables and views. To learn more, [_Introduction to datasets_](https://cloud.google.com/bigquery/docs/datasets-intro).|
|Cloud storage area|A working Cloud Storage bucket to store data inside. To learn more, read [_Create storage buckets_](https://cloud.google.com/storage/docs/creating-buckets).|
|Table prefix|An optional prefix to add to your destination table.|

When you are happy with your configuration, click **Continue**.