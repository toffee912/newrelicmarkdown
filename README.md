# Epics NewRelic Monitoring


**The Epics team is using account: '11576 Cox - Manheim'**

### **Naming convention:**

**Synthetic Test naming format:**
<br> *'epics-(service name in github)-(endpoint type)-(environment)'*  

**Examples:**
- epics-NotesWebService-aws-prod      
- epics-NotesWebService-ping-prod
<br>

### **Alert Conditions and Policy format:**
<br>

**Alert Conditions format:**
<br> *'epics-(web service github name)-(monitor target)-(env)'*

**Examples:**
- epics-NotesWebService-synthetic-prod


**Policy format:** 
<br>*'epics-(env)'*

**Examples:**


## **Synthetic, APM, and Alert Strategy:**

Synthetic tests will have the following verifications:

- Elastic Beanstalk (AWS) and Fargate (AWS) endpoints, as well as F5 endpoints like CheckoutWebService, will only be checked with a script written as a synthetic test.
- APM data will not be used for alerting at this time due to inconsistent alerting.
- Runscope is preferred for setting up tests to check the health of the service until the team becomes more familiar with APM data.

Scripts are written in JavaScript using the HTTP client $http and the GOT module. To set up, Node 10.0 legacy is used.

The team decided to store service credentials securely and call them from synthetic requests, which has been successful.

Synthetic monitors can be set to run every 15 minutes.

The epics_awsgdmowner minion is used for AWS services, and epics_plminion_onprem is used for on-prem.

APM data will have the following verifications:

- Alerts based on APM data will be set up to verify on-prem nodes. As nodes are not as critical as customer-facing endpoints, using APM data for alerts is acceptable. Synthetic tests will not be used for this purpose to avoid duplicate work.

## **Alerts:**

Alerts for synthetics will utilize the following workflow: PagerDuty, Towtruck email, and Slack channel.

Alerts based on APM data will be sent to the Slack channel.

## **Creating Synthetic Monitors:**

* Navigate to the Synthetic Monitoring tab and click the Create Monitor button in New Relic.
* Select 'Endpoint Availability' as the scripted monitor type. For basic pinging, you can select 'Ping'.
* Choose the 'Account: 11576 - Cox - Manheim' and runtime Node 10 legacy. Select the desired frequency for running the test and provide a name.
* Depending on the type of service you're monitoring (on-prem or AWS), select one of the EpICS minions.
* Write the script in the console and validate that you're receiving successful requests from the service.
* Store service credentials and tokens in 'Secure Credentials' in New Relic instead of hard-coding them in the script.