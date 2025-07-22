# 🌐 Azure Translator Automation (GIPROJ1)

This project automates the translation of uploaded `.txt` files using **Azure AI Translator** and securely stores the translated results in **Azure Blob Storage**. It integrates **Azure Functions**, **Terraform**, and a **Flask-based web interface** for end-to-end automation.

---

## 🗂️ Project Structure
<img width="248" height="552" alt="image" src="https://github.com/user-attachments/assets/aa6756ea-bd0c-4346-a907-8dc4eadffbde" />


---

## ⚙️ 1. Infrastructure (Terraform)

Provisions the following in **East US**:
- **Resource Group:** `RG-TMP-Maryem`
- **Storage Account:** `newtranslationstorage222`
- **Blob Containers:**
  - `input-requests` — for uploaded `.txt` files
  - `output-results` — for translated output files

> 🛠️ Run:
```bash
terraform init
terraform plan
terraform apply -var-file=".tfvars"
```
# 🔐 2. Environment Configuration

Create a .env file in the project root with:

AZURE_TRANSLATOR_KEY=...
AZURE_TRANSLATOR_ENDPOINT=https://gi-tmp-translator.cognitiveservices.azure.com/
AZURE_STORAGE_ACCOUNT_NAME=newtranslationstorage222
AZURE_STORAGE_CONNECTION_STRING=...
AZURE_REGION=westeurope
