# 🌐 Azure Translator Automation (GIPROJ1)

This project automates the translation of uploaded `.txt` files using **Azure AI Translator** and securely stores the translated results in **Azure Blob Storage**. It integrates **Azure Functions**, **Terraform**, and a **Flask-based web interface** for end-to-end automation.

---

## 🗂️ Project Structure
<img width="248" height="552" alt="image" src="https://github.com/user-attachments/assets/aa6756ea-bd0c-4346-a907-8dc4eadffbde" />

# 🏗️ Architecture

<img width="700" height="900" alt="image" src="https://github.com/user-attachments/assets/a16a8f7d-7465-4849-970b-3df0de60aea8" />

> This architecture shows how the app uses Azure Blob Storage, Azure Function, and AI Translator.

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
```bash
AZURE_TRANSLATOR_KEY=...
AZURE_TRANSLATOR_ENDPOINT=https://gi-tmp-translator.cognitiveservices.azure.com/
AZURE_STORAGE_ACCOUNT_NAME=newtranslationstorage222
AZURE_STORAGE_CONNECTION_STRING=...
AZURE_REGION=westeurope
```

Make sure .env is listed in .gitignore.

# ⚡ 3. Azure Function (Translation Trigger)

Trigger: When a .txt file is uploaded to input-requests
Action: Translates the file to French using Azure Translator
Output: Saves result in output-results

Blob trigger defined in function.json:
```bash
{
  "bindings": [
    {
      "name": "myblob",
      "type": "blobTrigger",
      "direction": "in",
      "path": "input-requests/{name}",
      "connection": "AzureWebJobsStorage"
    }
  ]
}
```

## Install dependencies:
```bash
pip install -r requirements.txt
```

# 🌐 4. Web Interface (Flask App)

Users can:
- Upload .txt files
- Select output language
- Download translated file

Run locally:
```bash
cd webapp
python app.py
```
Ensure python-dotenv loads the .env file from the root.

# 🧪 5. How It Works (Testing Flow)

1) User uploads .txt via the web interface
2) File saved to input-requests container
3) Azure Function triggers automatically
4) File is translated to French
5) Translated file is saved in output-results
6) User can download translated file from the UI


#🌐 **Live Demo**

## Try the app live here:  
🔗 [Azure Translator Web App](https://ai-text-translate-a5h6ddddaacgecfc.westeurope-01.azurewebsites.net/)

## 📸 Screenshot of the Home Page:  
<img width="1014" height="1127" alt="image" src="https://github.com/user-attachments/assets/7f9adc98-6cda-403e-8e45-318f916ce78d" />


> Users can upload .txt files, select output language, and download the translated results via the web interface.


# 🚀 Deployment Tips

- Function App Name: maryem-translator-functionapp
- Translator Resource: gi-tmp-translator
- Storage Account Region: East US
- Function App Region: West Europe
- Deploy using Azure CLI or the VS Code Azure Extension

# ✅ Best Practices Used

- Sensitive values in .env (excluded from git)
- Organized folder structure
- Automated provisioning with Terraform
- Serverless design using Azure Functions
- Clear separation of frontend/backend logic
- Blob-triggered function (no polling)

# 📌 Future Improvements

- Multi-language translation
- User authentication
- Translation history/logs
- Frontend enhancements

---

## 👩‍💻 Made by Maryem – Thanks for checking it out!


