## Google Cloud Pub/Sub and Scheduler: Quick Start Guide

This document provides a consolidated guide for setting up and using Google Cloud Pub/Sub, based on instructions from various Qwik Labs.

---

### 1. Pub/Sub: Qwik Start - Console (GSP096)

This section covers the basic setup of a Pub/Sub topic and subscription using the Google Cloud Console.

#### Task 1: Create a Pub/Sub Topic

1.  Navigate to the **Pub/Sub** section in the Google Cloud Console.
2.  Click **Create Topic**.
3.  For the **Topic ID**, enter `MyTopic`.
4.  Leave all other fields with their default values.
5.  Click **Create**.

#### Task 2: Add a Subscription

After the topic is created, you need a subscription to receive messages published to that topic.

1.  From the `MyTopic` details page, click **Create Subscription**.
2.  Provide a **Subscription ID** (e.g., `MySubscription`).
3.  Leave the remaining options at their default values and click **Create**.

---

### 2. Cloud Scheduler with Pub/Sub - gcloud CLI (GSP401)

This section demonstrates how to create a Pub/Sub topic and subscription using `gcloud` commands, which is useful for automation and for setting up a target for a Cloud Scheduler job.

#### Task 1: Enable Cloud Scheduler API
Before creating a cron job, ensure the Cloud Scheduler API is enabled for your project. This can be done via the console or the command line:
```bash
gcloud services enable cloudscheduler.googleapis.com
```

#### Task 2: Set up Pub/Sub via gcloud

*   **Create a Pub/Sub topic** to serve as the target for your cron job. This command creates a topic named `cron-topic`.
    ```bash
    gcloud pubsub topics create cron-topic
    ```

*   **Create a Pub/Sub subscription** to pull messages from the topic. This command creates a subscription named `cron-sub` attached to `cron-topic`.
    ```bash
    gcloud pubsub subscriptions create cron-sub --topic cron-topic
    ```

---

### 3. Verify Pub/Sub Messages (Challenge Lab)

After publishing messages to a topic (e.g., via a Cloud Scheduler job), you can verify that they were received by pulling them from the associated subscription.

*   **Pull messages from a subscription** using the `gcloud` command. This example pulls up to 5 messages from `cloud-pubsub-subscription`. Remember to replace the subscription name with your actual subscription ID (e.g., `cron-sub`).
    ```bash
    gcloud pubsub subscriptions pull cloud-pubsub-subscription --limit 5
    ```
