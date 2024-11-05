GLPi webhook
About webhook
This webhook creates tickets in GLPi Assistance section. Created tickets have the next severity mapping:

Severity In zabbix	Urgency in GLPi
0 - Not classified	Medium (default)
1 - Information	Very low
2 - Warning	Low
3 - Average	Medium
4 - High	High
5 - Disaster	Very High
On Update action in zabbix, webhook updates created problem's title, severity and creates followup with update comment.

On resolve action, webhook updates created problem title and creates followup with resolve information.

Created ticket have "New" status, and resolved - "Solved" status.

Due to the specifics of the webhook, the number of retries is set to 1 by default. We recommend that you do not change this setting, because in case of a transaction error, additional duplicate objects (tickets, followups) may be created during the retry.

Installation guide
This guide describes how to integrate your Zabbix installation with GLPi tickets using the Zabbix webhook feature. This guide provides instructions on setting up a media type, a user and an action in Zabbix.


In GLPi
1. Create or use existing user in GLPi with permission to create tickets and followups.  

2. Please create an API token. For that you should go into user profile and set tick in "Regenerate" field against "API token" and hit save. 

3. Copy the API token of your new integration to use it in Zabbix.


In Zabbix
The configuration consists of a media type in Zabbix, which will invoke the webhook to send alerts to GLPi problems through the GLPi Rest API.

1. Import the GLPi media type from file media_glpi.yaml.

2. Change in the imported media the values of the variable glpi_token and glpi_url.

For more information about the Zabbix Webhook configuration, please see the documentation.

3. Create a Zabbix user and add Media with the GLPi media type. Though a "Send to" field is not used in GLPi webhook, it cannot be empty. To comply with frontend requirements, you can put any symbol there. Make sure this user has access to all hosts for which you would like problem notifications to be converted into GLPi tickets.

4. Set up a global macro {$ZABBIX.URL} with URL of current zabbix. Please notice that HTTPS will be used by default if HTTP/HTTPS schema is not present in the URL.

For more information, please see Zabbix and GLPi documentation.


Tested on
GLPI 9.5.7


Supported Versions
Zabbix 7.0