# Deploy n8n on a CubePath VPS

Deploy self-hosted n8n through the CubePath Marketplace and create your first workflow.

This quickstart covers app deployment, finding your access details and running a simple workflow without external accounts or API keys.

## Prerequisites

- A verified CubePath account.
- Enough account balance to cover your VPS.
- A plan that meets the application's minimum RAM requirement.

A custom domain is optional for the initial deployment.

## 1. Deploy n8n

1. Sign in to the [CubePath dashboard](https://my.cubepath.com).
2. Open **Deploy App**.
3. Find and select **n8n**.
4. Review any application settings or environment variables shown in the form. Auto-generated values are created for you.
5. Review the preselected region and recommended plan. Adjust them to suit your location and workload, while meeting the application's minimum requirements.
6. Review the root password and deployment cost.
7. Click **Deploy**.

CubePath installs and configures the packaged application on a new Virtual Machine. You do not need to perform a separate manual installation of n8n.

See the [n8n Marketplace page](https://cubepath.com/marketplace/n8n) for application information.

## 2. Find your access details

After deployment, CubePath displays a window with the application's access URL and any credentials or secret keys provided for that deployment.

**Save any auto-generated passwords and secrets in a password manager before closing this window.** They are shown only once, and some can only be reset from inside the application.

Once the VPS is active, you can also find the application's access URL on the VPS details page.

Open that URL and follow the initial sign-in or account setup instructions shown by n8n.

Treat access links containing tokens as secrets. Do not share them or commit them to GitHub.

## 3. Check HTTPS and your domain

Before entering production credentials or connecting external services, check that your n8n address uses HTTPS with a valid certificate.

For a custom domain, create a DNS **A record** pointing your chosen hostname to the VPS's public IPv4 address. For example, use a subdomain such as `n8n.example.com`.

A DNS record alone does not configure the application's public URL or issue an HTTPS certificate.

The CubePath sources linked below do not specify the n8n Marketplace app's exact custom-domain and HTTPS procedure. Follow any instructions supplied with your deployment, or contact CubePath support through the dashboard before changing its configuration.

CubePath also publishes a separate manual installation tutorial using Docker Compose, Nginx and Let's Encrypt. That tutorial describes its own setup; do not assume its files or commands match an existing Marketplace deployment.

## 4. Run your first workflow

This example creates a message inside n8n. It does not contact external services or require credentials.

1. Create a new workflow.
2. Add a **Manual Trigger** node.
3. Connect an **Edit Fields (Set)** node to it.
4. In Edit Fields, select **Manual Mapping**.
5. Add a field named `message` with type **String**.
6. Set its value to the fixed text `Hello from n8n on CubePath!`.
7. Execute the workflow.
8. Open the Edit Fields node's output.

The output should contain:

    {
      "message": "Hello from n8n on CubePath!"
    }

Save the workflow as `CubePath - First Workflow`.

The Manual Trigger runs only when you execute the workflow yourself. For automatic execution, use an appropriate trigger, such as a schedule or webhook, and complete the activation or publishing step required by your n8n version.

## 5. Build useful automations

After the first test, you can add integrations for tasks such as:

- Receiving form submissions and creating CRM contacts.
- Sending team notifications.
- Synchronizing records between applications.
- Calling APIs.
- Connecting workflows to AI services.

Configure service credentials inside n8n. Never commit passwords, API keys, access tokens or exported credentials to this repository.

External services may charge separately and receive the data your workflow sends to them. Self-hosting n8n does not keep data on the VPS when a workflow sends it to another service.

## Backups and updates

Plan for application maintenance as part of self-hosting.

- Back up the database and any persistent files needed by your workflows.
- Preserve the original encryption key used by n8n to protect stored credentials.
- Keep a protected backup copy outside the VPS.
- Test that you can restore your instance.
- Read release notes and create a backup before updating.
- Test important workflows and service connections after an update.

CubePath provides an [n8n update guide for Docker Compose](https://cubepath.com/docs/apps/how-to-update-n8n-to-latest-version).

That guide assumes a particular installation directory, database and service names. Check them against your deployment before running its commands.

The Marketplace deployment process does not, by itself, confirm that automatic application updates or backups are enabled.

## Troubleshooting

### I cannot find the access URL

Wait for the VPS to become active, then open its details page. CubePath documents that the application access URL appears there.

### I closed the credentials window

Auto-generated secrets are displayed only once. Depending on the application, you may need to reset them inside the app. Contact CubePath support if you cannot access the instance.

### My custom domain does not work

Check that its DNS A record points to the correct VPS IPv4 address. Then check the application's public URL, reverse proxy, certificate and firewall configuration.

### My workflow does not run automatically

The example in this guide uses a Manual Trigger. Automatic execution requires a suitable trigger and the activation or publishing step required by your n8n version.

### Credentials cannot be decrypted after a restore

Check that you restored the original encryption key along with the database. A replacement key cannot decrypt credentials saved with the previous one.

## Sources and further reading

### CubePath

- [Deploy an App: deployment and access details](https://cubepath.com/docs/products/deployment/deploy-an-app)
- [n8n Marketplace page](https://cubepath.com/marketplace/n8n)
- [Manual installation with Docker Compose and HTTPS](https://cubepath.com/docs/web-applications-hosting/n8n-workflow-automation-installation)
- [Updating n8n with Docker Compose](https://cubepath.com/docs/apps/how-to-update-n8n-to-latest-version)

### n8n

- [Official documentation](https://docs.n8n.io/)
- [Manual Trigger](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.manualworkflowtrigger/)
- [Edit Fields (Set)](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.set/)
- [Encryption key configuration](https://docs.n8n.io/hosting/configuration/configuration-examples/encryption-key/)

---

Maintained by the CubePath team.
