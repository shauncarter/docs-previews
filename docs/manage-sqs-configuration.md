## Overview

When using Matillion ETL as part of a larger process, the best way to initiate an orchestration job is to use [Amazon Simple Queue Service](https://aws.amazon.com/sqs/){:target="_blank"} (SQS). Other applications can read messages posted to an SQS queue and perform further processing.

You can put messages onto an SQS queue using [Python](#send-messages-using-python) or the [SQS Message component](#send-messages-using-the-sqs-message-component).

---

## Setting up

1. To configure SQS for Matillion ETL, first create up to three SQS queues as described in [_Getting started with Amazon SQS_](http://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-getting-started.html#step-create-queue){:target="_blank"}.

2. In Matillion ETL, click **Project** → **Manage SQS Configuration**.

3. Complete the following fields in the **Manage SQS Configuration** dialog.

| Property | Description |
|---|---|
|Enable SQS| This turns on or off the sub-system that listens to SQS queues. Note: this is global, not for a particular project.|
|Credentials| Choose the credentials that you will be using to talk to SQS queues. An IAM user or Role will need the AmazonSQSFullAccess policy if you want to have a success or failure queue.|
|Region| The region where the queue exists in SQS.|
|Listen Queue| The name of the queue to listen for messages. These messages are in a set format as shown [below](#message-format).|
|Enable Success| Select this if you wish to place a message on an SQS queue when your orchestration job has completed.|
|Success Queue| The name of the success queue on which to place success messages.|
|Compress| When selected, the body of the message on the queue will be gzipped. Use this to avoid hitting [SQS limits](http://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSGettingStartedGuide/CreatingQueue.html){:target="_blank"}.|
|Enable Failure| Select this if you wish to place a message on an SQS queue when your orchestration job has failed.|
|Failure Queue| The name of the failure queue on which to place failure messages.|
|Compress| When selected, the body of the message on the queue will be gzipped. Use this to avoid hitting [SQS limits](http://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSGettingStartedGuide/CreatingQueue.html){:target="_blank"}.|

> #### Note
> The queues for success and failure can't be FIFO queues, as there is no property set for the message ID and message de-duplication ID.

4. Click **Test** to verify that the queues exist and can be read.

---

## Returned messages

The messages that are returned on the success or fail queues are in the following format:

```JSON
{  
   "type":"QUEUE_ORCHESTRATION",
   "groupName":"<the group name that was executed>",
   "projectName":"<the project name that was executed>",
   "versionName":"<the version name that was executed>",
   "environmentName":"<the version name that was executed>",
   "state":"SUCCESS|FAILED", 
   "enqueuedTime":<Time message placed on queue in unix epoc format>,
   "startTime":<Time orchestration job began in unix epoc format>,
   "endTime":<Time orchestration job ended in unix epoc format>,
   "message":<contains error messages where applicable>,
   "originator ID":"q_Queue",

   "tasks":[  <This is a list of tasks executed in the orchestration>
       {  
           "type":"VALIDATE_ORCHESTRATION",
           "jobName":"SimpleQueueJob",
           "componentName":"Start 0",
           "orchestrationJobName":"SimpleQueueJob",
           "orchestrationComponentName":"Start 0",
           "state":"SUCCESS",
           "rowCount":0,
           "startTime":1443526622364,
           "endTime":1443526622364,
           "message":""
       },
       {  
           "type":"VALIDATE_ORCHESTRATION",
           "jobName":"SimpleQueueJob",
           "componentName":"End Success 0",
           "orchestrationJobName":"SimpleQueueJob",
           "orchestrationComponentName":"End Success 0",
           "state":"SUCCESS",
           "rowCount":0,
           "startTime":1443526622365,
           "endTime":1443526622369,
           "message":""
       },
       {  
           "type":"EXECUTE_ORCHESTRATION",
           "jobName":"SimpleQueueJob",
           "componentName":"End Success 0",
           "orchestrationJobName":"SimpleQueueJob",
           "orchestrationComponentName":"End Success 0",
           "state":"SUCCESS",
           "rowCount":0,
           "startTime":1443526622369,
           "endTime":1443526622369,
           "message":""
       }
   ],
   "rowCount":0
}
```

---

## Send messages using Python

To put messages onto an SQS queue, you can adapt this Python snippet, or use any other AWS API at your disposal to achieve the same result.

```Python
import boto.sqs
import json
from boto.sqs.message import RawMessage

#connect to your region
conn = boto.sqs.connect_to_region("eu-west-1")

#create the queue to post messages
queue = conn.create_queue("QUEUE-NAME")

#set the queue to allow raw messages data
queue.set_message_class(RawMessage)

#prepare the message
p_message = {
 "created":"-",
 "group":"myGroup",
 "project":"myproject",
 "version":"default",
 "environment":"myEnv",
 "job":"myjob"
}

#prepare the message on the queue
message = queue.new_message(json.dumps(p_message))

#write the message to the queue
queue.write(message)
```

---

## Send messages using the SQS Message component

You can use the [SQS Message](/docs/2140977){:target="_blank"} component in an orchestration job to post a message to an SQS queue. You specify the message properties (such as **Queue Name** and **Region**) when you configure the component as part of a job. The message to be passed to the queue is written in plain text in the component's **Message** property. The message text can contain [variables](/docs/2037630){:target="_blank"} to be resolved at runtime, in the same way that other Matillion ETL components can use variables. The receiving queue must already exist so that you can select it when configuring the component.

The following example shows the SQS Message component configured to send a message with the text "This is a plain test message being sent to SQS":

![Configure SQS Message component](https://matillion-docs.s3-eu-west-1.amazonaws.com/images/2144265/manage-sqs-config-02.png)

---

## Message format

Messages are in a set format as follows.

```
{
  "group":"<Exactly matches the project group where your job resides>",
  "project":"<Exactly matches the project name where your job resides>",
  "version":"<Exactly matches the version Name>",
  "environment":"<Exactly matches the environment Name>",
  "job":"<Exactly matches the orchestration Job Name>",
  "variables":  {
               "<Name 1>": "<Value 1>",
               "<Name 2>": "<Value 3>"
           }
  "gridVariables" : {
"<GridVar Name>": [["<R1C1 Value>", "<R1C2 Value>"], ["<R2C1 Value>", "<R2C2 Value>"]]
           }
}
```

The `variables` and `gridVariables` fields are optional. Variables are passed to the orchestration job. Matching variable names must be declared in the project with default values set for each environment. If a variable is passed which isn't defined in the project, an error is logged in **Project** → **Task History**. Read the articles on [_Variables_](/docs/2037630){:target="_blank"} for more information.
