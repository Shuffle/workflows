1. Configure Wazuh with the Webhook URL Start by logging into your Wazuh management console with access to edit the ossec.conf file. We'll first start by adding the Shuffle webhook forwarder.

    Transfer these integration files to the server. Ignore the file named "ossec.conf" for now.
    Move the custom-* files to the location /var/ossec/integrations

    <File here>

    Change the files' ownership and access rights. This MAY be necessary if Wazuh doesn't have root privileges (it shouldn't)
    
    <File here>

2. Configure ossec.conf to forward to Shuffle 

Go to the location /var/ossec/etc/ossec.conf (or where the ossec.conf file is). Take the information below (including ) and paste it in. Find the webhook URL from earlier, copy it and add it to the <hook_url> section. 

Find more fields like levels, groups and rule_id here.

     <File here>

3. Restart ossec manager. Every time you change ossec.conf, you need to restart the ossec manager.

      <File here>
You should now start seeing data sent from Wazuh into Shuffle which can be used. If data is NOT sent, make sure of a few things:

    If https in the Shuffle URL: is the certificate of Shuffle signed? Default: no.
    Check /var/ossec/logs for logs: grep -R custom-shuffle

4. Test the integration There are many ways to test the integration, but you can simplify it by setting the "level" part of the configuration to a lower number (3~), as that would trigger it in a lot of cases, including when you SSH into the Wazuh manager. After an alert is supposed to have triggered, go to Shuffle, and you'll see something like the image below.
