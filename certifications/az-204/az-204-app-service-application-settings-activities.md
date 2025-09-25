# AZ-204 – Application Settings: Practical Activities

This file lists **hands-on activities** you can perform with your **existing projects** (blog project, AZ-204 sample test apps, etc.) to apply App Service Application Settings learnings in practice.

---

## 1. Application Settings Basics
- ✅ Add a new **key-value pair** in App Service application settings for your blog app (e.g., `AppTheme=Dark`).
- ✅ Verify the setting is available inside your app via environment variables.
- ✅ Edit the setting and confirm that the app restarts automatically.

---

## 2. Connection Strings
- ✅ Configure a **Connection String** in App Service (SQL DB or Storage).
- ✅ Override a connection string defined in `appsettings.json` with the App Service version.
- ✅ Test failover by changing the connection string in App Service without redeploying code.

---

## 3. CLI Configuration
- ✅ Use the CLI to add multiple settings at once:
  ```bash
  az webapp config appsettings set     --resource-group <rg>     --name <app-name>     --settings Environment=Prod FeatureXEnabled=true
  ```
- ✅ Verify your container app’s environment variables at:
  ```
  https://<app-name>.scm.azurewebsites.net/Env
  ```

---

## 4. General Settings
- ✅ Enable **HTTPS Only** for your blog app and verify HTTP requests are redirected.
- ✅ Change the **Minimum TLS Version** to 1.2 or 1.3 and attempt a client connection with a lower version.
- ✅ Toggle **ARR Affinity** on/off and observe behavior with multiple instances.

---

## 5. Path Mappings
- ✅ For a Windows-based test app, add a custom handler mapping (e.g., `*.test` → custom script processor).
- ✅ Inspect the default mapping of `/` → `D:\home\site\wwwroot`.
- ✅ For a Linux/container app, check container path handling.

---

## 6. Diagnostic Logging
- ✅ Enable **Application Logging** and add a `TraceError` statement in your .NET blog code:
  ```csharp
  System.Diagnostics.Trace.TraceError("Something went wrong!");
  ```
- ✅ Enable **Web Server Logging** and trigger a few HTTP requests.
- ✅ Compare **File System logging** vs **Blob Storage logging**.

---

## 7. Streaming Logs
- ✅ Enable log streaming and view live logs via CLI:
  ```bash
  az webapp log tail --name <app-name> --resource-group <rg>
  ```
- ✅ Trigger an intentional error and confirm it appears in the live log stream.

---

## 8. Accessing Logs
- ✅ Download the log ZIP file from the Kudu/SCM site:
  - Linux/Container: `https://<app-name>.scm.azurewebsites.net/api/logs/docker/zip`
  - Windows: `https://<app-name>.scm.azurewebsites.net/api/dump`
- ✅ Explore the `/LogFiles` directory structure and identify different log categories.

---

## 9. Stretch Goals
- 🚀 Configure different **App Settings per deployment slot** (staging vs production).
- 🚀 Automate settings updates with a **GitHub Action** workflow.
- 🚀 Centralize sensitive settings using **Azure Key Vault references** in App Service.

---

✅ Completing these activities will reinforce **App Service Application Settings** knowledge with real-world experience.
