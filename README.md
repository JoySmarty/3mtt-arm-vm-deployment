# 3mtt-arm-vm-deployment
My first VM deployment project in Azure


````md
# 🚀 Azure ARM Virtual Machine Deployment Project

## 📌 Project Overview

This project demonstrates the implementation of **Infrastructure as Code (IaC)** using **Azure Resource Manager (ARM) templates** to deploy a fully functional Linux Virtual Machine (VM) on Microsoft Azure.

Instead of manually creating resources through the Azure Portal, this project automates the entire infrastructure provisioning process using declarative JSON templates and Azure CLI commands.

The deployment includes:
- Virtual Network (VNet)
- Subnet
- Network Interface (NIC)
- Network Security Group (NSG)
- Public IP Address
- Ubuntu Linux Virtual Machine

This project reflects real-world DevOps practices used for scalable, repeatable, and automated cloud infrastructure deployment.

---

## 🎯 Project Objectives

- Understand Infrastructure as Code (IaC) using ARM templates
- Deploy Azure resources using declarative JSON templates
- Learn Azure CLI-based deployment workflow
- Configure networking components for secure VM access
- Apply cloud security principles using NSGs and SSH
- Understand resource dependencies in cloud infrastructure
- Handle deployment errors and troubleshoot Azure limitations

---

## 🏗️ Architecture Overview

The deployed architecture consists of:

1. **Resource Group**
   - Logical container for all resources

2. **Virtual Network (VNet)**
   - Provides isolated network environment

3. **Subnet**
   - Segments the virtual network

4. **Network Interface (NIC)**
   - Connects VM to network

5. **Public IP Address**
   - Enables external SSH access

6. **Network Security Group (NSG)**
   - Controls inbound traffic (SSH port 22)

7. **Virtual Machine (Ubuntu Server)**
   - Compute instance running Linux OS

---

## 🌍 Azure Region Selection

**Selected Region:** `South Africa North (southafricanorth)`

### 📌 Reason for Selection:
- Lower latency for local access
- Better availability after testing multiple regions
- Improved success rate for VM deployment compared to US/EU regions tested earlier

---

## ⚙️ ARM Template Structure

The ARM template consists of four main components:

### 1. Parameters
Defines user inputs such as:
- VM name
- Admin username
- Admin password
- Location

### 2. Variables
Stores reusable values such as:
- VNet name
- Subnet name
- NIC name
- Public IP name
- NSG name

### 3. Resources
Defines Azure infrastructure:
- Microsoft.Network/virtualNetworks
- Microsoft.Network/networkInterfaces
- Microsoft.Network/publicIPAddresses
- Microsoft.Network/networkSecurityGroups
- Microsoft.Compute/virtualMachines

### 4. Outputs
Returns deployment results such as:
- Public IP address of the VM

---

## 🚀 Deployment Steps (Azure CLI)

### 1. Create Resource Group
```bash
az group create --name arm-vm-rg --location southafricanorth
````

---

### 2. Validate ARM Template

Ensures JSON syntax and structure are correct before deployment.

```bash
az deployment group validate \
  --resource-group arm-vm-rg \
  --template-file templates/vm-template.json \
  --parameters templates/parameters.json
```

---

### 3. Deploy Infrastructure

```bash
az deployment group create \
  --resource-group arm-vm-rg \
  --template-file templates/vm-template.json \
  --parameters templates/parameters.json
```

---

### 4. Retrieve Public IP Address

```bash
az vm list-ip-addresses \
  --resource-group arm-vm-rg \
  --name devopsVM01 \
  --output table
```

---

### 5. SSH into Virtual Machine

```bash
ssh azureuser@<PUBLIC_IP>
```

---

## 🔐 Security Implementation

This project follows Azure security best practices:

### ✔ Network Security Group (NSG)

* Allows inbound SSH traffic on port 22 only
* Blocks all other unnecessary inbound traffic

### ✔ Identity & Access

* Uses admin username/password authentication
* Encourages secure password policy enforcement

### ✔ Shared Responsibility Model

| Layer                   | Responsibility                         |
| ----------------------- | -------------------------------------- |
| Physical Infrastructure | Microsoft Azure                        |
| Network Security        | Microsoft Azure + User (configuration) |
| Operating System        | User                                   |
| Application Security    | User                                   |
| Access Credentials      | User                                   |

---

## 💰 Cost Management Strategy

To avoid unnecessary charges:

* Azure Free Tier subscription was used
* VM size selected within free-tier-compatible limits
* Resources are deleted after testing using:

```bash
az group delete --name arm-vm-rg --yes --no-wait
```

---

## 🧪 Deployment Challenges & Troubleshooting

### ❌ Issue 1: VM SKU Not Available

* Several VM sizes (B-series, A-series) were unavailable in selected regions
* **Solution:** Switched to `Standard_D2s_v3` and tested multiple regions

---

### ❌ Issue 2: Public IP SKU Restriction

* Basic SKU Public IP was not allowed in subscription
* **Solution:** Upgraded to Standard SKU Public IP

---

### ❌ Issue 3: SSH Connection Timeout

* Caused by NSG misconfiguration or missing rule association
* **Solution:** Verified NSG rule for port 22 and ensured proper attachment

---

### ❌ Issue 4: SSH Authentication Failure

* Caused by incorrect or mismatched credentials
* **Solution:** Reset VM password via Azure CLI / Portal

---

## 📸 Verification Evidence (Included in Repository)

The following screenshots are included:

* Azure Resource Group creation
* Successful ARM deployment
* Virtual Machine running status
* Public IP address assignment
* Cost Management dashboard
* NSG configuration rules
* SSH connection proof

---

## 📊 Outputs Example

After deployment, the system returns:

* Public IP Address
* Resource IDs
* Deployment correlation ID
* VM provisioning status

---

## 🧠 Key Learnings

* Infrastructure as Code enables repeatable cloud deployments
* Azure ARM templates require strict JSON structure
* Cloud regions have capacity limitations affecting deployments
* Networking configuration is critical for VM accessibility
* Troubleshooting is a core DevOps skill

---

## 🏁 Conclusion

This project successfully demonstrates the deployment of a fully functional cloud-based virtual machine using Azure ARM templates and CLI automation.

It highlights real-world DevOps practices including:

* Infrastructure automation
* Cloud networking configuration
* Security implementation
* Cost optimization
* Deployment troubleshooting

---

## 📁 Repository Structure

```
├── templates/
│   ├── vm-template.json
│   ├── parameters.json
├── README.md
├── screenshots/
```

---

## 👤 Author

DevOps Learner Project – Azure ARM Deployment Lab

```
