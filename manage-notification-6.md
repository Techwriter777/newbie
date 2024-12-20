# Manage Notification

## Introduction

Monitoring updates of your CI/CD pipelines, such as their triggers, successes, and failures, can be tricky without a notification system in place.

The **Manage Notifications** feature in Devtron helps you solve this by sending updates about your pipelines through tools like Email, Slack, Discord, Microsoft Teams, and many more; thus ensuring you stay in the loop.

![Figure 1: Notifications Page in Global Configurations](https://devtron-public-asset.s3.us-east-2.amazonaws.com/images/global-configurations/manage-notification/notification-screen.gif)

{% hint style="info" %}
#### Prerequisite

OSS users should install **Notifications** integration available in Devtron Stack Manager.
{% endhint %}

Go to **Global Configurations** → **Notifications** to access this feature in Devtron. As shown below, there are 2 tabs available for you to manage your notification settings:

* [Configurations](broken-reference)
* [Notifications](broken-reference)

***

## Configurations

{% hint style="warning" %}
#### Who Can Perform This Action?

Only superadmins can manage configurations.
{% endhint %}

![](https://devtron-public-asset.s3.us-east-2.amazonaws.com/images/global-configurations/manage-notification/configurations-tab.jpg)

Here you can add and manage the following configurations:

* [SES Configuration](broken-reference)
* [SMTP Configuration](broken-reference)
* [Slack Configuration](broken-reference)
* [Webhook Configuration](broken-reference)

{% hint style="info" %}
#### Tip

At any point of time, you have the option to edit or delete an existing configuration, or add more as per your requirements.
{% endhint %}

### SES Configuration

{% hint style="info" %}
#### Prerequisites

* [Generate SMTP Credentials from AWS SES](https://docs.aws.amazon.com/ses/latest/dg/smtp-credentials.html) - To get the user access key and secret key.
* [Verify Email Identities in AWS SES](https://docs.aws.amazon.com/ses/latest/dg/creating-identities.html#verify-email-addresses-procedure) - This is to verify the email of the sender email address (e.g., _michael@devtron.ai_) you wish to use for sending email notifications.
{% endhint %}

You can use Amazon Simple Email Service (SES) to send email notifications to the recipients.

1. Click **Add**.
2.  Enter the following details in the **Configure SES** window:

    | Key                    | Description                                                                  |
    | ---------------------- | ---------------------------------------------------------------------------- |
    | **Configuration Name** | Give a name to your SES Configuration, e.g., `Email SES 2024`                |
    | **Access Key ID**      | Valid user ID from your AWS SMTP Settings page, e.g., `AKIAWEAVHF123ABCD123` |
    | **Secret Access Key**  | Password from your AWS SMTP Settings page                                    |
    | **AWS Region**         | The AWS Region you used while setting up SES                                 |
    | **Send email from**    | The sender email address verified by SES for sending emails                  |

![Figure 2: Sample SES Configuration](https://devtron-public-asset.s3.us-east-2.amazonaws.com/images/global-configurations/manage-notification/ses-data.jpg)

3. (Optional) If you wish to keep your configuration as the default one for sending emails, tick the **Set as default configuration to send emails** checkbox.
4. Click **Save**. You may watch the [Email Notification Walkthrough](broken-reference) for better understanding.

{% hint style="success" %}
#### Next Step

Refer [Create Notifications](broken-reference).
{% endhint %}

### SMTP Configuration

{% hint style="info" %}
#### Prerequisite

SMTP Credentials from your SMTP Provider. If you are using AWS SMTP, make sure to [verify domain identities](https://docs.aws.amazon.com/ses/latest/dg/creating-identities.html#verify-domain-procedure) to verify the domain (e.g., _devtron.ai_) of the sender email address you wish to use for sending emails notifications.
{% endhint %}

You can use any SMTP provider (e.g., Gmail SMTP, AWS) to send email notifications to the recipients.

1. Click **Add**.
2.  Enter the following details in the **Configure SMTP** window:

    | Key                    | Description                                                                                    |
    | ---------------------- | ---------------------------------------------------------------------------------------------- |
    | **Configuration Name** | Give a name to your SMTP Configuration, e.g., `Email SMTP 2024`                                |
    | **SMTP Host**          | The SMTP endpoint available in your SMTP settings, e.g., `email-smtp.ap-south-1.amazonaws.com` |
    | **SMTP Port**          | The port number available in your SMTP settings, e.g., `587`                                   |
    | **SMTP Username**      | A valid username created with your SMTP provider, e.g., `AKIAWEAVHF123ABCD123`                 |
    | **SMTP Password**      | The password generated by your SMTP provider                                                   |
    | **Send email from**    | The sender email address verified by your SMTP provider for sending emails                     |

![Figure 3: Sample SMTP Configuration](https://devtron-public-asset.s3.us-east-2.amazonaws.com/images/global-configurations/manage-notification/smtp-data.jpg)

3. (Optional) If you wish to keep your configuration as the default one for sending emails, tick the **Set as default configuration to send emails** checkbox.
4. Click **Save**. You may watch the [Email Notification Walkthrough](broken-reference) for better understanding.

{% hint style="success" %}
#### Next Step

Refer [Create Notifications](broken-reference).
{% endhint %}

### Slack Configuration

{% hint style="info" %}
#### Prerequisites

* A Slack account
* A Slack channel
* An [Incoming Webhook URL](https://slack.com/intl/en-gb/help/articles/115005265063-Incoming-webhooks-for-Slack) for your Slack Channel
{% endhint %}

This configuration helps you receive notifications on your preferred Slack channel.

1. Click **Add**.
2.  Enter the following details in the **Configure Slack** window:

    | Key               | Description                                                                                                           |
    | ----------------- | --------------------------------------------------------------------------------------------------------------------- |
    | **Slack Channel** | Name of the Slack channel on which you wish to receive notifications                                                  |
    | **Webhook URL**   | Enter a valid incoming webhook URL (see [prerequisites](broken-reference))                                            |
    | **Project**       | Select the project name to control the user access. Apps outside your selected project cannot use this configuration. |

![Figure 4: Sample Slack Configuration](https://devtron-public-asset.s3.us-east-2.amazonaws.com/images/global-configurations/manage-notification/slack-data.jpg)

3. Click **Save**. You may watch the [Slack Notification Walkthrough](broken-reference) for better understanding.

{% hint style="success" %}
#### Next Step

Refer [Create Notifications](broken-reference).
{% endhint %}

### Webhook Configuration

{% hint style="info" %}
#### Prerequisites

A Webhook URL for receiving notifications (e.g., Microsoft Teams Webhook URL, Discord Webhook URL, etc.)
{% endhint %}

1. Click **Add**.
2.  Enter the following details in the **Configure Webhook** window:

    | Key                    | Description                                                                                                                                                                                                                                                                                                |
    | ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | **Configuration name** | Name of the Slack channel on which you wish to receive notifications                                                                                                                                                                                                                                       |
    | **Webhook URL**        | Enter a valid Webhook URL link                                                                                                                                                                                                                                                                             |
    | **Headers**            | Add optional key-value pairs, e.g. `Content-Type: application/json`                                                                                                                                                                                                                                        |
    | **Data**               | <p>Write the payload content of the notification in a JSON format.<br>Refer:<br>- <a href="broken-reference">Microsoft Teams Payload</a><br>- <a href="broken-reference">Discord Payload</a><br>- <a href="broken-reference">Slack Payload</a><br>- <a href="broken-reference">RingCentral Payload</a></p> |

![Figure 5: Sample Webhook Configuration](https://devtron-public-asset.s3.us-east-2.amazonaws.com/images/global-configurations/manage-notification/webhook-data.jpg)

3. Here are some sample payloads for your reference:
4. Click **Save**. You may watch the [Discord Notification Walkthrough](broken-reference) for better understanding.

{% hint style="success" %}
#### Next Step

Refer [Create Notifications](broken-reference).
{% endhint %}

***

## Notifications

{% hint style="warning" %}
#### Who Can Perform This Action?

Only superadmins can manage notifications.
{% endhint %}

After completing the [configurations](broken-reference), you can create notifications.

### Create Notifications

1. Go to the **Notifications** tab and click **Add Notification**.

![Figure 6: Adding Notifications](https://devtron-public-asset.s3.us-east-2.amazonaws.com/images/global-configurations/manage-notification/add-notification-v2.jpg)

2. Click the **Send to** dropdown and select the recipient. It can be any of the following:
   * A verified email address (by SES/SMTP)
   * A Slack channel
   * A Webhook

![Figure 7: Choosing Recipients](https://devtron-public-asset.s3.us-east-2.amazonaws.com/images/global-configurations/manage-notification/send-to.gif)

{% hint style="info" %}
#### Note

You can add more than one recipient as per your requirement.
{% endhint %}

3. Click the **Select pipelines** dropdown and choose a filter. It can be any of the following:
   * Application
   * Project
   * Environment
   * Cluster

![Figure 8: Selecting Pipelines with Filters](https://devtron-public-asset.s3.us-east-2.amazonaws.com/images/global-configurations/manage-notification/filter-pipeline.gif)

{% hint style="info" %}
#### Note

You will see a list of CI/CD pipelines corresponding to your selected filter type.

* ![CI Icon](https://devtron-public-asset.s3.us-east-2.amazonaws.com/images/global-configurations/manage-notification/ci1.jpg) indicates that it is a CI (Build) pipeline.
* ![CD Icon](https://devtron-public-asset.s3.us-east-2.amazonaws.com/images/global-configurations/manage-notification/cd1.jpg) indicates that it is a CD (Deployment) pipeline.
* You can also choose to receive notifications for any CI or CD pipeline that do not exist currently but may exist in future.
{% endhint %}

4. For each pipeline, there are individual checkboxes for 3 types of events:
   * **Trigger** - Use this if you wish to receive notification whenever the pipeline is triggered.
   * **Success** - Use this if you wish to receive notification upon a successful build or deploy.
   * **Failure** - Use this if you wish to receive notification upon a failed build or deploy.

Click the checkbox relevant to you for receiving notifications. You can choose more than one as per your requirement.

![Figure 9: Selecting Events](https://devtron-public-asset.s3.us-east-2.amazonaws.com/images/global-configurations/manage-notification/choose-events.gif)

5. Click **Save**.

{% hint style="success" %}
#### Next Step

Build and Deploy your application to get notifications of its CI/CD events.
{% endhint %}

### Edit Notifications

You can use the checkbox besides the notifications to edit them one-by-one or in bulk.

#### Delete Notification

Use this to delete unwanted notifications.

![Figure 10: Deleting Existing Notifications](https://devtron-public-asset.s3.us-east-2.amazonaws.com/images/global-configurations/manage-notification/bulk-delete.gif)

#### Modify Event

Use this to change the events (trigger/success/failure) for which the notification is sent.

![Figure 11: Changing Event for Notifications](https://devtron-public-asset.s3.us-east-2.amazonaws.com/images/global-configurations/manage-notification/modify-event.gif)

#### Modify Recipients

Use this to remove or add recipients/channels to the existing notification(s).

![Figure 12: Changing Recipients of Notifications](https://devtron-public-asset.s3.us-east-2.amazonaws.com/images/global-configurations/manage-notification/modify-recipients.gif)

***

## Tutorials

### Email Notification

{% embed url="https://www.youtube.com/watch?v=rzP3KfTY3XU" %}

### Slack Notification

{% embed url="https://www.youtube.com/watch?v=ve1eGqslBqc" %}

### Discord Notification

{% embed url="https://www.youtube.com/watch?v=8RQ2dezrVvY" %}

***

## Sample Payloads

Here are some sample payloads for [webhook configurations](broken-reference).

### For Microsoft Teams

{% code title="Teams Webhook Payload" overflow="wrap" lineNumbers="true" %}
```json
{
    "type": "message",
    "attachments": [
        {
            "contentType": "application/vnd.microsoft.card.adaptive",
            "contentUrl": null,
            "content": {
                "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
                "type": "AdaptiveCard",
                "version": "1.2",
                "body": [
                    {
                        "type": "TextBlock",
                        "text": "Automation Notification for Devtron \n *App* : {{devtronAppName}} \n *Event Type* : {{eventType}}"
                    }
                ]
            }
        }
    ]
}
```
{% endcode %}

### For Slack

{% code title="Slack Webhook Payload" overflow="wrap" lineNumbers="true" %}
```json
{
    "text": "CI Triggered",
    "blocks": [
        {
            "type": "section",
            "text": {
                "type": "mrkdwn",
                "text": "Automation Notification for Devtron \n *App* : {{devtronAppName}} \n *Event Type* : {{eventType}}"
            },
            "accessory": {
                "type": "image",
                "image_url": "https://awsmp-logos.s3.amazonaws.com/3ec35b66-ca90-4ed0-8c9e-146fa65e1037/f3966518a472c0e5f51c57f5efb20da7.png",
                "alt_text": "Devtron Logo"
            }
        }
    ]
}
```
{% endcode %}

### For Discord

{% code title="Discord Webhook Payload" overflow="wrap" lineNumbers="true" %}
```json
{
    "content": "Automation Notification at Devtron \n App : {{devtronAppName}} \n Event Type : {{eventType}}"
}
```
{% endcode %}

### For RingCentral

{% code title="RingCentral Webhook Payload" overflow="wrap" lineNumbers="true" %}
```json
{
    "activity": "CI Triggered",
    "attachments": [
    {
        "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
        {
            "type": "TextBlock",
            "text": "Automation Notification at Devtron \n App: {{devtronAppName}} \n Event Type: {{eventType}}",
            "weight": "bolder",
            "size": "medium",
            "wrap": true
        },
        {
            "type": "ColumnSet",
            "columns": [
            {
                "type": "Column",
                "width": "auto",
                "items": [
                {
                    "type": "Image",
                    "url": "https://awsmp-logos.s3.amazonaws.com/3ec35b66-ca90-4ed0-8c9e-146fa65e1037/f3966518a472c0e5f51c57f5efb20da7.png",
                    "size": "small",
                    "style": "person"
                }
                ]
            },
            {
                "type": "Column",
                "width": "stretch",
                "items": [
                {
                    "type": "TextBlock",
                    "text": "Container Image Repo: {{devtronContainerImageRepo}} \n Container Image Tag: {{devtronContainerImageTag}}",
                    "weight": "bolder",
                    "wrap": true
                },
                {
                    "type": "TextBlock",
                    "spacing": "none",
                    "text": "Triggered By: {{devtronTriggeredByEmail}}",
                    "isSubtle": true,
                    "wrap": true
                }
                ]
            }
            ]
        },
        ]
    }
    ]
}
```
{% endcode %}
