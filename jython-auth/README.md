# Jython Authentication webhook

This sample integration showcasess Release triggers for a generic tool creating a webhook events.

There are two authentication checks in this example.  First, the Jython Webhook executes a jython script to validate the value of the request parameter `token`.  If the value of `token` is set to `s3cr3t` the request is authenticated.  The second authentication check is built into the trigger.  The event trigger uses a **Jython filter** which does have access to the XL Release Jython API.  Since the **Jython filter** has access to the Jython API it will look for an `Auth-Token` header and then split the value on `:` so the first half is the folder vairable name and the second half is the token.

The sample YAML file will configure the following object in Release under the _Webhook Samples_ folder:
* Single endpoint for all events for this webhook accessable from *http://<xlr-address>/webhooks/jython-webhook*
* Trigger to handle events
* Template that the trigger will use to create releases

You will still need to configure a folder variable in the UI for the second layer of authentication.

**Note**: In XLR 9.7 the jython authentiation script does not have access to the normal jython API calls for security reasons.  
