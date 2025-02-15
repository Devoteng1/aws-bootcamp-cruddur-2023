# Week 0 — Billing and Architecture

## Required Homework/Tasks

## Created Logical architectual Diagram in Lucid charts  

![logical Architecture](assets/logicaldiagramCrudder.png)
[[lucidChart](https://lucid.app/documents/view/e730cc85-0176-4c52-8acc-f213e74868df)](https://lucid.app/documents/view/e730cc85-0176-4c52-8acc-f213e74868df)

## Setup AWS CLI 

I have setup the AWS CLI both in the Gitpod workspace and the my local Desktop environment

In Gitpod, I used the below script to do the setup.
ON LINUX

- curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
- unzip awscliv2.zip
- sudo ./aws/install

![AWS CLI](assets/AWSCLIsetup.png)

## Created AWS Budget using the AWS CLI

AWS Budgets lets you set custom cost and usage budgets that alert you when your budget thresholds are exceeded (or forecasted to exceed).

Script to create AWS Budget using the AWS CLI
```
aws budgets create-budget \
    --account-id 820150472448 \
    --budget file://aws/json/budget.json \
    --notifications-with-subscribers file://aws/json/budget-notification-with-subscribers.json
```

Content of budget.json
```
{
    "BudgetLimit": {
        "Amount": "1",
        "Unit": "USD"
    },
    "BudgetName": "Free Cloud Bootcamp",
    "BudgetType": "COST",
    "CostFilters": {
        "TagKeyValue": [
            "user:Key$value1",
            "user:Key$value2"
        ]
    },
    "CostTypes": {
        "IncludeCredit": true,
        "IncludeDiscount": true,
        "IncludeOtherSubscription": true,
        "IncludeRecurring": true,
        "IncludeRefund": true,
        "IncludeSubscription": true,
        "IncludeSupport": true,
        "IncludeTax": true,
        "IncludeUpfront": true,
        "UseBlended": false
    },
    "TimePeriod": {
        "Start": 1477958399,
        "End": 3706473600
    },
    "TimeUnit": "MONTHLY"
}
```
Content of budget-notification-with-subscribers.json
```
[
    {
        "Notification": {
            "ComparisonOperator": "GREATER_THAN",
            "NotificationType": "ACTUAL",
            "Threshold": 80,
            "ThresholdType": "PERCENTAGE"
        },
        "Subscribers": [
            {
                "Address": "lovebergers@gmail.com",
                "SubscriptionType": "EMAIL"
            }
        ]
    }
]
```
![budgetscreen](assets/budgetscreen.png)
 
![budgetsAWSCLI](assets/createbudget_AWSCLI.png)

## Created AWS Simple Notification Service (SNS) Topic using AWS CLI

Amazon Simple Notification Service (SNS) sends notifications two ways, A2A and A2P. A2A provides high-throughput, push-based, many-to-many messaging between distributed systems, microservices, and event-driven serverless applications

![snstopic](assets/snstopicscreen.png)

### Subscribed to the SNS topic

![snstopic](assets/subscribe.png)

### Recieved Notification

![snstopic](assets/subscribetotopic.png)

## Created Billing Alarm

A CloudWatch Alarm that triggers the AWS bill reaches the specified threshold

![snstopic](assets/BillingAlarm.png)


