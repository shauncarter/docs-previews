## Overview

This page is a guide to manually installing an ETL agent into AWS Fargate.

---

## Prerequisites

- 
- Each time you click **Create** in AWS, a coloured banner will appear at the top of the AWS UI.
    - Blue indicates the creation of a resource is in-progress.
    - Green indicates the creation of a resource has completed.
    - Red indicates the creation of a resource has failed.

---
## Security groups

1. Log in to the [AWS Console](https://aws.amazon.com/console/).
2. Once logged in, type `security groups` in the search bar.
3. In the **Features** list, select **Security Groups|EC2 feature**.
4. Choose **Create security group**.

Complete the following fields:

|Property|Description|
|---|---|
|Security group name|Add the following: `matillion-etl-agent-<agentID>` Your Agent ID is available at **Agent environment variables** in Matillion Hub → **Matillion ETL Agents**.|
|Description|Add the following description: `Matillion ETL agent security group for agent ID <agentID>`. Alternatively, add a description of your choice.|
|VPC|Select your VPC.|
|Inbound rules|Add any inbound rules. None are required by default.|
|Outbound rules|`0.0.0.0/0`|
|Tags|It's recommended to add a tag where **Key** = `matillion-agent-id` and **Value** = `<agentID>`.|

Click **Create security group** to confirm creation. On successful creation of the security group, you will be redirected to the new security group's dashboard. Please make a note of your **Security group ID**.

---

## Log groups

1. In the AWS console, type `CloudWatch` in the search bar and navigate to AWS CloudWatch.
2. In the left-hand menu, choose **Logs** → **Log groups**.
3. Click **Create log group**.

Complete the following fields:

|Property|Description|
|---|---|
|Log group name|Add the following: `/ecs/matillion-etl-agent/agentID`.|
|Retention setting|Select a retention setting. It's recommended to choose **1 month (30 days)** from the dropdown.|
|KMS key ARN - optional|Not required.|
|Tags|It's recommended to add a tag where **Key** = `matillion-agent-id` and **Value** = `<agentID>`.|

Click **Create** to confirm creation of the log group. On successful creation of the log group, you will be redirected to **Log groups**.

---

## Cluster

1. In the AWS console, type `Elastic Container Service` in the search bar and choose that service.
2. Click **Get started** or **Clusters** if this is your first time using this service.
3. Click **Create Cluster**.

---

## Cluster configuration

|Property|Description|
|---|---|
|Cluster name|Add the following: `matillion-etl-agent-<agentID>`|
|VPC|Select your VPC.|
|Subnets|Optional. Choose subnets where your tasks will run.|
|Use Container Insights|Toggle this to **On**.|
|Tags|It's recommended to add a tag where **Key** = `matillion-agent-id` and **Value** = `<agentID>`.|

Click **Create** to confirm creation of the cluster. On successful creation of the cluster, you will be redirected to **All Clusters**.

---

## Task definitions



1. In the AWS console, type `Elastic Container Service` in the search bar and choose that service.
2. In the left-hand menu, click **Task definitions**.
3. Click **Create new task definition**.

Complete the following fields:

**Task definition configuration**

|Property|Description|
|---|---|
|Task definition family|Add the following: `matillion-etl-agent-<agentID>`. This must be unique—two task definitions can't share a name.|

**Container - n**

|Property|Description|
|---|---|
|Name|`matillion-etl-agent`|
|Image URI|Copy and paste your **Agent Image URI** from **Agent details**.|
|Port mappings|Remove any existing entries.|

In **Environment Variables** under **Add individually**, add the following environment variables using the values in your **Agent details** page in Matillion Hub:

|Property|Description|
|---|---|
|AGENT_ID|Your AGENT_ID value.|
|ACCOUNT_ID|Your ACCOUNT_ID value.|
|OAUTH_SECRET_REF|The Amazon resource number (ARN) of an AWS Secrets Manager secret that contains the `client_id` and `client_secret` located via **Matillion Start** → **Manage ETL Agents** → **Agent Details** → **Credentials** → **Reveal credentials**. To learn more about this process, read [_Add ETL agent credentials to AWS Secrets Manager_](/hub/docs/add-etl-agent-credentials-to-aws-secrets-manager).|
|OAUTH_DOMAIN|Your OAUTH_DOMAIN value.|
|extensionLibraryLocation|Your EXTENSION_LIBRARY_LOCATION value.|
|agentGatewayURI|Your AGENT_GATEWAY_URI value.|

Click **Next**.

---
### Configure environment, storage, monitoring, and tags

|Property|Description|
|---|---|
|App environment|Choose **AWS Fargate (serverless)**|
|CPU|Choose **1 vCPU**.|
|Memory|Choose **2 GB**.|
|Task role|Choose `ecsTaskExecutionRole`.|

Scroll down to **Monitoring and logging - optional**.

If the naming of components has been consistent so far, the **awslogs-group** value should equal the log group that was previously created (note the use of the `/` preceding the ID in the original **Log group** name). Otherwise, select the log group created earlier. Delete the **aws-create-group** entry by clicking **Remove**.

Once again, add a tag where **Key** = `matillion-agent-id` and **Value** = `<agentID>`.

Click **Next**. Review your settings and if you're happy, click **Create**. You will receive a blue banner at the top of the page explaining that AWS is currently creating the task definition. This banner will turn green upon completion.

---

## Service

1. In your newly created task definition, click the **Deploy** dropdown button and then click **Create service**.
2. In the **Choose a cluster** field, choose the cluster you created earlier. 

In **Deployment configuration**, complete the following fields:

|Property|Description|
|---|---|
|Service name|Add the following: `matillion-etl-agent-<agentID>`.|
|Desired tasks|Use the default value of `1`.|

In **Deployment options**, set both **Min running tasks** and **Max running tasks**. The max must be greater than the min.

In **Networking**, under **Security group name**, locate the security group you created earlier and select it. Remove any other security groups if they are not required.

Ensure that **Public IP** is toggled to **Enabled**, unless you are using Network Address Translation.

As in previous sections, add a tag where **Key** = `matillion-agent-id` and **Value** = `<agentID>`.

Click **Deploy**.

Once the deployment has finished, your ETL agent will be running.
