# Amazon DynamoDB

The Amazon DynamoDB integration allows you to monitor [Amazon DynamoDB](https://aws.amazon.com/dynamodb/)—a key-value NoSQL database.

Use the Amazon DynamoDB integration to collect metrics related to your Amazon DynamoDB databases.
Then visualize that data in Kibana, create alerts to notify you if something goes wrong, and reference metrics when troubleshooting an issue.

For example, you could use this data to visualize consumed read and write capacity units. You can then create alerts based on used or unused capacity, so that the relevant users can better scale their provisioned throughput capacity. This might mean they increase the capacity to provide more resources, or reduce capacity to save on costs.

## Data streams

The Amazon DynamoDB integration collects one type of data: metrics.

**Metrics** give you insight into the state of Amazon DynamoDB.
Metrics collected by the Amazon DynamoDB integration include the maximum number of read and write capacity units that can be used by an account, consume capacity units, throttle events, and more. See more details in the [Metrics reference](#metrics-reference).

## Requirements

You need Elasticsearch for storing and searching your data and Kibana for visualizing and managing it.
You can use our hosted Elasticsearch Service on Elastic Cloud, which is recommended, or self-manage the Elastic Stack on your own hardware.

Before using any AWS integration you will need:

* **AWS Credentials** to connect with your AWS account.
* **AWS Permissions** to make sure the user you're using to connect has permission to share the relevant data.

For more details about these requirements, see the **AWS** integration documentation.

## Setup

Use this integration if you only need to collect data from AWS DynamoDB.

If you want to collect data from two or more AWS services, consider using the **AWS** integration.
When you configure the AWS integration, you can collect data from as many AWS services as you'd like.

For step-by-step instructions on how to set up an integration, see the
{{ url "getting-started-observability" "Getting started" }} guide.

## Metrics reference

The `dynamodb` data stream collects DynamoDB metrics from AWS.
An example event for `dynamodb` looks like this:

{{event "dynamodb"}}

{{fields "dynamodb"}}