---

copyright:
  years:  2021
lastupdated: "2021-05-11"

keywords: IBM Cloud, monitoring, alerts, sms, SMS

subcollection: monitoring

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}
{:important: .important}
{:note: .note}
{:external: target="_blank" .external}

# Sending SMS alerts using {{site.data.keyword.openwhisk_short}}
{: #cf_sms}

In the {{site.data.keyword.mon_full_notm}} service, you can configure single alerts and multi-condition alerts to notify support staff about problems that might require attention. Using {{site.data.keyword.openwhisk}}, these alerts can trigger SMS (short message service) messages. 
{:shortdesc}

This example shows how to use [Twilio Programmable SMS Messaging support](https://www.twilio.com/docs/sms){: external} and {{site.data.keyword.openwhisk}} to send SMS alerts to support staff members.  This example uses the Twilio Python package.  [Other language support is available through Twilio.](https://www.twilio.com/docs/libraries){: external}

1. [Create a Twilio account.](https://www.twilio.com/docs/usage/tutorials/how-to-use-your-free-trial-account){: external}

2. [Create a Twilio phone number that will be used to send your SMS messages.](https://www.twilio.com/docs/usage/tutorials/how-to-use-your-free-trial-account#get-your-first-twilio-phone-number){: external}

   After you click **Get a trial phone number** make note of the phone number you are assigned.  You will need this phone number in later steps.
   {: important}   

3. [Install the {{site.data.keyword.openwhisk}} CLI and plug-in.](https://cloud.ibm.com/docs/openwhisk?topic=openwhisk-cli_install)

4. [Create an {{site.data.keyword.openwhisk}} namespace.](/docs/openwhisk?topic=openwhisk-namespaces#create_iam_namespace)

5. On your local computer, create a Python virtual environment to install the requirements.

   If you are running a Windows system, run the following commands:

   ```
   pip install virtualenv
   mkdir twilio
   virtualenv twilio
   cd twilio/scripts
   pip install twilio
   deactivate
   ```
   {: codeblock}

  If you are running a Unix or MacOS system, run the following commands:

   ```
   pip install virtualenv
   mkdir twilio
   cd twilio
   virtualenv virtualenv
   source virtualenv/bin/activate
   pip install twilio
   deactivate
   ```
   {: codeblock}

6. Create a new file named `__main__.py` with a new function named `twilio`.

   ```
   # Download the helper library from https://www.twilio.com/docs/python/install
   import os
   from twilio.rest import Client

   def twilio(args):
      # Find your Account SID and Auth Token at twilio.com/console
      # and set the environment variables. See http://twil.io/secure
      account_sid = "<YOUR_ACCOUNT_SID>"
      auth_token = "<YOUR_AUTH_TOKEN>"
      client = Client(account_sid, auth_token)

      message = client.messages \
                      .create(
                          body="Alert detected in your Sysdig instance" ,
                          from_='<TWILIO_NUMBER>',
                          to='<YOUR_DESTINATION_NUMBER>'
                      )

      return {"result": "Message status " + message.status}
   ```
   {: codeblock}

   Where:

   * `YOUR_ACCOUNT_SID` is your Twilio SID that can be found at [twilio.com/console](twilio.com/console){: external}.
   * `YOUR_AUTH_TOKEN`  is your Twilio Auth token that can be found at [twilio.com/console](twilio.com/console){: external}.
   * `TWILIO_NUMBER` is the Twilio trial phone number assigned to you in the second step.
   * `YOUR_DESTINATION_NUMBER` is the number where the SMS message is to be sent.

7. Create a `ZIP` file with the code and the information required to run.  Your `ZIP` file must contain your `__main__.py` file and all the files created in your `twilio` directory.

8. Create an {{site.data.keyword.cloud_notm}} function to run your code using the following command.

   ```
   ibmcloud fn action create sms-twilio twilio.zip --kind python:3.7 --main twilio
   ```
   {: pre}

   See [Packaging Python code with a local virtual environment in a compressed file](/docs/openwhisk?topic=openwhisk-prep#prep_python_local_virtenv) for more information on the process to deploy a function written in Python.

9. Get your {{site.data.keyword.cloud_notm}} API key by running the following command.  The API key will be required to integrate {{site.data.keyword.mon_full_notm}} with your {{site.data.keyword.cloud_notm}} function.

   ```
   ibmcloud iam api-key-create ibm-cloud
   ```
   {: pre}

10. [Access the {{site.data.keyword.mon_full_notm}} console.](/docs/monitoring?topic=monitoring-launch#launch_step2).


11. [Configure an {{site.data.keyword.mon_full_notm}} notification channel that will send the desired alerts to {{site.data.keyword.openwhisk}}.](/docs/monitoring?topic=monitoring-notifications#notifications_create)  

   
12. [Configure an {{site.data.keyword.mon_full_notm}} alert to send to the configured notification channel.](/docs/monitoring?topic=monitoring-alerts)

## Customizing the alert message
{: cf_sms_custom}

{{site.data.keyword.mon_full_notm}} sends alert data as a [JSON payload](https://docs.sysdig.com/en/configure-a-webhook-channel.html){: external}.  The information provided by the `JSON` file can be used to customize your SMS message.

For example, if you want to include the alert name, the affected entity, and the status of the alert, you can change your function code as follows:

```
# Download the helper library from https://www.twilio.com/docs/python/install
import os
from twilio.rest import Client

def twilio(args):
   # Find your Account SID and Auth Token at twilio.com/console
   # and set the environment variables. See http://twil.io/secure
   account_sid = "<YOUR_ACCOUNT_SID>"
   auth_token = "<YOUR_AUTH_TOKEN>"
   client = Client(account_sid, auth_token)

   message = client.messages \
                   .create(
                       body="Alert " + args['alert_name'] + " in " + args['entities'][0]['entity'] + " is " + args['state'],
                       from_='<TWILIO_NUMBER>',
                       to='<YOUR_DESTINATION_NUMBER>'
                   )

   return {"result": "Message status " + message.status}

```
{: codeblock}

An SMS message similar to the following would be sent when an issue is alerted:

```
Sent from your Twilio trial acount - Alert example in agent_tag_Tag = 'test=1' and agent_tag_sysdig_secure_enabled = 'true' and host = 'myhost' and host_name ='myhost' and host_mac = '00:00:00:00:00:00' is ACTIVE
```
{: screen}

When the alert is resolved an SMS similar to the following will be sent:

```
Sent from your Twilio trial acount - Alert example in agent_tag_Tag = 'test=1' and agent_tag_sysdig_secure_enabled = 'true' and host = 'myhost' and host_name ='myhost' and host_mac = '00:00:00:00:00:00' is OK
```
{: screen}


