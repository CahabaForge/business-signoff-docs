# Support Policy — Business Sign-off for Jira Data Center

**Effective Date:** February 17, 2026
**Last Updated:** February 17, 2026
**Vendor:** Cahaba Forge LLC

---

## Support Tier

All customers with a valid license for Business Sign-off receive Standard Support as described in this policy. Cahaba Forge LLC reserves the right to offer additional support tiers in the future.

---

## Supported Versions

### Jira Data Center Compatibility

| Plugin Version | Supported Jira DC Versions | Status |
|---|---|---|
| 1.0.x | 10.3.x | Current |

### End-of-Life Policy

Cahaba Forge supports each plugin version for as long as its corresponding Jira Data Center version is supported by Atlassian, plus an additional six (6) months grace period. After the grace period, the plugin version enters end-of-life and receives security fixes only (no feature development or bug fixes).

When Atlassian releases a new major Jira Data Center version, Cahaba Forge will release a compatible plugin version within 90 days of Jira's general availability, subject to breaking API changes.

---

## Support Channels

### Primary Support

| Channel | Details |
|---|---|
| **Email** | support@cahabaforge.com |
| **Support Portal** | https://cahabaforge.com/support |

### Community Resources

- Atlassian Community: Search for "Business Sign-off" discussions
- Plugin documentation: Available at https://cahabaforge.com/docs

---

## Severity Classifications

| Severity | Description |
|---|---|
| **Critical** | Plugin causes Jira instance instability, data corruption, or complete loss of approval functionality across all projects |
| **High** | Major feature is non-functional (e.g., approvals cannot be recorded, audit trail not recording, workflow functions failing) |
| **Medium** | Feature works but with limitations or workaround required (e.g., email notifications not sending, CSV export failing, UI display issue) |
| **Low** | Questions, feature requests, documentation clarifications, minor cosmetic issues |

---

## Response Time Targets

Response times are measured in business days from the time a properly categorized support request is received through a supported channel.

| Severity | Target First Response |
|---|---|
| **Critical** | 1 business day |
| **High** | 2 business days |
| **Medium** | 3 business days |
| **Low** | 5 business days |

### Issue Resolution

Cahaba Forge will use commercially reasonable efforts to resolve confirmed defects as expeditiously as possible, with priority given based on severity classification. Resolution may include a workaround, patch, configuration change, or scheduled fix in the next release. Resolution timelines will depend on the severity and complexity of the issue.

### Important Notes

- Response time targets represent Cahaba Forge's operational goals and do not constitute a warranty or guarantee of response or resolution times. No service credits, refunds, or other remedies are provided for failure to meet these targets.
- Cahaba Forge will make commercially reasonable efforts to meet these targets.
- Response time targets apply to customers with a current, valid license.
- Response time targets do not apply during scheduled maintenance windows or force majeure events.

---

## Hours of Operation

| | Details |
|---|---|
| **Business Hours** | Monday through Friday, 9:00 AM – 5:00 PM Central Time (US) |
| **Timezone** | CT (UTC-6 / UTC-5 during daylight saving) |
| **Holidays** | US federal holidays observed |

Critical severity issues submitted outside business hours will be triaged on the next business day.

---

## How to Report Issues

### Bug Reports

When submitting a bug report, include the following information to help us resolve the issue quickly:

1. **Environment details**:
   - Jira Data Center version (e.g., 10.3.15)
   - Business Sign-off plugin version (e.g., 1.0.0)
   - Java version (e.g., OpenJDK 17.0.x)
   - Database type and version (e.g., PostgreSQL 15.4)
   - Number of cluster nodes
   - Browser and version (for UI issues)

2. **Problem description**:
   - What you expected to happen
   - What actually happened
   - Steps to reproduce the issue
   - How many users or projects are affected

3. **Supporting materials**:
   - Screenshots or screen recordings
   - Relevant Jira log entries (set plugin debug logging via global config for detailed logs)
   - REST API response bodies (for API-related issues)
   - Browser console output (for JavaScript issues)

4. **Severity assessment**:
   - Impact on your team (blocking, degraded, minor inconvenience)
   - Whether a workaround exists

### Enabling Debug Logging

Business Sign-off includes a built-in debug logging toggle in the global configuration page. Enable it to capture detailed plugin logs before reproducing the issue. Debug logging automatically expires after the configured duration to prevent log bloat.

### Feature Requests

Feature requests are welcome and can be submitted through the same support channels. Please include:

- A description of the desired functionality
- The business problem it would solve
- How you currently work around the missing feature (if applicable)
- Priority relative to other requests (nice-to-have vs. business-critical)

Feature requests are tracked and prioritized for future releases. There is no guaranteed timeline for feature request implementation.

---

## What Is Covered

Support covers:

- Installation and configuration assistance
- Bug diagnosis and resolution
- Guidance on workflow integration
- Clarification of plugin behavior and capabilities
- Assistance with upgrade procedures
- Compatibility questions

## What Is Not Covered

Support does not cover:

- General Jira administration (contact Atlassian Support)
- Custom ScriptRunner scripts that use the plugin's API (best-effort guidance only)
- Performance issues caused by non-plugin factors (insufficient hardware, database tuning, etc.)
- Third-party plugin conflicts (we will help isolate whether Business Sign-off is the cause)
- Data recovery from customer-initiated deletions
- Versions of the plugin that have reached end-of-life (security fixes only)

---

## Security Vulnerability Reporting

If you discover a security vulnerability in Business Sign-off, please report it responsibly:

1. Email security@cahabaforge.com with "SECURITY" in the subject line
2. Include a description of the vulnerability and steps to reproduce
3. Do not publicly disclose the vulnerability until a fix is available

Cahaba Forge targets the following remediation timelines for confirmed vulnerabilities:
- **Critical** vulnerabilities: Fix within 2 weeks of confirmation
- **High** vulnerabilities: Fix within 4 weeks of confirmation
- **Medium/Low** vulnerabilities: Fix in the next scheduled release

---

*Cahaba Forge LLC | https://cahabaforge.com*
