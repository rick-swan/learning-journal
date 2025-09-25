# AZ-204 – Configure Application Settings in App Service

## 1. Application Settings Overview
- App Service **app settings** are passed as **environment variables** to the app code.
- On Linux apps & containers → passed with `--env` flag.
- Settings are **injected at startup** → restart required when adding, removing, or editing settings.
- App settings in Azure are **encrypted at rest**.
- They map to:
  - `<appSettings>` in **web.config**
  - `appsettings.json` in **.NET** apps

👉 Keep local dev settings in config files, production settings in Azure App Service.

---

## 2. Connection Strings
- Connection strings in App Service **override** values in `appsettings.json` or `web.config`.

---

## 3. Configure App Settings
**CLI example:**
```bash
az webapp config appsettings set   --resource-group <group-name>   --name <app-name>   --settings key1=value1 key2=value2
```

- Verify container environment variables:
  ```
  https://<app-name>.scm.azurewebsites.net/Env
  ```

---

## 4. General Settings
**Notable options:**
- **ARR Affinity** → ensures client requests in multi-instance apps route to the same instance.
- **HTTPS Only** → forces HTTP → HTTPS redirection.
- **Minimum TLS Version** → sets TLS version (security level) required.

---

## 5. Path Mappings
- For **Windows (non-containerized) apps**:
  - Can configure **handler mappings** → custom script processors for file extensions.
  - Example: add handler mapping for `*.php`.
  - Root path `/` maps to `D:\home\site\wwwroot`.

- For **Linux & containerized apps**:
  - Path mappings handled differently (through container config).

---

## 6. Diagnostic Logging
Types of logging available:
- **Application logging**
- **Web server logging**
- **Detailed error messages**
- **Failed request tracing**
- **Deployment logs**

**Log destinations:**
- **File system** → temporary (short-term retention).
- **Azure Blob Storage** → long-term retention.

**In-code logging (C# example):**
```csharp
System.Diagnostics.Trace.TraceError("If you're seeing this, something bad happened");
```

---

## 7. Streaming Logs
Enable log types first, then stream in real time:

```bash
az webapp log tail   --name <app-name>   --resource-group <rg>
```

- Log files stored under `/LogFiles` directory:
  - `/LogFiles/application/`
  - `/LogFiles/http/`
- Stream includes `.txt`, `.log`, `.htm` files.

---

## 8. Accessing Logs
- **Blob storage logs** → need a storage client.
- **File system logs** → download ZIP file:

Linux / Container apps:
```
https://<app-name>.scm.azurewebsites.net/api/logs/docker/zip
```

Windows apps:
```
https://<app-name>.scm.azurewebsites.net/api/dump
```

---

## 9. Key Definition
- **TLS (Transport Layer Security)**: Cryptographic protocol for secure communication over a computer network.

---

✅ **Exam tip:** Expect questions like:
- *“How do you override connection strings for production?”*  
- *“Where are app settings injected and when are they applied?”*  
- *“What’s the difference between ARR Affinity and HTTPS Only?”*  
