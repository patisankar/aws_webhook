# aws_webhook
## Context - Sending Webhooks on AWS

The application takes the change data capture event for DynamoDB streams and uses EventBridge Pipes and API destinations to send the event to an external endpoint

DynamoDB Table: Stores incoming data.​

EventBridge Pipe: Connects the DynamoDB stream to an EventBridge API Destination.​

API Destination: Specifies the external HTTP endpoint to send events to.​

Connection: Manages authentication for the API Destination.

## Amazon EventBridge Pipes

https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-pipes.html .

It connects source to targets

Amazon EventBridge event patterns

https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-event-patterns.html 



Chances are you won't want to process every single event that gets delivered to a given event bus or pipe. Rather, you'll likely want to select a subset of all the events delivered, based on the source of the event, the event type, and/or attributes of those events.

For event buses, you can specify an event pattern for each rule you create for the bus. In this way, you can select which events to send to specific targets. Event patterns for event buses can match against the event source, event metadata, and/or event detail values.

the event pattern includes fields about the event--source and detail-type--as well as a field from the event body--state.

{
  "source": ["aws.ec2"],
  "detail-type": ["EC2 Instance State-change Notification"],
  "detail": {
    "state": ["terminated"]
  }
}

npm install -g @mhlabs/evb-cli

https://github.com/mhlabs/evb-cli 

https://eventbridge-transformer.vercel.app/ 

## DynamoDB Streams

Data retention limit for DynamoDB Streams

All data in DynamoDB Streams is subject to a 24-hour lifetime. You can retrieve and analyze the last 24 hours of activity for any given table. However, data that is older than 24 hours is susceptible to trimming (removal) at any moment.

If you disable a stream on a table, the data in the stream continues to be readable for 24 hours. After this time, the data expires and the stream records are automatically deleted. There is no mechanism for manually deleting an existing stream. You must wait until the retention limit expires (24 hours), and all the stream records will be deleted

For more information about the KCL, see the Developing consumers using the Kinesis client library in the Amazon Kinesis Data Streams Developer Guide.

