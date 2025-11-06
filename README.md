# 🐳 GripoFlow (Docker Compose Deployment)

A minimal, production-minded Docker Compose setup for **GripoFlow** — your all-in-one workflow automation platform. This guide focuses on fast install, simple commands, and secure defaults.

---

## ✅ Prerequisites

* **Docker** 24+
* **Docker Compose** v2+
* CPU & RAM: 2 vCPU / 4 GB RAM (minimum)

---

## 🚀 Quick Start

### 1) Clone & enter

```bash
git clone https://github.com/gripoio/gripoflow-docker-deployment.git
cd gripoflow-docker-deployment
cd temporal/ 
sudo docker compose up -d
cd ..
# Wait for all temporal services to run properly
sudo docker compose up -d
```

### 2) Bring it up (detached)

```bash
docker compose up -d
```

### 3) Open the app

```
http://localhost:5055
```

---

## 🧾 Post-Install Notes

After successful deployment, Docker Compose displays running containers:

```bash
Thank you for installing GripoFlow!

Service Name: gripoflow
Network: gf
Access via:
http://127.0.0.1:5055
```

---

## 🔗 Connect External Apps (Plugins)

GripoFlow supports **plugin-based integration** with external applications using **JSON Manifests**. Each plugin defines its tools, APIs, and activities that can be triggered within workflows.

### Example Integrations

* **Slack:** Send automated notifications.
* **GitHub / GitLab / Jenkins:** Trigger CI/CD pipelines or deployment workflows.
* **Azure / AWS / GCP:** Manage Kubernetes clusters, servers, or storage.
* **Notion / Airtable / ClickUp:** Automate data syncing and task creation.
* **WhatsApp:** Send real-time alerts or workflow notifications.
* **PostgreSQL / MySQL:** Run database queries dynamically.
* **HubSpot / Salesforce:** Automate lead follow-ups or CRM updates.

Plugins are managed via JSON manifests and can be mounted in your container for runtime access.

---

## 🧩 Expression System

GripoFlow provides a powerful **expression syntax** to dynamically access and pass data between triggers, inputs, activities, and connections securely.

### 🔐 Secure Connection Access

Safely access credentials without exposing them in logs:

```handlebars
{{flow.connection.gripoAzure.token}}
{{flow.connection.github.access_token}}
{{flow.connection.slack.webhook_url}}
```

> 🔒 Connections are encrypted and evaluated securely at runtime.

### ⚡ Trigger Payloads

Four trigger types are supported: **onDemand**, **schedule**, **webhook**, and **whatsapp**.

Webhook and WhatsApp triggers can pass payload data:

```handlebars
{{flow.trigger.payload.user.email}}
{{flow.trigger.payload.event.type}}
{{flow.trigger.payload.message.text}}
```

> Example: A WhatsApp message like “start cluster” can trigger an Azure cluster startup.

### 🧠 Workflow-Level Inputs

Use custom inputs defined in the workflow:

```handlebars
{{input.Cluster}}
{{input.customerId}}
{{input.region}}
```

> Inputs are reusable across multiple activities.

### 🔄 Activity Outputs

Access results from previous activities:

```handlebars
{{activity.FetchUser.output.data.name}}
{{activity.CalculateCost.output.total}}
{{activity.SendEmail.output.status}}
```

> Example: Use data from `FetchUser` to personalize a message in `SendEmail`.

### 🧮 Expression Combinations

Combine multiple expressions for advanced automation:

```handlebars
{{activity.FetchUser.output.data.firstName}} {{activity.FetchUser.output.data.lastName}}
{{flow.trigger.payload.amount}} USD paid by {{activity.GetCustomer.output.name}}
{{flow.connection.azure.client_id}}::{{flow.connection.azure.tenant}}
```

> Expressions can be nested and evaluated inline.

---

## 🧰 Everyday Commands

Start (foreground):

```bash
docker compose up
```

Start (detached):

```bash
docker compose up -d
```

Stop (keep data):

```bash
docker compose down
```

Stop & remove volumes (fresh reset):

```bash
docker compose down -v
```

Recreate after config change:

```bash
docker compose up -d --build
```

Check logs:

```bash
docker compose logs -f
```

Check status:

```bash
docker compose ps
```

---

## 🧪 Health & Troubleshooting

Check container health:

```bash
docker compose ps
```

Tail one service:

```bash
docker compose logs -f gripoflow
```

Common fixes:

* Port already in use → change mapping in `docker-compose.yml`.
* Fresh database → `docker compose down -v && docker compose up -d`.

---

## 📘 Docs

Full documentation and advanced integration guides:
👉 [http://docs.gripoflow.gripo.io/](http://docs.gripoflow.gripo.io/)




