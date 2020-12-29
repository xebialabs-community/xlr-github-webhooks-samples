# Artifactory Webhook Sample

This sample integration showcases triggers for Artifactory *artifact* and *docker* webhook events.

The preferred approach of using this sample is by applying the `webhook-integration.yaml` as-code template as described
in the main README file.

After applying the YAML file you can test it using the `Test run` feature on the trigger configuration page.

Artifact events can be tested using `artifact_deployed_event.json`.

Docker events can be tested using `docker_event.json`.

The sample YAML file will configure the following objects in Release under the *Webhook Samples* folder:
 - Single endpoint for all events from Artifactory accessible from **http://&lt;xlr-address&gt;/webhooks/artifactory-sample-webhook**
 - Trigger to handle artifact deployed events
   - This trigger has been configured to use the visual rule editor. It checks the event payload to ensure it 
     is only executed when an artifact is deployed to the xlr-webhooks-samples repository.
 - Trigger to handle docker events
   - This trigger has been configured to use the visual rule editor. It checks the event payload to ensure it 
     is only executed when a docker image is pushed to the xlr-docker-webhooks-samples repository.
 - Template that all triggers use to create releases with a number of release variables that will be populated by the
   triggers

## Configure Artifactory to send webhook events to Digital.AI Release

In Artifactory go to the Administration tab in the left hand pane.  

Navigate to General > Webhooks and click the New Webhook button on the top right of the screen.

In the "Create new webhook" screen populate the following values:

	- Check the enabled box
	
	- Enter a descriptive name for the webhook in the Name field
	
	- For the URL use the endpoint created in Release, in this case **http://&lt;xlr-address&gt;/webhooks/artifactory-sample-webhook**.
	
	- Select the events and actions on the event that you want the webhook to be applied to. For this sample create two 
	  webhooks for the following events:
		- Artifact -> Artifact was deployed
		- Docker -> Docker tag was pushed

	- Select the repository that you want the webhook to be applied to.

Then click on *Create*.  Now the webhook is enabled and should send any of your selected event types to the
endpoint configured in Release.

More information can be found in the [Artifactory documentation](https://www.jfrog.com/confluence/display/JFROG/Webhooks).

### Troubleshooting webhooks from Artifactory

You can test the webhook that was created in Artifactory by generating a test webhook event with dummy data that will sent to 
Digital.AI Release.

In Artifactory navitage to the Administration tab and select General > Webhooks.  Click on one of the configured webhooks.
At the bottom of the page is a Test button.  Clicking the test button will cause a webhook event to be delivered to the configured
URL containing dummy data. This button can be used to test connectivity between Artifactory and Digital.AI Release. Note that 
the dummy payload data in the test webhook may not pass the filtering criteria in Digital.AI Release.

#### Customizing the YAML file for your environment

The sample here works in a Artifactory environment configured with a repository of *xlr-webhooks-samples* and 
*xlr-docker-webhooks-samples*. 

Look for this value in the YAML file and adjust according to your environment.