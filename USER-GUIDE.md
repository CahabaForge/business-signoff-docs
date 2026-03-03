# User Guide — Business Sign-off for Jira Data Center

**Version:** 1.0
**Last Updated:** [DATE]
**Vendor:** Cahaba Forge LLC

---

## Overview

Business Sign-off adds an approval panel directly to Jira issues. If your project has Business Sign-off enabled, you'll see the panel on the right side of the issue view. From there, you can view the current approval status, see who the approvers are, and — if you are an approver — record your decision.

---

## The Business Sign-off Panel

When you view an issue with Business Sign-off enabled, you'll see the sign-off panel in the right-side context area of the issue view.

[SCREENSHOT: A Jira issue view with the Business Sign-off panel visible on the right side, showing the panel title "Business Sign-off", the overall status lozenge, the approval progress bar, and a list of three approvers with different statuses]

### Panel Elements

| Element | Description |
|---|---|
| **Overall Status** | A colored lozenge showing the current approval state: Awaiting Decisions (blue), Approval Passed (green), or Approval Failed (red) |
| **Approval Progress** | Shows the count of approvals vs. the total number of approvers and the configured threshold |
| **Approver List** | Each approver with their avatar, display name, decision status, and any comments |
| **Action Buttons** | Buttons for adding approvers, recording decisions, and sending notifications (based on your permissions) |

---

## Understanding Approval Status

### Approver Statuses

Each individual approver has one of these statuses:

| Status | Icon | Meaning |
|---|---|---|
| **Added** | Grey circle | Approver has been assigned but not yet notified |
| **Pending** | Yellow clock | Approver has been notified and is awaiting their decision |
| **Approved** | Green checkmark | Approver has approved |
| **Rejected** | Red X | Approver has rejected |

### Overall Issue Status

The issue's overall approval status depends on the configured threshold and all approver decisions:

| Status | Meaning |
|---|---|
| **Awaiting Decisions** | One or more approvers have not yet made a decision |
| **Approval Passed** | The percentage of approvals meets or exceeds the threshold |
| **Approval Failed** | All approvers have decided and the approval percentage is below the threshold |

**Example with 75% threshold and 4 approvers:**
- 3 Approved, 1 Rejected = 75% = **Approval Passed**
- 2 Approved, 2 Rejected = 50% = **Approval Failed**
- 2 Approved, 1 Rejected, 1 Pending = **Awaiting Decisions**

---

## Approving or Rejecting

If you are assigned as an approver on an issue, you can record your decision directly from the issue panel.

### Recording Your Decision

1. Open the Jira issue
2. Find the Business Sign-off panel on the right side
3. Click the **Approve** or **Reject** button next to your name

[SCREENSHOT: The Business Sign-off panel with the current user's row highlighted, showing the Approve (green checkmark) and Reject (red X) buttons visible]

4. A decision dialog appears:
   - Select **Approve** or **Reject**
   - Enter an optional comment (or required, depending on your project's configuration)
   - Click **Submit**

[SCREENSHOT: The approval decision dialog showing the Approve/Reject radio buttons (Approve selected), the comment text area with placeholder text "Enter your comments...", the character counter showing "0/500", and the Submit and Cancel buttons]

5. Your decision is immediately recorded and the overall status updates

[SCREENSHOT: The Business Sign-off panel after a decision, showing the user's status changed to "Approved" with a green checkmark, their comment displayed below, and the overall status lozenge updated]

### Decision Comments

Depending on your project's configuration, you may be required to provide a comment when:
- Approving only
- Rejecting only
- Both approving and rejecting
- Neither (comments optional)

Comments are limited to 500 characters. Your comment becomes part of the permanent audit trail.

---

## Viewing Approval Details

### Approver Information

Click on any approver in the list to see their details:
- Display name and avatar
- Current decision status
- Decision date and time
- Decision comment (if provided)
- When they were added and by whom

[SCREENSHOT: An expanded approver row showing the avatar, display name, status badge, decision date, comment text, and "Added by [user] on [date]" timestamp]

### Eligibility Badges

Approvers may display badges indicating special conditions:

| Badge | Meaning |
|---|---|
| **SoD** | User is ineligible due to Segregation of Duties (they are the reporter or assignee) |
| **Ineligible** | User does not meet the eligible approver criteria (not in required role/group) |

[SCREENSHOT: An approver entry with a "SoD" badge next to the name, with a tooltip reading "Segregation of Duties: Issue assignee cannot be an approver"]

---

## Managing Approvers

If you have permission to manage approvers, you can add and remove approvers. Your administrator configures who can manage approvers — options include the issue reporter, issue assignee, and Jira administrators (system admins, Jira admins, and project admins). Workflow automation accounts can always manage approvers.

### Adding an Approver

1. Click the **Add Approver** button (person-plus icon) in the panel header
2. Start typing a user's name or username in the search field
3. Select the user from the dropdown results
4. The user is added as an approver with "Added" status

[SCREENSHOT: The Add Approver interface showing the Select2 type-ahead search field with search results displaying user avatars, display names, and email addresses, with one user highlighted]

**Note:** The search results only show users who are eligible to be approvers based on your project's configuration. Users who violate SoD rules or don't match eligible approver filters will not appear.

### Browsing All Eligible Approvers

If you need to see all eligible approvers rather than searching by name:

1. Click the **Browse** button (people icon) next to the search field
2. A list of all eligible approvers loads
3. Scroll down to load more results
4. Click a user to add them

[SCREENSHOT: The Browse Eligible Approvers dropdown showing a scrollable list of all eligible users with avatars and display names, with a "Loading more..." indicator at the bottom]

### Removing an Approver

1. Find the approver in the list
2. Click the **Remove** button (trash icon) next to their name
3. Confirm the removal

**Note:** Removing an approver is recorded in the audit trail. You can only remove approvers if you have manage-approver permissions.

[SCREENSHOT: The approver row with the Remove button (trash icon) visible on hover, and the confirmation dialog asking "Remove [user] as approver?"]

### Sending Notifications

If approvers need a reminder, you can notify all pending approvers:

1. Click the **Notify** button in the panel header
2. Choose a notification action:
   - **Send Notification**: Sends an email to all approvers who have not yet decided (Pending or Added status)
   - **Request Re-review**: Resets approvers who have already decided (Approved/Rejected) back to Pending status and sends notifications to all approvers
3. Click the action button to confirm

[SCREENSHOT: The Notify Approvers dialog showing the two action options — "Send Notification" for pending approvers and "Request Re-review" to reset decided approvers — with a confirmation button]

---

## Custom Fields on Create/Edit Screens

If your project administrator has added the BSO - Approvers custom field to the Create or Edit Issue screens, you can manage approvers directly from those screens.

### Adding Approvers on Create Issue

1. Open the **Create Issue** dialog
2. Find the **BSO - Approvers** field
3. Start typing a user's name — the type-ahead search shows eligible approvers for the selected project
4. Select one or more approvers
5. Create the issue — approvers are assigned immediately

[SCREENSHOT: The Jira Create Issue dialog with the BSO - Approvers multi-user picker field showing selected approvers as tags and the type-ahead search dropdown with results]

**Dynamic context**: If you change the project, assignee, or reporter in the create dialog, the approver field automatically re-validates. Approvers who become ineligible (e.g., due to SoD rules if you set them as the assignee) are automatically removed with a notification.

### Viewing Approval Status in Issue Lists

The **BSO - Status** custom field can be added as a column in issue navigators, boards, and dashboards. It displays a colored lozenge:
- **Approval Passed** — green
- **Approval Failed** — red
- **Awaiting Decisions** — blue
- Empty — no approvers assigned

[SCREENSHOT: A Jira issue navigator list view with the "BSO - Status" column showing colored lozenges for several issues]

---

## Searching with JQL

Business Sign-off provides custom JQL functions to search for issues based on approval data.

### Find Issues by Approver

```
issue in bsoApprovers("jsmith")
```
Returns all issues where "jsmith" is an approver (regardless of their decision).

### Find Issues by Approver and Status

```
issue in bsoApproverStatus("jsmith", "PENDING")
```
Returns issues where "jsmith" is an approver with a PENDING decision.

Valid status values: `ADDED`, `PENDING`, `APPROVED`, `REJECTED`

### Find Issues by Overall Approval Status

```
issue in bsoStatus("PASSED")
```
Returns issues where the overall approval has passed.

Valid values: `PASSED`, `FAILED`, `PENDING`

### Using with the BSO - Status Field

```
"BSO - Status" = "Approval Passed"
"BSO - Status" IS NOT EMPTY
```

JQL autocomplete suggests values when typing in the field: "Approval Passed", "Approval Failed", "Awaiting Decisions".

[SCREENSHOT: The Jira JQL search bar with autocomplete showing suggested values for "BSO - Status" field]

---

## Email Notifications

Depending on your project's configuration, you may receive email notifications for:

| Notification | When | Who Receives |
|---|---|---|
| **Approver Added** | When you are assigned as an approver | The added approver |
| **Approval Requested** | When a bulk notification is sent | All pending approvers |
| **Approval Reminder** | When a reminder is triggered | Pending approvers |
| **Decision Made** | When any approver records a decision | Reporter and/or Assignee (configurable) |
| **Outcome Reached** | When the overall approval passes or fails | Reporter and/or Assignee (configurable) |

Each notification email includes the issue key, summary, and a direct link to the issue.

[SCREENSHOT: An example email notification showing the subject "Business Sign-off: Approval Requested for PROJ-123", the issue summary, a list of pending approvers, and a "View Issue" button linking to the issue]

---

## Common Scenarios

### Scenario: Change Approval Board

A team requires three senior engineers to approve a deployment issue before it can move to "Done":

1. Engineers are added as approvers (manually or via workflow post-function)
2. Each engineer reviews the issue and clicks **Approve** or **Reject** with a comment
3. The "Require Approval" workflow validator blocks the "Done" transition until the threshold is met
4. Once approved, the issue can transition to "Done"

### Scenario: Regulatory Sign-off

A compliance team needs documented sign-off with SoD enforcement:

1. SoD rules prevent the reporter (requester) from approving
2. Approvers are restricted to members of the "Compliance Reviewers" group
3. Comment is required on all decisions for audit documentation
4. Threshold is set to 100% (unanimous)
5. Quarterly, the compliance officer exports the audit trail CSV for auditors

### Scenario: Quick Peer Review

A development team wants lightweight peer approval before code merges:

1. BSO - Approvers field is on the Create Issue screen
2. Developer adds a peer reviewer when creating the issue
3. Reviewer approves from the issue panel (no comment required)
4. Threshold is 50% with one approver = instant pass

---

*For administrator setup instructions, see the [Administrator Guide](../plugin/docs/guides/ADMIN-GUIDE.md).*

*Cahaba Forge LLC | https://cahabaforge.com*
