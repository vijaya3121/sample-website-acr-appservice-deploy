# Deploy Docker App from ACR to Azure App Service 

## Overview
This project demonstrates how to:
1) Build a docker image on an Azure Ubuntu VM  
2) Push that image to Azure Container Registry (ACR)  
3) Deploy the image from ACR to Azure App Service (Linux)

---   

## Architecture
(Local VM) → (Push image) → ACR → App Service → Public URL

---
## Resources Used
| Component | Value |
|----------|-------|
| VM OS | Ubuntu Linux |
| ACR Name | myacr2040 |
| Repository | sampleweb |
| Tag | v1 |
| App Service | sampleweb-appservice |

---

## Steps Performed

### 1) Build & Tag Docker Image on VM

```bash
docker build -t sampleweb:v1 .
docker tag sampleweb:v1 myacr2040.azurecr.io/sampleweb:v1
docker push myacr2040.azurecr.io/sampleweb:v1
```
---
### 2) Verify Image Present on VM
```
docker images
```
---
### 3) Enable Managed Identity on App Service

Portal → App Service → Identity
System assigned = ON

---
### 4) Assign ACR Pull Role

Portal → ACR → Access Control (IAM)
Add role → AcrPull → Assign to sampleweb-appservice

---
### 5) Configure App Service Container

Portal → App Service → Deployment Center → Container

| Field        | Value                    |
| ------------ | ------------------------ |
| Image Source | Azure Container Registry |
| Registry     | myacr2040                |
| Repository   | sampleweb                |
| Tag          | v1                       |

---

### 6) Browse the App

Collect the Web App URL from Overview:
App server URL: https://sampleweb-appservice.azurewebsites.net/

---
## Result

App Service successfully pulled container from ACR and displayed output in browser.

---
## Screenshots Included

![docker images output from VM]

ACR repositories page

App Service Identity screenshot

IAM showing AcrPull

Deployment center container configuration

Final browser output













