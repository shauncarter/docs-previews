## Overview

This page is a guide to adding your ETL agent credentials to AWS Secrets Manager.

---

## Locate your ETL agent credentials

1. Log in to [Matillion Hub](https://www.hub.matillion.com/).
2. Click **Platform Navigation** and choose **Matillion Start**.
3. Choose **Manage ETL Agents**.
4. Select an ETL agent. If you haven't created one yet, read [_Create an ETL agent_](/hub/docs/create-an-etl-agent).
5. In **Agent details**, scroll down to **Credentials**.
6. Click **Reveal credentials**.

---

## Add your credentials to AWS Secrets Manager

1. Log in to the [AWS Console](https://aws.amazon.com/console/).
2. Once logged in, type "Secrets Manager" in the search bar and click **Secrets Manager**.
3. Click **Store a new secret**.
4. Choose the tile labelled **Other type of secret**.
5. Add two key:value pairs:

|Key|Value|
|---|---|
|client_id|The value of the client ID located via **Matillion Start** → **Manage ETL Agents** → select an ETL agent → **Agent Details** → **Credentials** → **Reveal credentials**.|
|client_secret|The value of the client secret located via **Matillion Start** → **Manage ETL Agents** → select an ETL agent → **Agent details** → **Credentials** → **Reveal credentials**.|

6. Click **Next**.
7. Name the secret and provide a secret description. Click **Next**.
8. Click **Next** again unless you wish to configure rotation settings.
9. Review the secret and click **Store**. You'll return to **Secrets**. Refresh the page.

---

## Retrieve the ARN of your new secret

1. While in the **Secrets** dashboard of AWS Secrets Manager, click the name of your new secret.
2. In the **Secret details** container, copy the **Secret ARN** and save this value for later to reference it in the task definition.
