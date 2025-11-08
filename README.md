# 🐳 GripoFlow (Docker Compose Deployment)

**GripoFlow** is a Kubernetes-native workflow automation platform that lets you connect external apps, build intelligent workflows, and automate anything — from DevOps pipelines to business operations — in just a few steps.

---

## ✅ Prerequisites

* **Docker:** 24+
* **Docker Compose:** v2+
* **System Requirements:** 2 vCPU · 4 GB RAM (minimum)

---

## 🚀 Quick Start

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/gripoio/gripoflow-docker-deployment.git
cd gripoflow-docker-deployment
```

### 2️⃣ Start Temporal Services

```bash
cd temporal/
sudo docker compose up -d
```

### 3️⃣ Start GripoFlow

```bash
cd ..
sudo docker compose up -d
```

### 4️⃣ Access the App

```
http://localhost:7055
```

---

## 🧾 Post-Install Notes

After a successful launch, Docker Compose will display active containers:

```bash
Thank you for installing GripoFlow!

Service Name: gripoflow
Network: gf
Access via: http://127.0.0.1:5055
```

---

## 🔗 Connect External Apps (Plugins)

GripoFlow supports **plugin-based integration** via **JSON Manifests**.
Each plugin defines APIs, tools, and activities that can be executed inside workflows.

### 🌍 Example Integrations

* **Slack:** Send instant alerts or updates.
* **GitHub / GitLab / Jenkins:** Trigger CI/CD pipelines automatically.
* **Azure / AWS / GCP:** Start or stop Kubernetes clusters and cloud resources.
* **Notion / Airtable / ClickUp:** Sync data and automate tasks.
* **WhatsApp:** Trigger workflows from messages.
* **PostgreSQL / MySQL:** Execute dynamic queries.
* **HubSpot / Salesforce:** Automate CRM lead updates.

> 💡 Manage your plugins by mounting their JSON manifests into the container (e.g., `./plugins:/app/plugins:ro`).

---

## 🧩 Expression System

GripoFlow includes a powerful **expression syntax** to securely reference inputs, triggers, activities, and connections.

### 🔐 Secure Connection Access

Use credentials without exposing them in logs:

```handlebars
{{flow.connection.github.access_token}}
{{flow.connection.slack.webhook_url}}
{{flow.connection.gripoAzure.token}}
```

> 🔒 All credentials are encrypted and evaluated securely at runtime.

### ⚡ Triggers

Supported trigger types:

* `onDemand`
* `schedule`
* `webhook`
* `whatsapp`

Webhook and WhatsApp triggers allow you to use incoming payloads:

```handlebars
{{flow.trigger.payload.user.email}}
{{flow.trigger.payload.event.type}}
{{flow.trigger.payload.message.text}}
```

> Example: A WhatsApp message like “start cluster” can power up an Azure environment.

### 🧠 Workflow Inputs

Access workflow-level variables:

```handlebars
{{input.Cluster}}
{{input.customerId}}
{{input.region}}
```

### 🔄 Activity Outputs

Use data from previous activities:

```handlebars
{{activity.FetchUser.output.data.name}}
{{activity.CalculateCost.output.total}}
{{activity.SendEmail.output.status}}
```

### 🧮 Combine Expressions

Build complex logic dynamically:

```handlebars
{{activity.FetchUser.output.data.firstName}} {{activity.FetchUser.output.data.lastName}}
{{flow.trigger.payload.amount}} USD paid by {{activity.GetCustomer.output.name}}
{{flow.connection.azure.client_id}}::{{flow.connection.azure.tenant}}
```

---

## 🧰 Common Commands

| Action                   | Command                        |
| ------------------------ | ------------------------------ |
| Start (foreground)       | `docker compose up`            |
| Start (detached)         | `docker compose up -d`         |
| Stop (keep data)         | `docker compose down`          |
| Stop & remove volumes    | `docker compose down -v`       |
| Rebuild after changes    | `docker compose up -d --build` |
| View logs                | `docker compose logs -f`       |
| Check running containers | `docker compose ps`            |

---

## 🧪 Health & Troubleshooting

Check container health:

```bash
docker compose ps
```

View logs for GripoFlow:

```bash
docker compose logs -f gripoflow
```

### Common Fixes

* **Port conflict:** Change exposed port in `docker-compose.yml`.
* **Clean start:**

  ```bash
  docker compose down -v && docker compose up -d
  ```

---

## 📘 Documentation

Full documentation and advanced guides:
👉 [http://docs.gripoflow.gripo.io/](http://docs.gripoflow.gripo.io/)



