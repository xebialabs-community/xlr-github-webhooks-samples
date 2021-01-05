# Version One Webhook Sample

This sample integration showcases triggers for Version One *assetCreated* and *assetChanged* webhook events.

The preferred approach of using this sample is by applying the `webhook-integration.yaml` as-code template as described
in the main README file.

After applying the YAML file you can test it using the `Test run` feature on the trigger configuration page.

Version One events can be tested using both `asset_created_event.json` and `asset_changed_event.json`.

The sample YAML file will configure the following objects in Release under the *Webhook Samples* folder:
 - Single endpoint for all events from Version One accessible from **http://&lt;xlr-address&gt;/webhooks/version-one-sample-webhook**
 - Trigger to handle asset created events
   - This trigger has been configured to use the visual rule editor. It checks 
     the event payload to ensure the event type of the webhook is AssetCreated
	 and the asset type is story.
 - Trigger to handle asset change events indicating story has been closed
   - This trigger has been configured to use the groovy rule editor which allows for more complex conditions. It checks
     the payload from the event to ensure it is executed when:
        - The event type is AssetChanged
		- The asset type is Story
        - The changes for the event indicate the new value of AssetState is Closed
 - Template that all triggers use to create releases with a number of variables that will be populated by the
   triggers

## Configure Version One to send webhook events to Digital.AI Release

In Version One select the admin icon(gear wheel) on the left hand pane.  

Navigate to Extensions > Webhooks and click the Add button on the top right of the screen.

In the "Webhook Subscription" screen populate the following values:

	- For the URL use the endpoint created in Release, in this case **http://&lt;xlr-address&gt;/webhooks/version-one-sample-webhook**.
	
	- Enter a descriptive name for the webhook in the WebhookId field
	
	- In the From section select *Story* from the drop down list and select the *Asset Created* button under Event Types. 
	
	- Click the *Add Trigger Event* button.
	
	- In the From section select *Story* from the drop down list and select the *Asset Changed* button under Event Types. 
	
	- Click the *Add Trigger Event* button.

Then click on *Save*.  Now the webhook is enabled and should send any of your selected event types to the
endpoint configured in Release.

More information can be found in the [Version One documentation](https://versionone.github.io/api-docs/#webhookSubscription).

### Troubleshooting webhooks from Version One

In Version One navigate to the Admin section and select Extensions > Webhooks.  Click on one of the configured webhooks.
The Status section of the Webhook Subscription will contain a history of webhook events by a date and timestamp. Clicking 
on a timestamp will provide a summary on the webhook event and if it was delivered successfully.

## Customizing the YAML file for your environment

The sample works in a Version One environment to process webhook events generated when the assetType field is *Story* and the eventType
field is *AssetCreated* or *AssetChanged*. For eventType of AssetChanged the story new state must be *Closed*. 

Look for these values in the YAML file and adjust according to your environment.


