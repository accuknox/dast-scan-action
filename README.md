

# AccuKnox DAST

🔍 Automate Dynamic Application Security Testing (DAST) in Your CI/CD Pipeline

The **AccuKnox DAST GitHub Action** enables automated **Dynamic Application Security Testing** for web applications. It scans your application and uploads the findings to the **AccuKnox Console** for centralized monitoring and actionable security insights.

---

## 🎯 Key Features

✅ Dynamic Web Application Security Testing – Detects real-time vulnerabilities
✅ Seamless CI/CD Integration – Easily integrates into GitHub workflows
✅ Real-Time Visibility – Uploads scan results to the AccuKnox Console
✅ Severity Threshold Enforcement – Blocks deployments based on criticality
✅ Customizable Scan Options – Choose between `baseline` and `full-scan` modes

---

## ⚠️ Prerequisites

Before using this GitHub Action, ensure the following:

1️⃣ **AccuKnox Account** – Required to access the AccuKnox Console
2️⃣ **Running Web Application URL** – Required for performing the scan
3️⃣ **GitHub Repository with Actions Enabled** – To run workflows
4️⃣ **AccuKnox API Token & Tenant ID** – For authentication (see below)

---

## 📌 Installation & Usage

### Step 1: Retrieve AccuKnox API Credentials

To authenticate with the AccuKnox Console:

1️⃣ Navigate to **Settings → Tokens** in the AccuKnox Console
2️⃣ Click **Create Token** to generate your `accuknox_token` and view `tenant_id`
3️⃣ Securely store these credentials for GitHub Secrets

---

### Step 2: Implement the Workflow YAML

Create a workflow file `.github/workflows/accuknox-dast.yml` and add the following:

```yaml
name: AccuKnox DAST Scan Workflow
on:
  push:
    branches:
      - main

jobs:
  dast-scan:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Run AccuKnox DAST Scan
        uses: accuknox/dast-scan-action@v1.0.0
        with:
          target_url: "http://testphp.vulnweb.com"
          accuknox_endpoint: ${{ secrets.ACCUKNOX_ENDPOINT }}
          tenant_id: ${{ secrets.TENANT_ID }}
          accuknox_token: ${{ secrets.ACCUKNOX_TOKEN }}
          label: "my-dast-scan"
          severity_threshold: "High"
          scan_type: "baseline"
```

---

## ⚙️ Configuration Options (Inputs)

| Input                | Description                                                                  | Required | Default     |
| -------------------- | ---------------------------------------------------------------------------- | -------- | ----------- |
| `target_url`         | The web application URL to scan                                              | ✅ Yes    | —           |
| `accuknox_token`     | Token to authenticate with the AccuKnox Console                              | ✅ Yes    | —           |
| `accuknox_endpoint`  | URL of the AccuKnox Console to upload results                                | ✅ Yes    | —           |
| `tenant_id`          | Tenant ID associated with your AccuKnox account                              | ✅ Yes    | —           |
| `label`              | Label to tag the scan results in the AccuKnox Console                        | ✅ Yes    | —           |
| `severity_threshold` | Severity level (e.g., High, Medium, Low, Informational) to fail the pipeline | ✅ Yes    | —           |
| `scan_type`          | Type of scan to perform (`baseline` or `full-scan`)                          | ✅ Yes    | `full-scan` |

---

## 🔐 Secrets Setup

Go to **Settings > Secrets and variables > Actions** in your GitHub repository and add:

* `ACCUKNOX_ENDPOINT` → Your AccuKnox Console endpoint
* `TENANT_ID` → Your AccuKnox tenant ID
* `ACCUKNOX_TOKEN` → API token generated in the AccuKnox Console

---

## 🔍 How It Works

1️⃣ **Scan Execution** – The action triggers a DAST scan on the specified `target_url`
2️⃣ **Report Generation** – A vulnerability report is generated in JSON format
3️⃣ **Upload to AccuKnox Console** – The report is uploaded for centralized analysis
4️⃣ **Severity Check** – The pipeline fails if any issues meet or exceed the configured `severity_threshold`

---

## 🛠️ Troubleshooting & Best Practices

❌ **Pipeline Failed Due to Vulnerabilities?**
→ Adjust the `severity_threshold` or resolve critical issues before merge

🔐 **Invalid Token Errors?**
→ Recheck and update your GitHub secrets, or regenerate from the Console

💡 **Best Practices**
→ Run scans on production-like environments for accurate results
→ Tag scans meaningfully using the `label` input

---

## 📖 Support & Documentation

📚 Read More: [AccuKnox Documentation](https://help.accuknox.com)
📧 Contact: [support@accuknox.com](mailto:support@accuknox.com)

---

## 🏆 Conclusion

The **AccuKnox DAST GitHub Action** helps you shift security left by automating real-time vulnerability detection and enforcement—directly in your CI/CD pipelines.

🔹 **Secure Your Web Applications with AccuKnox DAST – Start Today!** 🔒


