# workflowAutomation_blueprint.html

This page (Datadog's Workflow Automation "Blueprints" catalog) lists 174 ready-made automation templates. Each one is a use case you can install with one click and tweak instead of building an automation from scratch. They're grouped below by what they're used for, in plain language.

## Incident Response & On-Call

- **Manually Triage Alerts in Real Time** — Lets a person quickly review and prioritize alerts as they come in.
- **Incident and Alert Routing with PagerDuty and Slack** — Sends alerts to the right on-call person through PagerDuty and posts updates in Slack.
- **Simplify Language of a Monitor Alert** — Rewrites a technical alert message into plain, easy-to-understand language.
- **Summarize Logs Fast with OpenAI** — Uses OpenAI to quickly summarize large amounts of log data into a short, readable summary.
- **Create and Enrich Case From Alert Event** — Turns an alert into a case and automatically adds useful extra details to it.
- **Declare PagerDuty Incident via Slack** — Lets someone start a PagerDuty incident directly from a Slack message.
- **Summarize Service Status with OpenAI** — Uses OpenAI to generate a plain-English summary of how a service is currently doing.
- **Summarize and triage alert with AI** — Uses AI to summarize an alert and suggest how urgent or important it is.
- **PagerDuty Create Incident** — Creates a new incident in PagerDuty automatically.
- **Retrieve existing incident data when handling an alert** — Pulls in details from a related, already-open incident when a new alert comes in.
- **Add Datadog Team to Incident Channel** — Automatically adds the right team to the chat channel created for an incident.
- **Create DORA Failure when Incident is Declared** — Automatically logs a failure event for DORA metrics whenever a new incident is declared.
- **Send a Slack Reminder to Complete Incident Postmortem** — Reminds the team in Slack to write up the postmortem after an incident is resolved.
- **Nudge Incident Commander about Old Incident** — Sends a reminder to the person leading an incident if it's been open too long.
- **Nudge for Missing Data in Incidents Blueprint** — Reminds people to fill in missing details on an open incident.
- **Page Teams Added to a High Severity Incident** — Automatically alerts (pages) any team that gets added to a high-severity incident.
- **Send Threaded Incident Updates** — Posts incident updates as replies in a single message thread instead of separate messages.
- **Send Slack Message to Incident Channel** — Posts an update message into the Slack channel created for an incident.
- **Ask a Question to Service Owner** — Sends a message to the person responsible for a service and asks them a question, then waits for their reply.

## Monitor & Alert Management

- **Mute a set of monitors** — Silences a group of alerts for a set period, for example during planned maintenance.
- **Unmute a set of monitors** — Turns alerts back on for a group of monitors that were previously silenced.
- **Clone Datadog Monitor** — Makes a copy of an existing monitor so it can be reused or adjusted for another service.
- **Check if service has any monitors in the alert state** — Checks whether a service currently has any active (firing) alerts.
- **Check if service has a cost monitor** — Checks whether a service has an alert set up to watch its cloud spending.
- **Restrict new monitors to tagged teams** — Automatically limits access to a new monitor to only the teams tagged on it.
- **Restrict new monitors to creator** — Automatically limits who can edit a newly created monitor to just the person who made it.
- **Restrict new dashboards to tagged teams** — Automatically limits access to a new dashboard to only the teams tagged on it.
- **Restrict new dashboards to creator** — Automatically limits who can edit a newly created dashboard to just the person who made it.
- **Create Standard Monitors for Service with Terraform** — Automatically sets up the standard set of monitoring alerts for a new service using Terraform.
- **Query Datadog Metrics Timeseries Points** — Pulls specific metric data points from Datadog for use elsewhere in a workflow.
- **Create a metric from a DDSQL query (count of hosts without an env tag)** — Builds a tracked metric that counts how many servers are missing an 'environment' label.

## Cloud Infrastructure & Cost Management

- **Mitigate Costs From Unused EBS Volumes** — Finds AWS storage disks that aren't being used and takes action to stop wasting money on them.
- **Detach and Delete a List of EBS Volumes** — Disconnects and deletes a list of unused AWS storage disks (EBS volumes).
- **Export all EBS volumes not in use from DDSQL as a CSV to S3** — Finds all unused AWS storage disks and saves the list as a spreadsheet file in S3.
- **Idle compute check via DDSQL with Slack Updates** — Finds servers that are sitting idle and posts a summary to Slack.
- **Check if 80% of a service's costs are allocated using the team tag** — Checks whether most (80%) of a service's cloud costs are properly labeled with a team tag, so spending can be tracked.
- **Check if a service's discount program coverage is at least 70%** — Checks whether enough of a service's infrastructure is covered by a cost discount program.
- **Perform AWS Autoscaling Instance Refresh** — Replaces the servers in an AWS auto-scaling group with fresh ones, for example after a new image is released.
- **Scale Capacity Up or Down with AWS Autoscaling** — Increases or decreases the number of running servers using AWS Auto Scaling.
- **Detach EC2 Instance from AWS Auto Scaling Group** — Removes a specific AWS server from an auto-scaling group without shutting it down.
- **Update EC2 Instances with AWS System Manager** — Applies updates or patches to AWS servers using AWS Systems Manager.
- **Enable Connection Draining for an ALB** — Turns on connection draining for an AWS load balancer, so in-progress requests finish safely before a server is removed.
- **Stop ECS Task** — Stops a running task in AWS ECS (a container service).
- **Perform Deployments with AWS CodeDeploy** — Rolls out a new application version to AWS servers using CodeDeploy.
- **Request and Tag Public Certificate with AWS ACM** — Requests a new public SSL/TLS certificate through AWS Certificate Manager and labels it properly.
- **Restart Azure VM and notify using MS Teams** — Restarts a virtual machine in Azure and posts an update in Microsoft Teams.
- **Run Azure DevOps Remediation Pipeline** — Triggers an Azure DevOps pipeline that automatically fixes a detected problem.
- **Periodically Update Allowlist With Datadog IPs** — Keeps a list of trusted (allowed) IP addresses up to date with Datadog's official IP ranges.

## Kubernetes & Deployments

- **Restart Kubernetes Deployment** — Restarts an application running in Kubernetes, useful when it needs a fresh start.
- **Restart Kubernetes Deployment from a Service** — Restarts the Kubernetes deployment tied to a specific service, straight from its service page.
- **Increase Kubernetes Replica Count for Service Using GitOps** — Scales up the number of running copies of a service in Kubernetes by updating its GitOps configuration.
- **Scale Kubernetes Deployment Memory Limit** — Adjusts how much memory a Kubernetes application is allowed to use.
- **Isolate and restart K8s pods** — Removes a problematic Kubernetes pod from service and restarts it.
- **Modify Blue Green Deployment Strategy** — Changes the settings of a blue-green deployment, a method for releasing new app versions with minimal downtime.
- **Release New Features Incrementally with LaunchDarkly Feature Flags** — Slowly rolls out a new feature to more users over time using LaunchDarkly feature flags.
- **Remediate by Toggling off Flag in LaunchDarkly** — Turns off a feature flag in LaunchDarkly automatically to fix or roll back a problem.

## Developer Workflow & Code Management

- **Restart Service via Github Actions** — Triggers a GitHub Actions workflow to restart a service.
- **Restart Service via Github Actions from Software Catalog** — Restarts a service through GitHub Actions, launched directly from its entry in the Software Catalog.
- **Ping Last Committer in GitHub** — Notifies the last person who made a code change in GitHub, for example when something breaks.
- **Ask for Approval of Merge Requests Older than 2 Weeks** — Finds code merge requests that have been waiting more than two weeks and asks someone to approve or reject them.
- **Send Slack Message with All Open Merge Requests from GitLab** — Posts a Slack message listing every merge request in GitLab that's still waiting to be reviewed.
- **Scaffold New Service with Github** — Sets up the starting files and structure for a new service in GitHub.
- **Scaffold New Service with GitLab** — Sets up the starting files and structure for a new service in GitLab.
- **Identify and Process Failed Jobs From CircleCI Workflow** — Finds failed build jobs in CircleCI and automatically handles them (for example, by notifying someone or retrying).
- **Check if a service has a tier defined** — Checks whether a service has been marked with an importance level (tier), and flags it if not.
- **Send Scorecard Report to Service Owners** — Sends each service owner a report card showing how their service is scoring against best practices.

## Learning Guides (How To)

- **How to Use Variables** — A guide explaining how to store and reuse values (variables) inside a workflow.
- **How to Use Loops** — A guide explaining how to repeat steps automatically in a workflow using loops.
- **How to Use Datastore** — A guide explaining how to store and reuse data within a workflow.
- **How to Migrate from For Each to For Loop** — A guide showing how to switch a workflow from using a 'For Each' step to a 'For Loop' step.

## Security: Check if Something Is Dangerous (Threat Assessment)

- **Assess IP Threat with AbuseIPDB** — Looks up an IP address in AbuseIPDB to see how risky or dangerous it is.
- **Assess IP Threat with APIVoid** — Looks up an IP address in APIVoid to see how risky or dangerous it is.
- **Assess IP Threat with Anomali ThreatStream** — Looks up an IP address in Anomali ThreatStream to see how risky or dangerous it is.
- **Assess IP Threat with URLScan** — Looks up an IP address in URLScan to see how risky or dangerous it is.
- **Assess URL Threat with Google Safe Browsing** — Looks up a URL in Google Safe Browsing to see how risky or dangerous it is.
- **Assess URL Threat with APIVoid** — Looks up a URL in APIVoid to see how risky or dangerous it is.
- **Assess URL Threat with URLScan** — Looks up a URL in URLScan to see how risky or dangerous it is.
- **Assess URL Threat with Anomali ThreatStream** — Looks up a URL in Anomali ThreatStream to see how risky or dangerous it is.
- **Assess Domain Threat with APIVoid** — Looks up a domain in APIVoid to see how risky or dangerous it is.
- **Assess Domain Threat with Anomali ThreatStream** — Looks up a domain in Anomali ThreatStream to see how risky or dangerous it is.
- **Assess Domain Threat with URLScan** — Looks up a domain in URLScan to see how risky or dangerous it is.
- **Assess Email Threat with APIVoid** — Looks up an email address in APIVoid to see how risky or dangerous it is.
- **Assess Email Threat with Anomali ThreatStream** — Looks up an email address in Anomali ThreatStream to see how risky or dangerous it is.
- **Assess Hash Threat with URLScan** — Looks up a file hash in URLScan to see how risky or dangerous it is.
- **Assess Hash Threat with Anomali ThreatStream** — Looks up a file hash in Anomali ThreatStream to see how risky or dangerous it is.
- **Assess ASN Threat with URLScan** — Looks up a network (ASN) in URLScan to see how risky or dangerous it is.
- **Detect IP Threat with MISP** — Checks MISP's threat database to see if an IP address is already known to be malicious.
- **Detect URL Threat with MISP** — Checks MISP's threat database to see if a URL is already known to be malicious.
- **Detect Hash Threat with MISP** — Checks MISP's threat database to see if a file hash is already known to be malicious.
- **Check IP with GreyNoise and Block Using Cloudflare** — Checks if an IP address is known to be harmful using GreyNoise, and blocks it in Cloudflare if it is.
- **Enrich IP Details with Censys** — Looks up extra details about an IP address (like open ports and services) using Censys.
- **Identify Phishing URL with PhishTank** — Checks whether a link is a known phishing site, using the PhishTank database.
- **Identify Abusive Phone Number with APIVoid** — Checks whether a phone number has a history of spam or abuse, using APIVoid.
- **Detect Malicious Files using Malshare** — Checks a file against the Malshare database to see if it's known malware.
- **Create IOC Event in MISP** — Adds a new malicious indicator (like an IP or file hash) into the MISP threat-sharing database.
- **Detect Emerging Vulnerabilities** — Watches for newly discovered security vulnerabilities that could affect your systems.

## Security: Block Dangerous Traffic

- **Block IP with Cloudflare** — Blocks a single malicious IP address using Cloudflare so it can no longer reach your systems.
- **Block a set of IPs in CloudFlare** — Blocks a whole list of malicious IP addresses at once using Cloudflare.
- **Block IP with Fastly** — Blocks a malicious IP address using Fastly so it can no longer reach your systems.
- **Investigate and Block Malicious IPs in AWS WAF** — Looks into suspicious IP addresses and blocks the dangerous ones using AWS's Web Application Firewall.

## Security: Lock Down a Compromised Account

- **Suspend Suspicious Okta User** — Temporarily disables an Okta account that's showing suspicious activity.
- **Suspend Okta Account and Revoke Sessions** — Temporarily disables an Okta account and logs it out everywhere.
- **Suspend Okta Device** — Temporarily disables a device registered in Okta.
- **Unlock Locked out Okta User** — Unlocks an Okta account that got locked out, for example after too many failed logins.
- **Deactivate Okta Device** — Turns off a device registered in Okta so it can no longer be used to log in.
- **Delete Okta User** — Permanently removes a user account from Okta.
- **Delete Okta API Token** — Revokes and deletes an API token in Okta so it can no longer be used.
- **Dormant Okta Users Cleanup** — Finds Okta accounts that haven't been used in a long time and cleans them up.
- **Remove Okta user from assigned groups and apps** — Removes a user from their groups and connected apps in Okta.
- **Add an Existing Okta User to a Group** — Adds a user in Okta to a specific group, which controls what they can access.
- **Restrict Okta User Access and Credential Reset** — Limits a user's access in Okta and forces them to reset their credentials.
- **Block Auth0 Account and Revoke Sessions** — Locks an Auth0 user account and logs them out of every active session.
- **Lock Auth0 User** — Locks a user's Auth0 account so they can't log in.
- **Delete Auth0 User** — Permanently removes a user account from Auth0.
- **Unblock Auth0 User** — Removes a block on an Auth0 user account, letting them log in again.
- **Rotate Auth0 User Credentials** — Forces a user's Auth0 password or credentials to be changed.
- **Remove Assigned Roles and Permissions from Auth0 User** — Strips away a user's roles and permissions in Auth0.
- **Revoke Auth0 User MFA Browsers, Sessions, and Tokens** — Logs a user out everywhere and resets their two-factor authentication in Auth0.
- **Verify Auth0 Blocked IP and Unblock** — Checks whether an IP address that was blocked in Auth0 is now safe, and unblocks it if so.
- **Contain Compromised User in Azure Entra** — Locks down a suspicious user account in Azure Entra (Azure AD) to stop an attacker from using it.
- **Disable Entra ID User** — Turns off a user account in Azure Entra ID (Azure AD) without deleting it.
- **Delete Entra ID User** — Permanently removes a user account from Azure Entra ID (Azure AD).
- **Disable Device with Entra ID** — Turns off a device in Azure Entra ID so it can no longer access company resources.
- **Remove User Role with Entra ID** — Takes away a specific role or permission from a user in Azure Entra ID.
- **Restrict Access to Sensitive Apps with Entra ID** — Limits who can open sensitive applications, enforced through Azure Entra ID.
- **Restrict High Risk Users Login with Entra ID** — Blocks or limits login for users flagged as high-risk in Azure Entra ID.
- **Suspend Google Workspace User and Credential Reset** — Suspends a Google Workspace account and resets its credentials.
- **Reset Credentials and Revoke in Google Workspace** — Resets a user's password and logs them out of all sessions in Google Workspace.
- **Delete Google Workspace User** — Permanently removes a user account from Google Workspace.
- **Remove Google Workspace User from Groups** — Removes a user from all their groups in Google Workspace, cutting off shared access.
- **Manage Super Admin Role with Google Workspace** — Adds or removes the highest level of admin access for a user in Google Workspace.
- **Suspend JumpCloud User** — Temporarily disables a user's account in JumpCloud.
- **Lock JumpCloud User** — Locks a user's JumpCloud account so they can't log in.
- **Delete JumpCloud User** — Permanently removes a user account from JumpCloud.
- **Erase JumpCloud System** — Wipes a device that's managed through JumpCloud, usually because it was lost, stolen, or compromised.
- **Remove JumpCloud User from User Groups** — Removes a user from their groups in JumpCloud, cutting off shared access.
- **Remove Suspicious JumpCloud User from Systems** — Removes a suspicious user's access to the systems they're connected to in JumpCloud.
- **Enforce MFA & Password Reset for JumpCloud Admins** — Forces JumpCloud administrators to turn on multi-factor authentication and reset their passwords.
- **Review and Manage Policy for JumpCloud** — Checks and updates security policies configured in JumpCloud.
- **Compromised M365 user triage** — Walks through the steps to investigate and contain a Microsoft 365 account that might be compromised.

## Security: Contain a Compromised Device

- **Contain Host and Block IOCs with CrowdStrike** — Isolates an infected computer and blocks known malicious indicators using CrowdStrike.
- **Contain Mobile Host & Block IOCs with CrowdStrike** — Isolates an infected mobile device and blocks known malicious indicators using CrowdStrike.
- **Kill Suspicious Process with CrowdStrike** — Stops a suspicious running program on a device, using CrowdStrike.
- **Threat Hunt Command-Line Execs with CrowdStrike** — Searches CrowdStrike across all devices for suspicious command-line activity, so analysts can spot attacks early.
- **Lift Containment Host and Allow IOCs with CrowdStrike** — Reverses an earlier lockdown on a device and un-blocks previously flagged indicators, using CrowdStrike.
- **Isolate Endpoint with SentinelOne** — Cuts off a compromised computer from the network using SentinelOne, so it can't spread an infection.
- **Unisolate Endpoint with SentinelOne** — Reconnects a device to the network after it was isolated, using SentinelOne.
- **Kill Malicious Processes with SentinelOne** — Stops harmful programs that are running on a device, using SentinelOne.
- **Quarantine Files & Remediate with SentinelOne** — Isolates a malicious file and cleans up the infected device using SentinelOne.
- **Create IOC and Block File Hash with SentinelOne** — Adds a malicious file's fingerprint (hash) to SentinelOne's blocklist so it can't run anywhere.
- **Mitigate Ransomware Threat with SentinelOne** — Stops and cleans up a ransomware attack on a device using SentinelOne.
- **Threat Hunt Command-Line Execs with SentinelOne** — Searches SentinelOne across all devices for suspicious command-line activity, so analysts can spot attacks early.
- **Isolate, Quarantine & Block IOCs with MS Defender** — Cuts off an infected device, quarantines the threat, and blocks known malicious indicators, using Microsoft Defender.
- **Isolate Machine and Restrict Apps with MS Defender** — Cuts off a compromised computer from the network and blocks apps from running on it, using Microsoft Defender.
- **Unisolate Machine and Allow Apps with MS Defender** — Reconnects a device and un-blocks its apps after it was isolated, using Microsoft Defender.
- **Quarantine Malicious File with Microsoft Defender** — Isolates a malicious file so it can't run, using Microsoft Defender.
- **Device Risk Analysis & Response with MS Defender** — Checks how risky a device is and takes action automatically, using Microsoft Defender.
- **Detect Task/Registry Persistence with MS Defender** — Looks for signs that malware has planted itself permanently on a Windows machine (via scheduled tasks or registry changes), using Microsoft Defender.
- **Monitor User/Group Persistence with MS Defender** — Watches for signs that an attacker is trying to keep long-term access by creating or modifying users and groups, using Microsoft Defender.
- **Threat Hunt Command-Line Execs with MS Defender** — Searches MS Defender across all devices for suspicious command-line activity, so analysts can spot attacks early.

## Security: AWS Account & Cloud Protection

- **AWS IAM Create User and Add to a IAM group** — Creates a new AWS user account and puts it into the right permissions group automatically.
- **AWS IAM Disable/Delete User** — Turns off or completely removes an AWS user account, for example after someone leaves the company.
- **AWS IAM Revoke Permissions (Remove User from Group)** — Takes away an AWS user's permissions by removing them from their access group.
- **Retrieve and Enrich AWS IAM User Details** — Looks up an AWS user account and gathers extra details about it for an investigation.
- **Compromised AWS Access Key Containment** — Immediately disables an AWS access key that may have been stolen or misused, to stop further damage.
- **Compromised AWS Access Key Identity Enrichment** — Gathers more details about who owns a suspicious AWS access key, to help investigate it.
- **Compromised AWS Access keys triage** — Walks through the steps to check, contain, and investigate an AWS access key that might be compromised.
- **S3 Block Public Access** — Turns on the setting that stops an AWS S3 storage bucket from being publicly accessible.
- **S3 Enable Default Bucket Encryption** — Turns on automatic encryption for everything stored in an AWS S3 bucket.
- **S3 Set Canned ACL** — Applies a pre-defined access permission template (ACL) to an AWS S3 bucket.
- **Notify on Slack if S3 Buckets are not Encrypted** — Checks AWS S3 storage buckets for missing encryption and warns the team in Slack.
- **Remediate issues using AWS Lambda** — Automatically fixes detected issues by triggering an AWS Lambda function.
- **Remediate Service Issues Using AWS Lambda** — Runs a small AWS Lambda function automatically to fix a known service problem.

## Security: Case & Ticket Management

- **Create a bidirectional Jira ticket for a security finding** — Creates a Jira ticket for a security issue, and keeps it synced both ways as the issue is updated.
