# soarWorkflows.html

This page is the security-focused slice of the Blueprints catalog — the SOAR (Security Orchestration, Automation and Response) workflows. It has 101 use cases, all also present in `workflowAutomation_blueprint.html`, but filtered down to just security tasks like checking threats, locking compromised accounts, and containing infected devices. Grouped below by what they're used for, in plain language.

## Cloud Infrastructure & Cost Management

- **Stop ECS Task** — Stops a running task in AWS ECS (a container service).

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

## Security: Case & Ticket Management

- **Create a bidirectional Jira ticket for a security finding** — Creates a Jira ticket for a security issue, and keeps it synced both ways as the issue is updated.
