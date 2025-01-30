

# AccuKnox DAST Scan GitHub Action

## Learn More

- [About Accuknox](https://www.accuknox.com/)

**Description**  

This GitHub Action performs a Dynamic Application Security Testing (DAST) scan using [ZAP](https://www.zaproxy.org] and uploads the scan results to the AccuKnox CSPM panel. This action can be configured with specific inputs to integrate seamlessly into your DevSecOps pipeline.

## Inputs

| Input               | Description                                                                                                  | Required  | Default       |
|---------------------|--------------------------------------------------------------------------------------------------------------|-----------|---------------|
| `target_url`        | The URL of the web application to scan.                                                                      | Yes       |               |
| `accuknox_token`    | Token for authenticating with the AccuKnox CSPM panel.                                                       | Yes       |               |
| `accuknox_endpoint` | The URL of the AccuKnox CSPM panel where scan results will be uploaded.                                      | Yes       |               |
| `tenant_id`         | The ID of the tenant associated with the AccuKnox CSPM dashboard.                                            | Yes       |               |
| `label`             | Label created in AccuKnox SaaS to associate the scan results.                                                | Yes       |               |
| `severity_threshold`| Minimum severity level (e.g., High, Medium, Low, Informational) that will cause the pipeline to fail.       | Yes       |               |
| `scan_type`         | Type of ZAP scan to run: `baseline` or `full-scan`.                                                          | Yes       | `full-scan`   |

## Usage

### Steps for Using the AccuKnox DAST Scan Action in a Workflow

1. **Checkout the Repo**  
   Use the `actions/checkout` action to ensure the codebase is available for scanning.

2. **Add AccuKnox DAST Scan Action**  
   Reference the `accuknox/dast-scan-action` repository with the desired version tag, e.g., `v1.0.0`.

3. **Token Generation from AccuKnox SaaS and Viewing Tenant ID**  
   To obtain the `accuknox_token` and `tenant_id` values needed to authenticate with AccuKnox:
   
   - **Navigate to Tokens**  
     Go to the **Settings** section in the AccuKnox SaaS sidebar.

     ![1](https://github.com/udit-uniyal/container-scan-action/assets/115368361/8f4e188b-d9f3-4404-83af-134d5dc1417a)
   
   - **Create Token**  
     In the "Tokens" section, click on **Create Token**. This action will display your `tenant_id` and allow you to generate an access token.

     ![2](https://github.com/udit-uniyal/container-scan-action/assets/115368361/296bc611-acb8-4918-9d6b-3a8ec7733377)
   
   - **Generate the Token**  
     After clicking **Generate**, copy the `accuknox_token` to use in the workflow.

   ![3](https://github.com/udit-uniyal/container-scan-action/assets/115368361/16032af0-bcac-4787-8f2a-a3fa0edc6ec6)

### Example Workflow File

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

### Secrets Setup

Add the following secrets in your GitHub repository under **Settings > Secrets**:

- `ACCUKNOX_ENDPOINT`: Your AccuKnox CSPM endpoint.
- `TENANT_ID`: Your AccuKnox tenant ID.
- `ACCUKNOX_TOKEN`: Your AccuKnox API token.

## How It Works

1. **ZAP DAST Scan**: The action initiates a DAST scan on the specified `target_url` using ZAP.
2. **AccuKnox Report Generation**: Generates a report in JSON format.
3. **Report Upload**: The report is uploaded to the AccuKnox CSPM panel for centralized monitoring and insights.
4. **Severity Check**: The action checks for vulnerabilities that meet or exceed the specified `severity_threshold`. If any are found, the workflow fails.

## Notes

- Ensure secrets are configured correctly in your GitHub repository.
- The AccuKnox panel provides a centralized view of all DAST results.

For more information, visit the [AccuKnox website](https://www.accuknox.com/).
