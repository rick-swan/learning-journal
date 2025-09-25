# AZ-204 – App Service Web Apps: Practical Activities

This file lists **hands-on activities** you can perform with your **existing projects** (blog project, AZ-204 sample test apps, etc.) to apply App Service learnings in practice.

---

## 1. App Service Basics
- ✅ Deploy your blog app to **Azure App Service** using `az webapp up`.
- ✅ Experiment with both **Linux** and **Windows** runtimes.
- ✅ Check available Linux runtimes via:
  ```bash
  az webapp list-runtimes --os-type linux
  ```

---

## 2. App Service Plans
- ✅ Deploy your blog app into a **Free plan**, then upgrade to **Standard** and test scaling.
- ✅ Create **two different App Service Plans** (Standard and Premium) and deploy sample apps to compare cost/features.
- ✅ Practice **when to isolate an app** into a new plan (e.g., resource-heavy vs. lightweight).

---

## 3. Deployment Methods
- ✅ Set up **GitHub Actions** for your blog project to auto-deploy on push.
- ✅ Try a **manual deployment** using:
  - Git push to deployment URL
  - FTP upload
  - Zip deploy (`az webapp deployment source config-zip`)
- ✅ Deploy your AZ-204 test app using a **staging slot**, then **swap slots** with production.

---

## 4. Containers & Sidecars
- ✅ Containerize your blog app and push it to **Azure Container Registry (ACR)**.
- ✅ Deploy the container from ACR to App Service.
- ✅ Add a **sidecar container** (e.g., monitoring/logging service) alongside your app.

---

## 5. Authentication & Authorization
- ✅ Enable **Microsoft Entra ID authentication** on your blog project.
- ✅ Configure **unauthenticated requests allowed** vs **login required** modes.
- ✅ Inspect tokens in the **App Service token store** using environment variables.
- ✅ Add logging and check how **auth traces** appear in logs.

---

## 6. Networking
- ✅ Retrieve **outbound IP addresses** of your blog app and whitelist them in a test API or DB firewall:
  ```bash
  az webapp show --resource-group <rg> --name <app> --query outboundIpAddresses --output tsv
  ```
- ✅ Compare **multitenant vs. isolated (ASE)** by reading documentation and designing when each fits your projects.
- ✅ Restrict inbound traffic to your blog app using **Access Restrictions (IP rules)**.

---

## 7. Integration Scenarios
- ✅ Connect your blog app to an external **Azure SQL DB** and test firewall rules.
- ✅ Use **Key Vault references** in your app’s settings (e.g., store DB connection string).
- ✅ Enable **Application Insights** to trace and log app requests.

---

## 8. Stretch Goals
- 🚀 Deploy your **AZ-204 sample app** into multiple slots (dev, staging, prod) and practice swapping.
- 🚀 Scale your blog app using **autoscaling rules** (CPU/memory thresholds).
- 🚀 Experiment with **zero-downtime deployments** using deployment slots + GitHub Actions.

---

✅ By completing these activities, you’ll bridge the gap between **exam theory** and **real-world implementation**.
