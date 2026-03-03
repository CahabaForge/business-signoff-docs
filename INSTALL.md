# Business Sign-off for Jira -- Installation Guide

## What's in This ZIP

Extract all files from this ZIP to a folder on your Jira server:

| File | Purpose |
|------|---------|
| `business-signoff-X.Y.Z.jar` | The plugin |
| `business-signoff-X.Y.Z.sig` | Detached signature (proves the JAR is authentic) |
| `cahabaforge-cert.pem` | Cahaba Forge vendor certificate (one-time trust store import) |
| `admin-guide-X.Y.Z.html` | Administrator guide — configuration, REST API reference, and troubleshooting |
| `user-guide-X.Y.Z.html` | User guide — approving/returning issues, viewing sign-off status |
| `INSTALL.html` | This file |

## Before You Begin

- Jira Data Center 10.3+ required
- Jira admin permissions required
- Steps 1 and 2 below only need to be done once (skip if already completed)

---

## Step 1: Add the Cahaba Forge Certificate to the Jira Trust Store

### Jira 10.3 -- 10.4 -- SKIP

UPM does **not** support app signing in Jira 10.3 or 10.4. Skip directly
to Step 2.

### Jira 10.5 -- 10.7 -- OPTIONAL

Jira 10.5 through 10.7 ships with UPM app signing support, but it is
**disabled by default** during a grace period. The plugin will install
without the certificate unless your administrator has explicitly enabled
signature verification.

**You only need to install the certificate if:**
- Your Jira administrator has enabled app signing by setting
  `-Datlassian.upm.signature.check.disabled=false` (or using the UPM
  configuration), **or**
- You want to set it up now for a future upgrade to Jira 11.x

If neither applies, skip to Step 2. Otherwise, follow the instructions
below.

### Jira 11.x -- REQUIRED

Starting with Jira 11, UPM app signing is **enabled by default**. You
**must** install the Cahaba Forge certificate before uploading the plugin.

### Certificate Installation Steps

*Only required on first install -- skip if already done.*

1. Copy `cahabaforge-cert.pem` from this ZIP to your Jira server
2. Place it in: `<jira-home>/upmconfig/truststore/`
   - If these directories don't exist yet, create them and set read-only permissions:

         mkdir -p <jira-home>/upmconfig/truststore
         chmod 555 <jira-home>/upmconfig/
         chmod 555 <jira-home>/upmconfig/truststore/

   - If they already exist, skip the above -- the permissions are already correct
3. Set the certificate file to read-only:

       chmod 444 <jira-home>/upmconfig/truststore/cahabaforge-cert.pem

4. No restart required -- UPM picks up the certificate automatically

> **Tip:** Not sure where `<jira-home>` is? In Jira, go to
> **Administration > System > System Info** and look for the
> **Jira Home Directory** entry.

---

## Step 2: Enable Plugin Upload (if the Upload Button is Hidden)

*Only required once -- skip if you already see the "Upload app" button.*

Starting with Jira 9.4.17 / 10.x, the upload button is hidden by default.

1. Open `<jira-install>/bin/setenv.sh` (Linux) or `setenv.bat` (Windows)
2. Add this JVM parameter:

       -Dupm.plugin.upload.enabled=true

3. Restart Jira
4. The "Upload app" button will now appear in Manage Apps

> **Tip:** Atlassian recommends disabling this after upload for security.
> You can remove the parameter and restart after installing.

---

## Step 3: Install the Plugin

1. Log in to Jira as a system administrator
2. Go to **Administration > Manage Apps**
3. Click **Upload app**
4. Select `business-signoff-X.Y.Z.jar` from this ZIP
5. If UPM prompts for a signature file, upload `business-signoff-X.Y.Z.sig`
6. Click **Upload** -- Jira installs the plugin
7. No restart required

---

## Step 4: Verify Installation

1. Go to **Administration > Manage Apps**
2. Find **Business Sign-off** in the list
3. Verify the version number matches: X.Y.Z
4. The plugin is now active and ready to configure

---

## Upgrading

For future upgrades, only Step 3 is needed. The certificate (Step 1)
persists across upgrades. If you removed the `-Dupm.plugin.upload.enabled=true`
parameter after the initial install (as recommended in Step 2), you will need
to re-enable it before uploading the new version, then remove it again afterward.

---

## Alternative: File System Installation

If you prefer not to use the UI upload:

1. Copy `business-signoff-X.Y.Z.jar` to:
   `<jira-shared-home>/plugins/installed-plugins/`
2. Jira detects the new plugin automatically (all cluster nodes)
3. Note: File system installs bypass signature verification

---

## Next Steps

After installation, see `admin-guide-X.Y.Z.html` (included in this ZIP) for:
- Global and project configuration
- Setting up approval workflows
- REST API reference for automation and integration
- Troubleshooting

The latest version is also available online at https://cahabaforge.com/docs/admin-guide/

---

## Troubleshooting

- **"Upload app" button not visible** -- See Step 2 above
- **"Untrusted app" error** -- See Step 1 above
- **Plugin not appearing after upload** -- Check Jira logs for errors
- **Need help?** Contact support@cahabaforge.com
