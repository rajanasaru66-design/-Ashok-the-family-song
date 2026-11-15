---
title: "Log Drains"
description: "Log Drains connect site traffic logs and function logs from Netlify's CDN to third-party monitoring services for analysis, alerting, and data persistence."
---

> For the complete documentation index for AI agents, see [llms.txt](https://docs.netlify.com/llms.txt). Markdown versions of any documentation page are available by appending `.md` to its docs.netlify.com URL.

> **Pricing Information:** This feature is available on [Enterprise](https://www.netlify.com/pricing/?category=enterprise) plans.

The Log Drains feature allows you to connect site traffic logs, [function logs](/build/functions/logs), and [edge function logs](/build/edge-functions/get-started#monitor) from Netlify's CDN to third-party monitoring services for analysis, alerting, and data persistence. Additionally, this feature allows you to connect [deploy logs](/deploy/deploy-overview#deploy-log) from our builds service.

Once you've configured a log drain for a site, Netlify batches the site's log records from our CDN and build system and posts them to an endpoint in JSON/NDJSON format in near real-time. A configured external monitoring provider receives these records from the intake endpoint and makes them available for processing. You can drain the following data:

- **[site traffic log output](#traffic-log-output):** tracks visitor requests for assets and pages.
- **[function log output](#function-log-output):** tracks information such as function invocations.
- **[edge function log output](#edge-function-log-output):** tracks edge functions that output console log statements.
- **[server log output](#server-log-output):** tracks lines that a [Netlify Server](/build/server/) writes to its logs.
- **[deploy log output](#deploy-log-output):** tracks deploy information gathered while building and deploying a site.
- **[Web Application Firewall (WAF) log output](#waf-log-output):** tracks [WAF](/manage/security/secure-access-to-sites/web-application-firewall) rules matching requests.

If your site will handle HIPAA-regulated data, learn more about our [Trust Center](https://www.netlify.com/trust-center/), where you can download the reference architecture for HIPAA-compliant sites on Netlify. Read it before configuring a log drain. Anyone with a Netlify account can download it.

## Configure a log drain

To set up a log drain, you must be a Netlify Team Owner and have an account and API key provisioned with an external monitoring provider. Netlify supports integration with:

- [Datadog](https://www.netlify.com/integrations/datadog/)
- [New Relic](https://newrelic.com/instant-observability/netlify-logs/63f08781-18ad-4a89-ae63-49718deee041)
- [Axiom](https://axiom.co/)
- [Azure Monitor](https://learn.microsoft.com/en-us/azure/azure-monitor/logs/data-platform-logs)
- [Sumo Logic](https://service.sumologic.com/)
- [Splunk Observability Cloud](https://www.splunk.com/en_us/products/observability.html)
- [Logflare](https://logflare.app/)
- [Amazon Simple Storage Service (Amazon S3)](https://aws.amazon.com/s3/)
- General HTTP endpoints

## Facet Switcher

Select your external monitoring provider:

### Available Tabs:

#### Datadog Tab

### Datadog

1. For your selected site, go to 
### NavigationPath Component:

Analytics & metrics > Log Drains
 and select **Enable a log drain**.
2. Select `Datadog` as the **Log drain service**.
3. Select the **Log types** to drain. You can drain your site's traffic logs, function logs, edge function logs, and deploy logs.
4. Optional: add **Traffic log filtering**. If you're draining traffic logs and don't want `client_ip` and `user_agent` in the data, select `Exclude personally identifiable information (PII)`.
5. Under **Service settings**, select the **Region** where your [Datadog site](https://docs.datadoghq.com/getting_started/site/) is located.
6. Enter the unique **API key** for your logging service provider account. Verify that you are entering your **API key** instead of the Datadog application key.
7. Optional: add key/value pairs under **Tags** to tag your logs with certain attributes. These become query parameters in requests to the logs intake endpoint.

Available keys for Datadog:
| Key | Tag Description | Example value |
| --- | --- | --- |
| `ddtag` | tags associated with logs, grouped into a single list with the value `ddtags` | `env:prod` |
| `service` | name of the application or service generating the log events | `mysubdomain` |

8. Select **Connect**.

#### New Relic Tab

### New Relic

1. For your selected site, go to 
### NavigationPath Component:

Analytics & metrics > Log Drains
 and select **Enable a log drain**.
2. Select `New Relic` as the **Log drain service**.
3. Select the **Log types** to drain. You can drain your site's traffic logs, function logs, edge function logs, and deploy logs.
4. Optional: add **Traffic log filtering**. If you're draining traffic logs and don't want `client_ip` and `user_agent` in the data, select `Exclude personally identifiable information (PII)`.
5. Under **Service settings**, select the **Region** that applies to your New Relic account.
6. Enter a [License API key](https://docs.newrelic.com/docs/apis/intro-apis/new-relic-api-keys/#overview-keys), also called `INGEST-LICENSE`, for your New Relic account. Verify that you're entering your License API key and not your License API key ID or [user key](https://docs.newrelic.com/docs/apis/intro-apis/new-relic-api-keys/#user-key).
7. Optional: to add a tag for your log drain, under **Tags**, enter the `key` and `value`. Then select **Add tag**. Any tags you add become query parameters in log drain requests to New Relic.

Example tags for New Relic:

| Key           | Value         | Tag description                                              |
| ------------- | ------------- | ------------------------------------------------------------ |
| `environment` | `production`  | environment type                                             |
| `service`     | `mysubdomain` | name of the application or service generating the log events |

For guided help on optimizing your New Relic dashboard for your site's logs, install the [Netlify Logs quickstart](https://newrelic.com/instant-observability/netlify-logs/63f08781-18ad-4a89-ae63-49718deee041) on New Relic.

8. Select **Connect**.

#### Axiom Tab

### Axiom

To configure a log drain that sends your site logs to Axiom:

1. On Axiom, go to **Integrations**.
2. Install Netlify's Axiom integration, which opens a prompt to authorize the Axiom app to access Netlify on your behalf.
3. Once installed, you're redirected to configure your Netlify integration on Axiom. Copy the Axiom integration token.
4. On Netlify, for your chosen site, go to 
### NavigationPath Component:

Analytics & metrics > Log Drains
 and select **Enable a log drain**.
5. Select `Axiom` as the **Log drain service**.
6. Select the **Log types** to drain. You can drain your site's traffic logs, function logs, edge function logs, and deploy logs.
7. Optional: add **Traffic log filtering**. If you're draining traffic logs and don't want `client_ip` and `user_agent` in the data, select `Exclude personally identifiable information (PII)`.
8. Under **Service settings**, paste the **Integration token** copied from Axiom.
9. Confirm with **Connect**.

For an overview of reviewing your logs on Axiom, check out [Axiom's Netlify Integration docs](https://axiom.co/docs/integrations/netlify).

#### Azure Monitor Tab

### Azure Monitor

To send your site's log drains to Azure Monitor through the Netlify UI:

1. On Azure Monitor, from your log analytics workspace, go to 
### NavigationPath Component:

Settings > Agents
. Under the **Log Analytics Agent Instructions** dropdown, you'll find the **Workspace ID** and **Primary key** you'll need to enter into the Netlify UI.
   ![Azure analytics workspace screenshot highlighting the Workspace ID and Primary Key fields under Log Analytics Agent Instructions.](/images/log-drains-azure-inputs.png)
2. On Netlify, for your chosen site, go to 
### NavigationPath Component:

Analytics & metrics > Log Drains
. If this is your first log drain for your site, select **Enable a log drain**.
3. Select `Azure` as the **Log drain service**.
4. Select the **Log types** to drain. You can drain your site's traffic logs, function logs, edge function logs, and deploy logs.
5. Optional: add **Traffic log filtering**. If you're draining traffic logs and don't want `client_ip` and `user_agent` in the data, select `Exclude personally identifiable information (PII)`.
6. Under **Service settings**, enter your Azure **Workspace ID** and **Primary key**.
7. Confirm with **Connect**.

For an overview of reviewing your logs on Azure, check out [Azure's Analytics workspace docs](https://learn.microsoft.com/en-us/azure/azure-monitor/logs/log-analytics-workspace-overview).

#### Sumo Logic Tab

### Sumo Logic

To configure a log drain that sends logs to your Sumo Logic account, you need to:

1. [Configure your HTTP Logs and Metrics Source in Sumo Logic](#configure-your-http-logs-and-metrics-source-in-sumo-logic)
2. [Set up the log drain in the Netlify UI](#set-up-the-log-drain-in-the-netlify-ui)

#### Configure your HTTP Logs and Metrics Source in Sumo Logic

1. If you haven't already, create a [hosted collector](https://help.sumologic.com/docs/send-data/hosted-collectors/) to collect your data in Sumo Logic.

2. In the Sumo Logic web app, add and configure your HTTP Logs and Metrics Source using [Sumo Logic's docs](https://help.sumologic.com/docs/send-data/hosted-collectors/http-source/logs-metrics/#configure-an-httplogs-and-metrics-source).

3. Ensure that you copy your **HTTP Source Address** to use in the Netlify UI.

#### Set up the log drain in the Netlify UI

For security, Netlify hides the full **HTTP Source Address** in the Netlify UI. After you configure your log drain, only the base URL is visible in the Netlify UI.

1. On Netlify, for your selected site, go to 
### NavigationPath Component:

Analytics & metrics > Log Drains
 and select **Enable a log drain**.
2. Select `Sumo Logic` as the **Log drain service**.
3. Select the **Log types** to drain. You can drain your site's traffic logs, function logs, edge function logs, and deploy logs.
4. Optional: add **Traffic log filtering**. If you're draining traffic logs and don't want `client_ip` and `user_agent` in the data, select `Exclude personally identifiable information (PII)`.
5. Under **Service settings**, fill in the **Full URL** field using the **HTTP Source Address** you copied from Sumo Logic.
6. Select **Connect**.

#### Splunk Observability Cloud Tab

### Splunk Observability Cloud

1. For your selected site, go to 
### NavigationPath Component:

Analytics & metrics > Log Drains
 and select **Enable a log drain**.
2. Select `Splunk Observability Cloud` as the **Log drain service**.
3. Select the **Log types** to drain. You can drain your site's traffic logs, function logs, edge function logs, and deploy logs.
4. Optional: add **Traffic log filtering**. If you're draining traffic logs and don't want `client_ip` and `user_agent` in the data, select `Exclude personally identifiable information (PII)`.
5. Under **Service settings**, enter the [**Realm**](https://docs.splunk.com/observability/en/admin/references/organizations.html) from your Splunk Observability Cloud profile.
6. Enter the [**Access Token**](https://docs.splunk.com/observability/en/admin/authentication/authentication-tokens/org-tokens.html#admin-org-tokens) from your Splunk Observability Cloud settings.
7. Select **Connect**.

#### Logflare Tab

### Logflare

1. For your selected site, go to 
### NavigationPath Component:

Analytics & metrics > Log Drains
 and select **Enable a log drain**.
2. Select `Logflare` as the **Log drain service**.
3. Select the **Log types** to drain. You can drain your site's traffic logs, function logs, edge function logs, and deploy logs.
4. Optional: add **Traffic log filtering**. If you're draining traffic logs and don't want `client_ip` and `user_agent` in the data, select `Exclude personally identifiable information (PII)`.
5. Under **Service settings**, enter your Logflare Ingest **API key**.
6. To specify where you want your logs to go, enter the Logflare **Source ID** for your logs.
7. Select **Connect**.

#### Amazon S3 Tab

### Amazon S3

To configure a log drain that sends logs to your Amazon S3 account as Gzip-compressed files, you need to:

1. [Create an Amazon S3 bucket and set up a bucket policy](#create-an-amazon-s3-bucket-and-set-up-a-bucket-policy)
2. [Configure the log drain in the Netlify UI](#configure-the-log-drain-in-the-netlify-ui)

#### Create an Amazon S3 bucket and set up a bucket policy

1. In the AWS Management Console, [create an S3 bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/creating-bucket.html).

- **Object Ownership** for the bucket should be set to either **Bucket owner enforced** or **Bucket owner preferred**.
- Make note of the bucket name to use in your Netlify configuration.

2. Go to your bucket's **Permissions** and under **Bucket policy** select **Edit**.
3. Copy and paste the following bucket policy, replacing `YOUR_BUCKET_NAME` with the name of your Amazon S3 bucket:

```json title="JSON" frame="terminal"
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "NetlifyLogDrains",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::128866310339:role/log-shipper"
      },
      "Action": "s3:PutObject",
      "Resource": "arn:aws:s3:::YOUR_BUCKET_NAME/*",
      "Condition": {
        "StringEquals": {
          "s3:x-amz-acl": "bucket-owner-full-control"
        }
      }
    }
  ]
}
```

4. Select **Save Changes**.

### Caution - Bucket lifecycle

For cost control reasons, we recommend deleting logs after a period of 90 days. You can configure your Amazon S3 bucket to delete logs automatically by [setting lifecycle rules](https://docs.aws.amazon.com/AmazonS3/latest/userguide/how-to-set-lifecycle-configuration-intro.html).

#### Configure the log drain in the Netlify UI

1. For your selected site, go to 
### NavigationPath Component:

Analytics & metrics > Log Drains
 and select **Enable a log drain**.
2. Select `Amazon S3` as the **Log drain service**.
3. Select the **Log types** to drain. You can drain your site's traffic logs, function logs, edge function logs, and deploy logs.
4. Optional: add **Traffic log filtering**. If you're draining traffic logs and don't want `client_ip` and `user_agent` in the data, select `Exclude personally identifiable information (PII)`.
5. Under **Service settings**, select the **Bucket region** where your bucket is located.
6. Enter your S3 **Bucket name**.
7. Enter your S3 **Bucket path**. We recommend using `YOUR_BUCKET_NAME/logs/netlify/`.
8. Select **Verify bucket and connect**.

   ![](/images/log-drains-configure-log-drain-in-netlify-ui.png)

9. Use the provided path to navigate to your S3 bucket's verification file.
10. Copy and paste the contents of the file into the **Verification token** field, then select **Verify**.

#### General HTTP endpoint Tab

### General HTTP endpoint

Netlify's General HTTP endpoint support allows you to set up a custom log drain with any external monitoring provider that accepts log drain requests in JSON or NDJSON format.

To set up a custom log drain, you must provide a full URL of your external monitoring provider's endpoint. Depending on your external monitoring provider, you can enter your API key as a query parameter in your endpoint or you can enter an Authorization header in the Netlify UI.

For example, this URL includes an API key and a tag as query parameters:

```
http://YOUR_ENDPOINT_RESOURCE_PATH?api-key=YOUR_API_KEY&environment=production
```

For security, Netlify hides the full endpoint in the Netlify UI. After you configure your log drain, only the base URL is visible in the Netlify UI.

1. For your selected site, go to 
### NavigationPath Component:

Analytics & metrics > Log Drains
 and select **Enable a log drain**.
2. Select `General HTTP endpoint` as the **Log drain service**.
3. Select the **Log types** to drain. You can drain your site's traffic logs, function logs, edge function logs, and deploy logs.
4. Optional: add **Traffic log filtering**. If you're draining traffic logs and don't want `client_ip` and `user_agent` in the data, select `Exclude personally identifiable information (PII)`.
5. Under **Service settings**, enter the **Full URL** for your endpoint, including any optional tags as query parameters. Depending on your external monitoring provider, enter your API key as a query parameter in your endpoint or under **Authorization header**.
6. Select the **Log Drain Format** that your endpoint accepts.
7. Select **Connect**.

## Edit a log drain

If you need to adjust the settings for an existing log drain, under 
### NavigationPath Component:

Analytics & metrics > Log Drains
, select **Configure**. Configuration changes become active within approximately five minutes.

To stop sending specific log data to your external monitoring provider, clear the **Log types** you no longer need and then save your change.

## Remove a log drain

To terminate an existing log drain configuration for a site, under 
### NavigationPath Component:

Analytics & metrics > Log Drains
, select **Delete**. All log types associated with the site's log drain will be removed. Saved logs are accessible in your logging service provider account.

## Traffic log output

Drained site traffic logs include the following fields parsed from our CDN logs:

- **`account_id`:** ID of the Netlify team that the site belongs to.
- **`client_ip`:** IP address of the client. Omitted if you selected **Exclude personally identifiable information (PII)**.
- **`content_type`:** [Content-Type](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Type) of the request (for example, `text/html`).
- **`country`:** country of origin for the request, formatted as an ISO 3166-1 two-letter code.
- **`deploy_id`:** ID of the deploy (for example, `61153ae8b0f6a900088386e8`).
- **`duration`:** duration of processing the request and sending the response, in milliseconds.
- **`firewall_rule`:** the Firewall traffic rule that matches the request. Can be one of `default_allow`, `default_deny`, `ip_allow`, `ip_deny`, `geo_allow`, `geo_deny` , or `-`. If there are no traffic rules added to a site, then `firewall_rule` returns `-`. Learn more about [Firewall traffic rules](/manage/security/secure-access-to-sites/traffic-rules).
- **`block_reason`:** indicates why the request was blocked. If there are rate limiting rules applied to the site and if the rules match the request, then `block_reason` returns `rate_limit`. Learn more about [Rate limiting Rules](/manage/security/secure-access-to-sites/rate-limiting).
- **`rate_limit`:**
  - **`rule_id`:** ID of the rate limiting rule the request matched. Learn more about [Rate limiting Rules](/manage/security/secure-access-to-sites/rate-limiting).
- **[Deprecated]** **`rule_id`:** ID of the rate limiting rule the request matched. This field is being deprecated and will disappear in a future release, use **`rate_limit.rule_id`** instead.
- **`log_type`:** indicates the type of log. The value is `traffic`.
- **`method`:** request method.
- **`referrer`:** [referrer](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referer) on the request.
- **`request_id`:** Netlify request ID (for example, `01FDWR77JMF2DA1CHF5YA6H07C`).
- **`request_size`:** size of the request in bytes.
- **`response_size`:** size of the response in bytes.
- **`site_id`:** ID of the site.
- **`status_code`:** status code of the HTTP response.
- **`timestamp`:** timestamp of the request, formatted with RFC 3339 (for example, `2021-08-24T18:54:34.831Z`).
- **`url`:** URL of the request.
- **`user_agent`:** [user-agent](https://developer.mozilla.org/en-US/docs/We
