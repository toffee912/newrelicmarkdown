Epics-NewRelic-Monitoring
Monitoring apps that Epics owns with New Relic

**Our team on account '11576 Cox - Manheim'**

# **Naming convention:**

Synthetic test naming format 'epics-(service name in github)-(endpoint type)-(environment)'  examples

epics-NotesWebService-aws-prod      epics-NotesWebService-ping-prodAlert Conditions and Policies format

Policy format 'epics-(env)'

epics-prodAlert format 'epics-(web service github name)-(monitor target)-(env)'

epics-NotesWebService-synthetic-prod

Synthetic, APM  and Alert strategy:

# **Synthetic tests will have these verifications:**

Elastic Beanstalk (aws) and Fargate(aws) endpoints  and F5 endpoints i.e. CheckoutWebService,  will only be checked with a script written as a synthetic. 
We don't feel comfortable with using APM data at this time so we are choosing not to use it for alerting.  At this time we cant get consisting alerting from APM data.
We are also very comfortable with Runscope and have more confidence in setting our tests up to model that method of checking the health of the service.  Once we get more familiar with APM data we can evaluate how to use it.

Scripts are written in JavaScript and http client $http GOT module, to setup we use Node 10.0 legacy

Team decided to store our service credentials in secure credentials, we call that from synthetic request and it worked

We can monitor synthetic monitor every 15 mins
We use epics_awsgdmowner minion for aws services and epics_plminion_onprem for on-prem


# **APM data will have these verifications:**

For verifying our on prem nodes we will set up Alerts off of the APM data.  Since nodes are not as critical as a customer facing endpoint we fill ok with using APM data.   We won't use synthetics bcse this is duplicate work of what the APM data provides.

# **Alerts:**

we will have alerts that point to our synthetics and they will use this work flow pagerduty, towtruck email and slack channelwe will alerts that point to APM data and this work flow will be slack channel