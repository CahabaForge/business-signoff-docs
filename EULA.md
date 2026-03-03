# End User License Agreement (EULA) — Business Sign-off for Jira Data Center

**Effective Date:** February 17, 2026
**Last Updated:** February 17, 2026
**Vendor:** Cahaba Forge LLC

---

## 1. Definitions

- **"Software"** means the Business Sign-off plugin for Jira Data Center, including all updates, patches, documentation, and related materials provided by Cahaba Forge LLC.
- **"Licensee"** or **"You"** means the individual or entity that has acquired a valid license for the Software from Cahaba Forge LLC or an Authorized Reseller.
- **"Licensor"** or **"We"** means Cahaba Forge LLC.
- **"Authorized Users"** means the individuals authorized by the Licensee to use the Software, as limited by the applicable license tier.
- **"Authorized Reseller"** means an Atlassian Solutions Partner or other entity authorized by Cahaba Forge LLC to distribute the Software.
- **"Order"** means the purchase agreement, invoice, or order form under which You acquire a license for the Software from Cahaba Forge LLC or an Authorized Reseller.

---

## 2. License Grant

Subject to the terms of this Agreement and payment of applicable fees as set forth in the applicable Order, Cahaba Forge LLC grants You a limited, non-exclusive, non-transferable, non-sublicensable license to:

a) Install and use the Software on Your Jira Data Center instance(s) for the number of Authorized Users specified in Your Order.

b) Make one (1) backup copy of the Software for archival purposes.

c) Use the Software's exported public API (`io.cahaba.jira.signoff.api` package) for custom integrations within Your Jira instance, including ScriptRunner scripts and custom workflow extensions.

### 2.1 Fees and Payment

License fees are as set forth in the applicable Order. All fees are due within thirty (30) days of the invoice date and are non-refundable except as expressly stated in this Agreement. Cahaba Forge LLC reserves the right to modify pricing for future renewal periods upon thirty (30) days' prior written notice.

### 2.2 Trial License

The Software includes a one-time, automatic thirty (30) day free trial period during which full functionality is enabled. Upon expiration of the trial period, a valid paid license is required for continued use. Additional trial licenses may be granted at the sole discretion of Cahaba Forge LLC upon request.

---

## 3. License Restrictions

You shall NOT:

a) Modify, adapt, translate, reverse engineer, decompile, disassemble, or create derivative works based on the Software, except to the extent permitted by applicable law.

b) Distribute, sublicense, lease, rent, loan, or otherwise transfer the Software or any license rights to any third party.

c) Remove, alter, or obscure any proprietary notices, labels, or marks on the Software.

d) Use the Software to develop a competing product or service.

e) Use the Software in any manner that violates applicable laws or regulations.

f) Exceed the number of Authorized Users specified in Your Order.

g) Share, publish, or distribute the Software's license key or activation credentials.

h) Use the Software for High-Risk Activities. "High-Risk Activities" means activities where use or failure of the Software could lead to death, personal injury, or environmental damage, including life support systems, nuclear facilities, air traffic control, weapons systems, or any other use where the Software is used as a component of a safety-critical system.

---

## 4. Intellectual Property

The Software is the intellectual property of Cahaba Forge LLC and is protected by copyright, trade secret, and other intellectual property laws. Cahaba Forge LLC retains all right, title, and interest in and to the Software, including all copies, modifications, and derivative works. This Agreement does not convey any ownership rights.

The Software includes the following third-party open-source component:
- **Apache Commons CSV 1.10.0** — Licensed under the Apache License 2.0

All other dependencies (Jira API, ActiveObjects, Spring Scanner, etc.) are provided by the Jira Data Center platform and are not distributed with the Software.

---

## 5. Data Processing

The Software runs entirely on Your infrastructure. It does not transmit any data to Cahaba Forge LLC, Atlassian, or any third party. The Software makes zero external network calls — it does not phone home, transmit telemetry, or communicate with any server outside Your Jira instance.

The Software creates database tables within Your Jira database to store approver assignments, approval history (audit trail), project configuration, and export task tracking. All data processing occurs within Your Jira Data Center instance and is subject to Your organization's existing data governance policies.

For detailed information on data stored, data retention, GDPR considerations, and Your rights as data controller, see the [Cahaba Forge Privacy Policy](https://cahabaforge.com/legal/privacy/).

---

## 6. License Enforcement

### 6.1 License Validation

The Software includes a built-in license module that validates license status based on a license key provided by Cahaba Forge LLC or an Authorized Reseller. A valid license is required for the Software to function beyond the trial period.

### 6.2 License States

The Software recognizes the following license states:

| State | Behavior |
|-------|----------|
| **Valid** | Full functionality enabled |
| **Trial** | Full functionality enabled for the thirty (30) day trial period |
| **Grace Period** | Full functionality enabled for thirty (30) days after license expiration |
| **Expired** | Core approval operations are blocked; existing data remains accessible read-only |
| **User Mismatch** | Functionality restricted when licensed user count is exceeded |
| **Invalid / None** | All plugin operations are blocked; admin UI displays license status |

### 6.3 Grace Period

When a paid license expires, the Software provides a thirty (30) day grace period during which full functionality remains enabled and informational messages are displayed in the admin UI indicating the expiration. After the grace period, the Software transitions to the Expired state as described in Section 6.2.

### 6.4 Data Preservation

License expiration or removal does **not** delete any data. All approver records, audit history, and configuration are preserved in the database and become fully accessible again upon license renewal.

---

## 7. Warranties and Disclaimers

### 7.1 Limited Warranty

Cahaba Forge LLC warrants that:

a) The Software will substantially conform to its published documentation for a period of ninety (90) days from the date of initial license purchase.

b) The Software does not contain any known malicious code, backdoors, or hidden functionality designed to disable, damage, or gain unauthorized access to Your systems.

### 7.2 Warranty Remedy

a) You must report any claim of breach of the Limited Warranty in reasonable detail within the ninety (90) day warranty period ("Claim").

b) Upon receiving a verified Claim, Cahaba Forge LLC will have thirty (30) days to use commercially reasonable efforts to correct the non-conformance or provide a reasonable workaround ("Fix Period").

c) If Cahaba Forge LLC fails to provide a correction or reasonable workaround within the Fix Period, You may terminate the applicable license and Cahaba Forge LLC will refund to You any prepaid, unused fees for the remainder of the then-current Subscription Term on a prorated basis.

d) THE REMEDY SET FORTH IN THIS SECTION 7.2 IS YOUR EXCLUSIVE REMEDY AND CAHABA FORGE LLC'S SOLE LIABILITY FOR BREACH OF THE LIMITED WARRANTY IN SECTION 7.1(a).

### 7.3 Disclaimer

EXCEPT AS EXPRESSLY STATED IN SECTION 7.1, THE SOFTWARE IS PROVIDED "AS IS" AND "AS AVAILABLE" WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE IMPLIED WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, AND NON-INFRINGEMENT. CAHABA FORGE LLC DOES NOT WARRANT THAT THE SOFTWARE WILL BE ERROR-FREE, UNINTERRUPTED, OR FREE OF VULNERABILITIES.

### 7.4 Compliance Disclaimer

While the Software provides features designed to support SOC 2, SOX, and other compliance frameworks (such as Segregation of Duties enforcement and immutable audit trails), Cahaba Forge LLC does not guarantee that use of the Software will ensure compliance with any specific regulatory requirement. Compliance depends on Your organization's overall policies, procedures, and controls. Consult your compliance officer or auditor.

---

## 8. Limitation of Liability

TO THE MAXIMUM EXTENT PERMITTED BY APPLICABLE LAW:

a) IN NO EVENT SHALL CAHABA FORGE LLC BE LIABLE FOR ANY INDIRECT, INCIDENTAL, SPECIAL, CONSEQUENTIAL, OR PUNITIVE DAMAGES, INCLUDING BUT NOT LIMITED TO LOSS OF PROFITS, DATA, BUSINESS OPPORTUNITIES, OR GOODWILL, ARISING OUT OF OR IN CONNECTION WITH THIS AGREEMENT OR THE USE OF THE SOFTWARE.

b) CAHABA FORGE LLC'S TOTAL AGGREGATE LIABILITY UNDER THIS AGREEMENT SHALL NOT EXCEED THE AMOUNT PAID BY THE LICENSEE FOR THE SOFTWARE IN THE TWELVE (12) MONTHS PRECEDING THE CLAIM.

c) THE LIMITATIONS IN THIS SECTION APPLY REGARDLESS OF THE FORM OF ACTION, WHETHER IN CONTRACT, TORT, STRICT LIABILITY, OR OTHERWISE, AND EVEN IF CAHABA FORGE LLC HAS BEEN ADVISED OF THE POSSIBILITY OF SUCH DAMAGES.

---

## 9. Indemnification

You agree to indemnify, defend, and hold harmless Cahaba Forge LLC from and against any claims, damages, losses, and expenses (including reasonable attorneys' fees) arising from:

a) Your use of the Software in violation of this Agreement.

b) Your violation of applicable laws or regulations.

c) Any data processing You perform using the Software that violates applicable data protection laws.

---

## 10. Confidentiality

### 10.1 Definition

"Confidential Information" means any non-public information disclosed by one party ("Discloser") to the other party ("Recipient") in connection with this Agreement that is designated as confidential or that reasonably should be understood to be confidential given the nature of the information and the circumstances of disclosure. Confidential Information includes, but is not limited to, technical data, system configurations, log files, error reports, and business information exchanged during support interactions.

### 10.2 Obligations

The Recipient shall: (a) use Confidential Information only to fulfill its obligations or exercise its rights under this Agreement, (b) not disclose Confidential Information to third parties without the Discloser's prior written consent, except to the Recipient's employees, contractors, or agents who have a need to know and are bound by confidentiality obligations no less protective than this Section 10, and (c) protect Confidential Information using at least the same degree of care it uses for its own similar information and no less than a reasonable standard of care.

### 10.3 Exclusions

Confidential Information does not include information that: (a) is or becomes publicly available through no fault of the Recipient, (b) was already known to the Recipient without restriction prior to disclosure, (c) is independently developed by the Recipient without use of the Discloser's Confidential Information, or (d) is rightfully received from a third party without restriction on disclosure. The Recipient may also disclose Confidential Information to the extent required by law, regulation, or court order, provided the Recipient gives the Discloser reasonable prior notice (where legally permitted) to allow the Discloser to seek a protective order.

### 10.4 Survival

The obligations under this Section 10 shall survive termination of this Agreement for a period of three (3) years.

---

## 11. Term and Termination

### 11.1 Term

This Agreement is effective from the date You acquire a valid license and continues until terminated.

### 11.2 Termination by Licensee

You may terminate this Agreement at any time by uninstalling the Software and destroying all copies.

### 11.3 Termination by Licensor

Cahaba Forge LLC may terminate this Agreement if You materially breach any term and fail to cure such breach within thirty (30) days of written notice.

### 11.4 Effect of Termination

Upon termination:
- Your license to use the Software is revoked
- You must uninstall the Software from all Jira instances
- Sections 4, 7, 8, 9, 10, and 12 survive termination
- Plugin data in Your database is not automatically deleted; You may retain or delete it at Your discretion

---

## 12. General Provisions

### 12.1 Governing Law

This Agreement shall be governed by and construed in accordance with the laws of the State of Alabama, United States, without regard to its conflict of law provisions.

### 12.2 Dispute Resolution

Any dispute arising under this Agreement shall be resolved through binding arbitration in accordance with the rules of the American Arbitration Association, with arbitration conducted in Alabama, United States, or as otherwise agreed in writing by the parties.

### 12.3 Entire Agreement

This Agreement, together with the applicable Order, the [Cahaba Forge Privacy Policy](https://cahabaforge.com/legal/privacy/), and the [Cahaba Forge Support Policy](https://cahabaforge.com/legal/support/), constitutes the entire agreement between the parties regarding the Software and supersedes all prior agreements and understandings.

### 12.4 Severability

If any provision of this Agreement is held to be unenforceable, the remaining provisions shall continue in full force and effect.

### 12.5 Assignment

You may not assign this Agreement without the prior written consent of Cahaba Forge LLC. Cahaba Forge LLC may assign this Agreement in connection with a merger, acquisition, or sale of all or substantially all of its assets.

### 12.6 Waiver

No waiver of any right under this Agreement shall be effective unless in writing and signed by the waiving party.

### 12.7 Modifications

Cahaba Forge LLC reserves the right to modify this Agreement at any time. Material changes will be communicated with at least thirty (30) days' prior notice through the Cahaba Forge website and/or email notification. Your continued use of the Software after the effective date of any modification constitutes Your acceptance of the modified terms. If You do not agree with any modification, Your sole remedy is to terminate this Agreement in accordance with Section 11.2.

### 12.8 Notices

All notices under this Agreement shall be in writing and sent to:

**Cahaba Forge LLC**
Email: info@cahabaforge.com
Website: https://cahabaforge.com

---

## 13. Support

Support for the Software is provided in accordance with the [Cahaba Forge Support Policy](https://cahabaforge.com/legal/support/). The Support Policy describes available support channels, response time targets, severity classifications, and scope of support. The Support Policy is incorporated by reference into this Agreement.

---

*By installing or using Business Sign-off for Jira Data Center, You acknowledge that You have read, understood, and agree to be bound by the terms of this End User License Agreement.*
