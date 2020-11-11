# Digital.AI Release Webhook Samples

This repository showcases the **Webhook event trigger** feature with example integrations for the following third-party systems and events:
* GitHub - React to push to master and pull request with a label being opened and synchronised
* BitBucket - Same events as above
* Gitlab - Same events as above
* Atlassian JIRA - Epic has been closed as Resolved
* Jenkins - Build pipeline completed with status success
* Dockerhub - React to push requests to a specific repository

For a general overview of the functionality please refer to the documentation topic [Webhooks overview](https://docs.xebialabs.com/release/webhooks/webhooks-overview/). The feature is available in Release 9.7 and up.

## Usage

Each integration contains an as-code file to quickly create the necessary `HTTP endpoint for Webhooks`, `Webhook event trigger` and `Release template`.

Please ensure you have XL CLI installed and configured by following the [instructions](https://docs.xebialabs.com/release/how-to/install-the-xl-cli).

Apply the as-code template:

> xl apply -f github/webhook-integration.yaml

After the as-code template is applied, Release will contain the new entities in the `Webhook Samples` folder.

Next step is to test the integration by configuring the third-party system to send data to the `HTTP endpoint for Webhooks` exposed on the URL of the following format:

> https://<xlr-public-address>:<xlr-public-address>/webhooks/<integration-name>-sample-webhook

As an alternative, event samples are available in the integration specific folder and can be sent to the endpoint using cURL:

> curl --request POST \
  --url 'http://localhost:5516/webhooks/github-sample-webhook' \
  --header 'Content-Type: application/json' \
  --header 'X-GitHub-Event: pull_request' \
  --data '@github/pull_request.json'
