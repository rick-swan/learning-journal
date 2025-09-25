# AZ-204 – Explore App Service Web Apps

## 1. Azure App Service – Overview
Azure App Service is a **PaaS offering** for hosting web apps, APIs, and containers.

**Key features:**
- Auto-scaling (scale up = bigger VM, scale out = more instances).
- Multiple runtimes (Windows/Linux).
- Custom containers (single or multi-container with Docker Compose).
- CI/CD integration (GitHub, Azure DevOps, Bitbucket, etc.).
- Deployment slots (staging, production, swap).
- Built-in authentication (Microsoft Entra ID, Google, Facebook, etc.).

👉 CLI to check Linux runtimes:
```bash
az webapp list-runtimes --os-type linux
```

---

## 2. App Service Plans
App Service Plans define the **compute resources** for one or more apps.

**Pricing tiers:**
- **Free/Shared** → Multi-tenant, dev/test only.
- **Basic/Standard/Premium** → Dedicated workers, scale up/out.
- **Isolated (ASE)** → Single-tenant, high security/isolation.

**Scaling:**
- Scaling applies to **all apps** in the plan.
- Create a new plan when:
  - The app is resource-intensive.
  - The app needs independent scaling.
  - The app needs resources in another region.

---

## 3. Deployment Options
**Automated (CI/CD):**
- GitHub Actions, Azure DevOps, Bitbucket.

**Manual:**
- Git push to deployment URL.
- CLI:  
  ```bash
  az webapp up
  ```
- Zip deploy, FTP, cURL.

**Deployment slots:**
- Create staging vs. production slots.
- Swap with zero downtime.

**Containers:**
- Deploy from ACR or Docker Hub.
- Linux supports sidecar containers (e.g., monitoring, logging).

---

## 4. Authentication & Authorization
Azure App Service provides **built-in authentication and authorization** without writing custom code.

**Providers:**
- Microsoft Entra ID, Google, Facebook, Twitter, GitHub, etc.

**Flows:**
- Without provider SDK.
- With provider SDK (e.g., MSAL).

**Authorization behaviors:**
- Allow unauthenticated requests.
- Require login for all requests.

**Token Store:**
- Stores provider tokens.
- Accessible via environment variables or HTTP headers.

**Logging:**
- Auth traces collected in App Service log stream.

---

## 5. Networking
**Default behavior:**
- Apps are internet-accessible by default.

**Models:**
- **Multitenant App Service** → Apps share front ends & workers.
- **App Service Environment (ASE)** → Dedicated, single-tenant isolation.

**Outbound IP addresses:**
- Used for outbound connections (APIs, DBs, 3rd-party services).
- Changing VM family or SKU changes outbound IPs.

👉 CLI examples:
```bash
az webapp show   --resource-group <rg>   --name <app>   --query outboundIpAddresses   --output tsv

az webapp show   --resource-group <rg>   --name <app>   --query possibleOutboundIpAddresses   --output tsv
```

---

## 6. Key Definitions
- **Multitenant**: Multiple customers share infra/resources (isolated data/config).
- **Single-tenant**: Each customer isolated with their own resources.
- **Outbound addresses**: Public IPs App Service uses for outbound traffic.

---

## 7. Extra Reading / Practice
- [App Service Environment v3 vs Multitenant](https://learn.microsoft.com/en-us/azure/app-service/environment/overview)
- [AZ-204 Study Guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/az-204)
- [Microsoft official GitHub labs](https://microsoftlearning.github.io/AZ-204-DevelopingSolutionsforMicrosoftAzure/)

---

✅ **Exam tip:** Expect scenario questions such as:
- *“When should you isolate into a new App Service Plan?”*  
- *“How do you retrieve outbound IPs for firewall rules?”*
