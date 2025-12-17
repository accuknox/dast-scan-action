

# AccuKnox DAST

🔍 Automate Dynamic Application Security Testing (DAST) in Your CI/CD Pipeline

The **AccuKnox DAST GitHub Action** enables automated **Dynamic Application Security Testing** for web applications. It scans your application and uploads the findings to the **AccuKnox Console** for centralized monitoring and actionable security insights.

---

## 🎯 Key Features

- Dynamic Web Application Security Testing – Detects real-time vulnerabilities
- Seamless CI/CD Integration – Easily integrates into GitHub workflows
- Real-Time Visibility – Uploads scan results to the AccuKnox Console
- Severity Threshold Enforcement – Blocks deployments based on criticality
- Customizable Scan Options – Choose between `baseline` and `full-scan` modes

---

## ⚠️ Prerequisites

Before using this GitHub Action, ensure the following:

- **AccuKnox Account** – Required to access the AccuKnox Console
- **Running Web Application URL** – Required for performing the scan
- **GitHub Repository with Actions Enabled** – To run workflows
- **AccuKnox API Token & Tenant ID** – For authentication (see below)

---

## 📌 Installation & Usage

### Step 1: Retrieve AccuKnox API Credentials

To authenticate with the AccuKnox Console:

- Navigate to **Settings → Tokens** in the AccuKnox Console
- Click **Create Token** to generate your `accuknox_token` 
- Securely store these credentials for GitHub Secrets

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
        uses: accuknox/dast-scan-action@latest
        with:
          target_url: "http://testphp.vulnweb.com"
          accuknox_endpoint: ${{ secrets.ACCUKNOX_ENDPOINT }}
          accuknox_token: ${{ secrets.ACCUKNOX_TOKEN }}
          accuknox_label: ${{ secrets.ACCUKNOX_LABEL }}
          severity_threshold: "HIGH"
          dast_scan_type: "full-scan"
```

---

## ⚙️ Configuration Options (Inputs)

| Input                | Description                                                                  | Required | Default     |
| -------------------- | ---------------------------------------------------------------------------- | -------- | ----------- |
| `target_url`         | The web application URL to scan                                              | ✅ Yes    | —           |
| `accuknox_token`     | Token to authenticate with the AccuKnox Console                              | ✅ Yes    | —           |
| `accuknox_endpoint`  | URL of the AccuKnox Console to upload results                                | ✅ Yes    | —           |
| `accuknox_label`     | Label to tag the scan results in the AccuKnox Console                        | ✅ Yes    | —           |
| `severity_threshold` | Severity level (e.g., High, Medium, Low, Informational) to fail the pipeline | ✅ Yes    | —           |
| `scan_type`          | Type of scan to perform (`baseline` or `full-scan`)                          | ❌ No    | `baseline` |

---

## 🔐 Secrets Setup

Go to **Settings > Secrets and variables > Actions** in your GitHub repository and add:

* `ACCUKNOX_ENDPOINT` → Your AccuKnox Console endpoint  
* `ACCUKNOX_TOKEN` → API token generated in the AccuKnox Console  
* `ACCUKNOX_LABEL` → Label to tag and identify your scan results in AccuKnox Console  

---

## 🔍 How It Works

- **Scan Execution** – The action triggers a DAST scan on the specified `target_url`
- **Report Generation** – A vulnerability report is generated in JSON format
- **Upload to AccuKnox Console** – The report is uploaded for centralized analysis
- **Severity Check** – The pipeline fails if any issues meet or exceed the configured `severity_threshold`

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


