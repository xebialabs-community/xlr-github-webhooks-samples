# GitLab Webhook Sample

This sample integration showcases Release triggers for GitLab *merge request* and *push* webhook events.

The preferred approach of using this sample is by applying the `webhook-integration.yaml` as-code template as described
in the main README file.

After applying the YAML file you can test it using the `Test run` feature on the trigger configuration page.

Merge request events can be tested using both `merge_request_headers.txt` and `merge_request_event.json`.

Pull events can be tested using both `push_headers.txt` and `push_event.json`.

The sample YAML file will configure the following objects in Release under the *Webhook Samples* folder:
 - Single endpoint for all events from GitLab accessible from **http://&lt;xlr-address&gt;/webhooks/gitlab-sample-webhook**
 - Trigger to handle push events
   - This trigger has been configured to use the visual rule editor.  It checks the headers from the event to ensure
     it is executed only for push events.  It checks the event payload to ensure it is only executed when pushing to the
     master branch of the xlr-webhooks-samples repository.
 - Trigger to handle merge request events
   - This trigger has been configured to use the groovy rule editor which allows for more complex conditions. It checks
     the headers from the event to ensure it is executed only for merge request events. It checks the event payload to
     ensure it is only executed when:
        - The merge request is opened, reopened or when a commit has been added to it
        - It contains the label BUILD
        - It is merging into the master branch of the xlr-webhooks-samples repository
 - Template that both triggers use to create releases with a number of release variables that will be populated by the
   triggers

## Configure GitLab to send webhook events to Digitial.AI Release

In GitLab go to the repository you want to enable the webhook events for and navigate to Settings > Webhooks.

For the URL use the endpoint created in Release, in this case **http://&lt;xlr-address&gt;/webhooks/gitlab-sample-webhook**.

Then choose the events you want send, in this case *Push events* and *Merge request events*.

Then click on *Add webhook*.  Now the webhook is enabled and should send any of your selected event types to the
endpoint configured in Release.

More information can be found in the [GitLab documentation](https://docs.gitlab.com/ee/user/project/integrations/webhooks.html).
Also, if your environment has GitLab and Digitial.AI Release running on the same server you may need to [enable GitLab
to send webhooks to localhost](https://docs.gitlab.com/ee/security/webhooks.html).

### Troubleshooting webhooks from GitLab

You can test the webhook that was created in GitLab by resending previously sent events.

In GitLab go to the repository that contains the webhook and navigate to Settings > Webhooks.  At the bottom of the
page is a list of webhooks for the project.  Select *edit* on the webhook.  At the bottom of the edit page you will
find the most recent events sent.  Select *View details* to see the header and payload of the event as well as
a button that will allow you to resend that event.

## Customizing the YAML file for your environment

The sample here works in a GitLab environment configured with:
 * repository *xlr-webhooks-samples*
 * branch *master*
 * labels *BUILD*

Look for those values in the YAML file and adjust according to your environment.


