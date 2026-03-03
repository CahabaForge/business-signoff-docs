# Privacy Policy — Business Sign-off for Jira Data Center

**Effective Date:** February 17, 2026
**Last Updated:** February 19, 2026
**Vendor:** Cahaba Forge LLC

---

## Overview

Business Sign-off is a Jira Data Center plugin that runs entirely on your infrastructure. It does not transmit any data to Cahaba Forge, third-party services, or any external endpoint. All data is stored within your Jira Data Center instance using Jira's built-in database (ActiveObjects framework) and is subject to your organization's existing data governance policies.

---

## 1. Information We Collect

Business Sign-off reads and writes data exclusively within your Jira Data Center instance. It does **not** collect, transmit, or store data outside your infrastructure.

### Data Read from Jira (Not Stored Separately)

The plugin reads the following Jira data during normal operation. This data is accessed via standard Jira APIs and is never copied to external systems:

- **User information**: User keys, display names, email addresses, group memberships, and project role assignments (used for approver management, permission checks, eligible approver filtering, and email notifications)
- **Issue information**: Issue keys, IDs, summaries, types, priorities, statuses, reporter, and assignee (used for panel display, SoD checks, and audit context)
- **Project information**: Project keys, IDs, and project role configurations (used for permission checks and project-level configuration)
- **Workflow information**: Transition context during workflow function execution

### Data Stored by the Plugin

The plugin creates and manages four database tables using Jira's ActiveObjects framework. All data resides in your Jira database:

#### Table: `AO_SIGNOFF_APPROVER`
Stores approver assignments for each issue.
| Column | Data | Purpose |
|--------|------|---------|
| issueId | Jira issue internal ID | Links approver to issue |
| approverUserKey | Jira user key | Identifies the approver |
| status | ADDED, PENDING, APPROVED, REJECTED | Tracks decision state |
| comment | Free-text (unlimited length) | Approver's decision comment |
| createdDate | Timestamp | When the approver was assigned |
| createdByUserKey | Jira user key | Who assigned the approver |
| decisionDate | Timestamp | When the decision was made |
| lastNotifiedDate | Timestamp | When the approver was last emailed |

#### Table: `AO_SIGNOFF_HISTORY`
Immutable audit trail for compliance. Records are append-only and integrity-protected with SHA-256 hashes.
| Column | Data | Purpose |
|--------|------|---------|
| issueId, projectKey, issueKey | Issue identifiers | Links record to issue |
| issueSummary, issueType, issuePriority, issueStatus | Issue snapshot | Captures issue state at action time |
| action | Action type (e.g., APPROVER_ADDED, APPROVED) | What happened |
| eventTime | Timestamp | When it happened |
| actorUserKey, actorDisplayName, actorEmail | Actor snapshot | Who performed the action |
| targetUserKey, targetDisplayName, targetEmail | Target snapshot | The approver acted upon |
| reporterUserKey, reporterDisplayName, reporterEmail | Reporter snapshot | Issue reporter at action time |
| assigneeUserKey, assigneeDisplayName, assigneeEmail | Assignee snapshot | Issue assignee at action time |
| previousValue, newValue | State change | Before/after values |
| sodResult | PASS, FAIL, NOT_APPLICABLE | SoD validation outcome |
| comment | Decision comment | Text provided with the decision |
| recordHash | SHA-256 hex string (64 chars) | Tamper-detection hash |

**Note on PII in audit records:** The audit trail intentionally denormalizes user display names and email addresses as point-in-time snapshots. This is a compliance requirement — auditors need to see who acted and how they were identified at the time of the action, even if the user's details later change. These snapshots cannot be modified after creation.

#### Table: `AO_SIGNOFF_CONFIG`
Project-level configuration. One record per Jira project with Business Sign-off enabled.
| Column | Data | Purpose |
|--------|------|---------|
| projectId | Jira project ID | Links config to project |
| enabled, panelVisibility, approvalRequired | Booleans/strings | Feature toggles |
| approvalThreshold | Integer (50-100) | Approval pass percentage |
| requiredIssueTypes | Comma-separated issue type IDs | Issue types requiring approval |
| commentRequiredOn | ALL, APPROVAL_ONLY, REJECT_ONLY, NONE | When comments are mandatory |
| Email settings (5 columns) | Notification preferences | Email notification rules |
| SoD settings (2 columns) | Booleans | Segregation of Duties rules |
| Eligible approver settings (5 columns) | Mode, role IDs, group names | Who can be an approver |
| finishingMode | Boolean | Whether the project is in finishing mode (no new approvers) |

#### Table: `AO_SIGNOFF_EXPORT`
Tracks background audit CSV export tasks. Records are transient and cleaned up automatically.
| Column | Data | Purpose |
|--------|------|---------|
| taskId | UUID | Task identifier |
| state | RUNNING, COMPLETED, FAILED | Task progress |
| progress | Integer (0-100) | Completion percentage |
| fileName | String | CSV output filename |
| nodeId | String | Cluster node executing the task |
| errorMessage | Free-text (unlimited length) | Error details for failed tasks |
| Timestamps | Epoch milliseconds | Creation, completion, download times |

### Global Configuration Storage

Global plugin settings are stored using Jira's `PluginSettingsFactory` (Jira's standard plugin configuration store). Settings include:
- Plugin enabled/disabled flag
- Global finishing mode flag
- Approval threshold defaults (including project override permission and minimum threshold)
- SoD rule defaults
- Comment requirement settings
- Eligible approver mode and filter settings
- Debug logging toggle and expiry timestamp
- Approver management permission settings

#### License Data

The plugin stores license-related data in `PluginSettingsFactory` for local license validation. License validation is performed entirely on your infrastructure -- the plugin does not contact any external server to validate licenses.

- **License key:** A Base64-encoded, Ed25519-signed license blob containing the organization name, license type, expiration date, licensed server IDs, and seat count. The license key is provided by Cahaba Forge LLC or an Authorized Reseller and is stored locally for offline validation.
- **Auto-trial tracking:** The date the automatic 30-day trial was activated and a flag indicating whether the trial has been used.
- **Seat overage tracking:** The date when the licensed user count was first exceeded (used for grace period calculations).
- **License notification timestamps:** ISO date values recording when system administrators were last notified about license events (e.g., expiring, expired, seat overage). Used to prevent duplicate email notifications (at most one notification per event type per day).

No user credentials, passwords, API keys, or external authentication secrets are stored by the plugin. The license key contains an organization name but no individual personal data.

---

## 2. How We Use Information

All data processing occurs within your Jira Data Center instance for the following purposes:

- **Approver management**: Assigning, removing, and tracking approval decisions on issues
- **Permission enforcement**: Verifying that users have appropriate Jira permissions and meet eligibility criteria before performing actions
- **Segregation of Duties**: Preventing reporters/assignees from serving as approvers when SoD rules are configured
- **Audit trail**: Recording every approval-related action with full context for compliance reporting
- **Email notifications**: Sending approval-related notifications to approvers, reporters, and assignees using Jira's built-in mail system
- **License validation**: Verifying the license key locally using Ed25519 signature verification with an embedded public key. No external network calls are made for license validation.
- **License notifications**: Sending license status emails (expiring, expired, grace period, seat overage) to Jira system administrators via Jira's built-in mail system. These emails contain the administrator's display name, license status details, and the organization name from the license key. Notifications are sent at most once per day per event type.
- **Status calculation**: Computing approval pass/fail status based on configured thresholds
- **JQL search**: Enabling custom JQL functions to search issues by approver, approver status, or overall approval status

---

## 3. Data Storage

- **Location**: All data is stored in your Jira Data Center database using the ActiveObjects framework. The data resides wherever your Jira database is hosted.
- **Encryption at rest**: Subject to your database encryption configuration. The plugin does not implement its own encryption layer.
- **Encryption in transit**: Subject to your Jira instance's TLS/SSL configuration. The plugin does not make external network calls.
- **Temporary files**: Audit CSV exports are written to temporary files in the Jira shared home directory (`jiraHome.getHome()`). These files are accessible from all cluster nodes and are cleaned up after download or on a scheduled basis.
- **Backup**: Plugin data is included in your standard Jira database backups. No separate backup mechanism is required.

---

## 4. Data Retention

- **Approver records**: Retained as long as the associated Jira issue exists. When an issue is deleted, all approver records for that issue are automatically deleted within the same transaction.
- **Audit history records**: Retained as long as the associated Jira issue exists. Audit records are deleted when the parent issue is deleted. There is no separate retention period or automatic purging — records persist for the life of the issue to support compliance requirements.
- **Project configuration**: Retained as long as the Jira project exists. Deleted automatically when the project is deleted.
- **Export task records**: Transient. Completed and failed task records are cleaned up automatically.
- **Orphaned data cleanup**: When a project is deleted, a background task identifies and removes any approver or audit records associated with issues that no longer exist.
- **License data**: License key and associated tracking data (trial dates, notification timestamps) are retained in plugin settings until the license is removed or replaced by an administrator. This data is not automatically deleted when the plugin is uninstalled; administrators can clear it by removing the plugin settings from the database.

Cahaba Forge does not have access to your data and cannot control retention. Your organization is responsible for data retention policies applied to your Jira database.

---

## 5. Third-Party Sharing

**None.** Business Sign-off does not transmit any data to Cahaba Forge, Atlassian, or any third party. The plugin makes **zero external network calls**. All processing occurs within your Jira Data Center instance.

The only bundled third-party library is Apache Commons CSV 1.10.0, used exclusively for generating CSV export files locally. It does not perform any network operations.

---

## 6. Cookies and Tracking Technologies

Business Sign-off does not use cookies, web beacons, tracking pixels, browser fingerprinting, or any client-side tracking technologies. The plugin does not set or read any cookies in the user's browser. All client-side functionality is delivered through standard Jira web resource modules and does not include any analytics, telemetry, or tracking scripts.

---

## 7. User Rights

Because Business Sign-off is a Data Center plugin, your organization has full control over all data:

- **Access**: Jira administrators can query all plugin ActiveObjects tables directly via the database
- **Export**: The audit CSV export feature enables export of all approval history data. Individual approver data is accessible via the REST API.
- **Deletion**: Deleting a Jira issue automatically removes all associated approver and audit records. Jira administrators can also delete data directly from the database.
- **Correction**: Approver records can be modified through normal plugin operations (remove and re-add approvers). Audit history records are immutable by design for compliance purposes.

### GDPR Considerations

- **Right to access**: Users can view their approver assignments and decision history through the Jira issue panel and REST API
- **Right to erasure**: Deleting the Jira issues associated with a user's approver records will remove the data. Note that audit trail records are intentionally immutable to satisfy compliance requirements; erasure of audit records may conflict with regulatory obligations. Consult your Data Protection Officer.
- **Right to rectification**: Current approver assignments can be removed and re-added. Historical audit records are immutable by design.
- **Data portability**: The audit CSV export provides data in a portable format
- **Data minimization**: The plugin stores only the data necessary for approval workflow management and compliance audit trails

### Data Processing Addendum (GDPR)

For deployments subject to the EU General Data Protection Regulation (GDPR):

a) **Data Controller**: You (the Licensee) are the sole data controller for all personal data processed by the Software within your Jira instance.

b) **Data Processor**: Because the Software runs entirely on your infrastructure and Cahaba Forge LLC has no access to your data, Cahaba Forge LLC does not act as a data processor.

c) **Personal Data Processed**: The Software processes Jira user keys, display names, and email addresses as part of approver management and audit trail recording.

d) **Data Retention**: You control all data retention. Data is stored in your database for the lifetime of the associated Jira issue and is automatically deleted when the issue is deleted.

e) **Data Subject Rights**: You are responsible for fulfilling data subject requests (access, erasure, rectification, portability) using the plugin's REST API, CSV export functionality, and direct database access. Note that audit trail records are immutable by design for compliance purposes; erasure of audit records may conflict with regulatory retention obligations.

f) **Sub-Processors**: None. The Software does not use sub-processors or transmit data to third parties.

g) **International Transfers**: None. All data remains within your infrastructure.

Since this is a self-hosted Data Center plugin, your organization acts as the data controller and is responsible for fulfilling data subject requests. Cahaba Forge does not process, access, or store any of your data.

---

## 8. Children's Privacy

Business Sign-off is enterprise software designed for use in organizational settings. It is not intended for use by individuals under the age of 16 (or such younger age as permitted by applicable law). The plugin does not knowingly collect data from children.

---

## 9. Changes to This Privacy Policy

We may update this privacy policy to reflect changes in the plugin's data handling practices. Material changes will be communicated with at least thirty (30) days' prior notice through the Cahaba Forge website and/or email notification. The "Last Updated" date at the top of this document indicates when the policy was last revised.

---

## 10. Contact Information

For privacy-related questions or concerns:

**Cahaba Forge LLC**
Email: privacy@cahabaforge.com
Website: https://cahabaforge.com

---

*This privacy policy applies to Business Sign-off for Jira Data Center. Since this is a self-hosted plugin, all data processing occurs on your infrastructure under your control. Cahaba Forge has no access to your Jira instance or its data.*
