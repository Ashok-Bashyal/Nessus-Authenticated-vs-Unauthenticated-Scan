# Nessus Authenticated vs. Unauthenticated Scan

This project demonstrates how to perform an **Unauthenticated Vulnerability Scan** using **Tenable Nessus** against an Azure Virtual Machine. It also explains how to review vulnerability findings and remediation recommendations.

---

## Lab Environment

| Component | Value |
|-----------|-------|
| Vulnerability Scanner | Tenable Nessus |
| Cloud Provider | Microsoft Azure |
| Target | Windows Virtual Machine |
| Scan Type | Basic Network Scan (Unauthenticated) and (Authenticated)|

---

# Unauthenticated Vulnerability Scan

## Step 1 - Create a Virtual Machine

Create a virtual machine using your preferred cloud provider or hypervisor.

> **Note:** This guide uses **Microsoft Azure**.

For detailed VM deployment instructions, refer to my Azure VM guide:

**Azure VM Project**

https://github.com/Ashok-Bashyal/Azure-VM

Configure the Network Security Group (NSG) to allow communication between the Nessus Scanner and the target virtual machine.

<img width="1309" height="213" alt="Azure NSG Rule" src="https://github.com/user-attachments/assets/e6f60711-0833-4ff4-bfbe-9bd169268534" />

---

## Step 2 - Create a New Nessus Scan

1. Sign in to your Tenable Nessus account.
2. Open the **Scans** page.
3. Click **Create Scan**.
4. Select **Basic Network Scan**.
5. Give the scan a descriptive name.
6. (Optional) Add a description.
7. Choose your Nessus Scanner.

---

## Step 3 - Configure the Target

Return to your Azure Virtual Machine.

Copy the **Private IP Address** and paste it into the **Targets** field of the Nessus scan configuration.

<img width="778" height="259" alt="Target Configuration" src="https://github.com/user-attachments/assets/42a7325f-a35e-4e7b-85db-55f6dc002c88" />

<img width="1255" height="751" alt="Target IP" src="https://github.com/user-attachments/assets/b1eef114-16b8-48ee-b725-a68e1dfde4a5" />

---

## Step 4 - Configure Discovery Settings

Navigate to the **Discovery** section.

Modify the following settings:

- Discovery Type: **Custom**
- Enable **Ping the remote host**
- Enable **Fast Network Discovery**

<img width="717" height="458" alt="Discovery Settings" src="https://github.com/user-attachments/assets/74a53d40-92bd-4077-8f41-59d8ab81c7a2" />

---

## Step 5 - Launch the Scan

For a standard unauthenticated scan, the default configuration is sufficient.

Click:

**Save → Launch**

> **Note:** Scan duration varies depending on the target and network size. The scan may take up to one hour.

---

## Step 6 - Review Scan Results

After the scan finishes:

1. Open the completed scan.
2. Click **See All Details**.

<img width="1813" height="596" alt="Scan Results" src="https://github.com/user-attachments/assets/c7c85359-0fee-4b87-8d15-7c1421d32319" />

The results include:

- Vulnerability Name
- Severity Level
- CVSS Score
- Risk Factor
- Affected Services
- Plugin ID
- Plugin Output

Severity levels include:

- Critical
- High
- Medium
- Low
- Informational

---

## Step 7 - Review Vulnerability Details

Selecting any vulnerability provides detailed technical information including:

- Description
- Synopsis
- CVSS Score
- Risk Information
- Plugin Output
- References
- Solution (Remediation)

To view the complete remediation guidance, open the associated **Plugin ID**.

<img width="1523" height="681" alt="Plugin Details" src="https://github.com/user-attachments/assets/03f4ce88-df9d-49a8-9854-4987e39a54bc" />

Example:

### SSL Certificate Cannot Be Trusted

<img width="1195" height="885" alt="SSL Certificate Cannot Be Trusted" src="https://github.com/user-attachments/assets/2fdd9873-208e-4129-a002-4df6155534bd" />

---

# What an Unauthenticated Scan Can Detect

An unauthenticated scan examines a system from an external perspective without logging into the operating system.

Typical findings include:

- Open Ports
- Running Services
- SSL/TLS Issues
- Missing Security Headers
- Outdated Software
- Weak Encryption
- Publicly Exposed Vulnerabilities
- Misconfigurations
- CVE-Based Vulnerabilities

---

# Limitations

Because Nessus does **not** authenticate to the operating system, it **cannot** detect:

- Missing Windows Updates
- Missing Linux Packages
- Registry Misconfigurations
- Local User Permissions
- Installed Software Versions
- Local Security Policies
- File Permissions
- Patch Compliance
- Operating System Configuration Issues

These require an **Authenticated Scan**.

For Authenticated Scan, your configuration is the same, but you have to add the credentials of the Windows Account
<img width="706" height="570" alt="image" src="https://github.com/user-attachments/assets/d8493864-cf20-43f5-a9cb-2e431e841bfc" />
Now, when the scan is complete 
You can see more vulnerabilities since the scanner can now log in to the target system and scan everything
With this new scan, you can again download the report and see the list of all vulnerabilities and their remediation steps. 
<img width="2121" height="792" alt="image" src="https://github.com/user-attachments/assets/7e120b60-35c9-42c0-a801-128aeda84aa9" />
<img width="2038" height="677" alt="image" src="https://github.com/user-attachments/assets/7b0a5391-aa93-47fc-b28f-b921715cf625" />
<img width="1185" height="746" alt="image" src="https://github.com/user-attachments/assets/66752761-6a6b-458c-8498-4cf98227494f" />


