
---

# 🩺 GCP Load Balancer Health Inspector

### *“Stop paying for broken things”*

Hey SRE friend! 🧑‍🚀
Tired of digging through GCP manually to figure out which load balancer backend is failing silently and draining your budget like a vampire in prod?

This Ansible playbook automates that check and posts a **clear, readable summary to Slack**, so your team knows what’s unhealthy — before your CFO does. 💸

---

## 🚀 TL;DR

This playbook:

* Lists all global GCP backend services
* Skips serverless ones (because they’re different beasts)
* Checks each one’s health status
* If it’s not `HEALTHY`, it formats it into a pretty Slack message
* Posts it to your chosen channel
* Saves you from wasting time and **cloud budget**

---

## 💡 Why This Exists (a.k.a. The Problem We’re Solving)

GCP will happily charge you for unhealthy or unused load balancers — even if traffic isn’t flowing.

For teams with growing infra or multiple environments:

* It’s easy to miss broken LBs.
* Alerts don’t always catch idle/broken-but-not-alarming resources.
* Monthly costs creep up, and no one knows why.

This playbook fixes that.

📉 **It’s part observability, part housekeeping, part budget watchdog.**

---

## 🧰 Prerequisites

* Ansible (obviously)
* `gcloud` CLI configured
* GCP Service Account JSON with permission to:

  * List backend services
  * Get backend health
* Slack bot token with `chat:write` permission

---

## ⚙️ Usage

1. Clone the repo
2. Set your secrets (or use Ansible Vault / env vars):

```yaml
gcp_terraform_sa: /path/to/service-account.json
slack_token: xoxb-your-slack-token
```

3. Run the playbook:

```bash
ansible-playbook check-unhealthy-lbs.yml \
  -e "gcp_terraform_sa=/path/to/creds.json slack_token=xoxb-your-token"
```

4. Get Slack’d.

---

## 🧾 Example Slack Output

```
Unhealthy Load Balancers:
-------------------------------------------------------------------------
| Load Balancer | Backend Service | Region        | Status        |
-------------------------------------------------------------------------
| Global LB     | api-backend     | N/A           | UNHEALTHY     |
| Global LB     | internal-check  | N/A           | DRAINING      |
```

Readable. Actionable. Team-friendly.

---

## 💸 Cloud Cost Awareness

> **GCP doesn’t stop charging for unhealthy infra. You should stop running it.**

This playbook helps you:

* Identify idle or broken backend services
* Start conversations around cleanup and optimization
* Shift left on reliability and cost control

✅ **Health check + cost visibility = operational win**

---

## 🔧 Troubleshooting

* If you're not seeing results:

  * Ensure `gcloud` is working with the provided service account
  * Double-check IAM roles (needs compute viewer / read perms)
  * Make sure your Slack token is valid and scoped correctly

---

## 🤝 Contributing

Have a cool enhancement? Want to support regional LBs?
Spotted a formatting issue or edge case? PRs welcome.
We ❤️ clean code and smart automation.

---

## 📜 License

MIT — do whatever you want, just don’t make a SaaS out of it and charge us \$49/mo 😅

---

## 💬 Final Thoughts

You already monitor the important stuff.
But forgotten, unhealthy infra is a quiet cost sink.

This tool is your lightweight check to surface and **take action on dead weight**.

> Because in SRE, **"no alert" doesn’t always mean "no problem."**

---

