# Nexus Webhook Sample

This sample integration showcases Release triggers for Nexus *push* webhook events including both component and asset push events.

The preferred approach of using this sample is by applying the `webhook-integration.yaml` as-code template as described
in the main README file.

After applying the YAML file you can test it using the `Test run` feature on the trigger configuration page.

Asset push events can be tested using both `push_asset_headers.txt` and `push_asset_event.json`.

Component push events can be tested using both `push_component_headers.txt` and `push_component_event.json`.

The sample YAML file will configure the following objects in Release under the *Webhook Samples* folder:
 - Single endpoint for all events from Nexus accessible from **http://&lt;xlr-address&gt;/webhooks/nexus-sample-webhook**
 - Trigger to handle asset push events
   - This trigger has been configured to use the groovy rule editor which allows for more complex conditions. It checks
     the headers from the event to ensure it is executed only for asset events. It checks the event payload to
     ensure it is only executed when:
        - The asset event occured in the releases repository
        - The action that caused the event is CREATED or UPDATED
		- The asset format is maven2
        - The asset name containes the value 'xlr-server-' and ends with '.jar'
 - Trigger to handle component push events
   - This trigger has been configured to use the groovy rule editor which allows for more complex conditions. It checks
     the headers from the event to ensure it is executed only for component events. It checks the event payload to
     ensure it is only executed when:
        - The component event occured in the releases repository
        - The action that caused the event is CREATED or UPDATED
		- The component format is maven2
        - The component name is xlr-server
 - Template that both triggers use to create releases with a number of release variables that will be populated by the
   triggers

## Configure Nexus to send webhook events to Digital.AI Release

You must have administrative privileges in Nexus to configure a webhook. In Nexus select *Capabilities* under the *Administration*
menu.

Click the *Create capability* button to bring up the 'Select Capability Type' table

Select *Webhook: Repository* to open the 'Create Webhook: Repository Capability' screen

For Repository select the repository you would like to create the webhook for from the dropdown box

For Event Types add both asset and component from the available to selected window

For the URL use the endpoint created in Release, in this case **http://&lt;xlr-address&gt;/webhooks/nexus-sample-webhook**.

Then click on *Create capability*.  Now the webhook is enabled and should send any of your selected event types to the
endpoint configured in Release.

More information can be found in the [Nexus documentation](https://help.sonatype.com/repomanager3/webhooks).

### Customizing the YAML file for your environment

The sample here works in a Nexus environment configured with:
 * repository *releases*
 * asset and component format *maven2*
 * component exists in the repository with the name *xlr-server*
 * asset exists in the repository with the name xlr-server-<version>.jar

Look for those values in the YAML file and adjust according to your environment.


