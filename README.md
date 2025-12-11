# Azure CLI Deployment Lab - Microsoft Sentinel

A minimal, hands-on lab demonstrating how to deploy core Microsoft Sentinel components entirely via Azure CLI, validate the deployment, run a simple KQL test, and clean up the environment.

This project shows a CLI-first workflow for cloud security beginners, proving familiarity with Azure Resource Manager, Log Analytics Workspaces, Sentinel onboarding, and KQL.

## 1. Lab Goals
- Create Azure resources using Azure CLI only
- Deploy:
  - Resource Group
  - Log Analytics Workspace
  - Microsoft Sentinel onboarding
- Validate deployment through KQL queries
- Capture logs and screenshots for documentation
- Fully clean up the environment at the end

## 2. Repository Structure

05_azure-cli-deployment-lab/  
│  
├── 00_setup/  
│   ├── environment_info.txt          # Subscription, tenant, CLI version  
│  
├── 01_commands/  
│   ├── step1_login.txt               # az login + subscription check  
│   ├── step2_rg.txt                  # Create Resource Group  
│   ├── step3_law.txt                 # Create Log Analytics Workspace  
│   ├── step4_sentinel.txt            # Add Sentinel extension + onboard workspace  
│   ├── step5_kql_test.txt            # Test query via Azure Portal  
│   ├── step6_cleanup.txt             # az group delete  
│  
├── 02_screenshots/  
│   ├── portal_rg.png                 # Resource Group visible in portal  
│   ├── portal_law.png                # Workspace visible in portal  
│   ├── portal_sentinel.png           # Sentinel enabled  
│   ├── logs_kql_test.png             # KQL query result  
│  
└── README.md  

## 3. Tools Used
- Azure CLI (current version)
- Sentinel CLI Extension (`az extension add --name sentinel`)
- Azure Portal (for visual validation only)
- KQL query editor

## 4. Deployment Steps (CLI)

### Step 1 - Login
az login
az account show

### Step 2 - Create Resource Group
az group create \\  
--name rg-cli-lab \\  
--location westeurope

### Step 3 - Create Log Analytics Workspace
az monitor log-analytics workspace create \\  
--resource-group rg-cli-lab \\  
--workspace-name law-cli-lab

### Step 4 - Enable Microsoft Sentinel
Install extension:  
az extension add --name sentinel

Onboard workspace:  
az sentinel onboarding-state create \\  
--resource-group rg-cli-lab \\  
--workspace-name law-cli-lab \\  
--onboarding-state-name default

Verify a built-in rule exists:  
az sentinel alert-rule list \\  
--resource-group rg-cli-lab \\  
--workspace-name law-cli-lab

## 5. KQL Validation
In Azure Portal -> Logs:  

SecurityEvent  
| limit 10

Screenshot saved as logs_kql_test.png.

## 6. Cleanup (Destroy All Resources)
az group delete \\  
  --name rg-cli-lab \\  
  --yes \\  
  --no-wait

## 7. Why This Lab Matters
This project demonstrates:
- Cloud resource management via CLI, not GUI
- Understanding of Log Analytics + Sentinel onboarding
- Ability to troubleshoot Sentinel extension issues
- Basic KQL familiarity
- Clean and controlled cloud workflow suitable for SOC/Cloud junior roles

The goal is to show hands-on, reproducible cloud security skills — not just theoretical knowledge.

## 8. Author
**Bartosz Cuzytek**  
Cloud-Security / SOC Junior – CLI-first approach
GitHub: https://github.com/cyberweles