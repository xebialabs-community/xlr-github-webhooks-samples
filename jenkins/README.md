# Jenkins Webhook Sample

This sample integration showcases Release triggers for Jenkins *build pipeline with Success status* event.

The preferred approach of using this sample is by applying the `webhook-integration.yaml` as-code template as described
in the main README file.

After applying the YAML file you can test it using the `Test run` feature on the trigger configuration page.

Build event can be tested using `build_success.json`.

The sample YAML file will configure the following objects in Release under the *Webhook Samples* folder:
 - Single endpoint for all events from Jenkins accessible from **http://&lt;xlr-address&gt;/webhooks/jenkins-sample-webhook**
 - Trigger to handle successful jenkins build events
   - This trigger has been configured to use the visual rule editor. It checks the event payload to ensure it is only executed when the build is successful for the project 'Test job'
 - Template that the trigger use to create releases with a number of release variables that will be populated by the trigger
   
## Configure Jenkins to send webhook events to Digital.AI Release

* Add the Outbound Webhook plugin
* Click on Jenkins ->  Manage Jenkins
* Add Post-build Actions
  * In the Webhook URL enter the endpoint created in Release, in this case **http://&lt;xlr-address&gt;/webhooks/jenkins-sample-webhook**
  * Check Send notification on success
* Click on Apply and Save

Detailed information can be found [here](https://plugins.jenkins.io/outbound-webhook/).

## Customizing the YAML file for your environment

The sample here works in a Jenkins environment configured with:
 * project *Test job*

Look for those values in the YAML file and adjust according to your environment.
