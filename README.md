# Nessus Authenticated vs. Unauthenticated Vulnerability Scans

This project demonstrates how to perform both **Unauthenticated** and **Authenticated Vulnerability Scans** using **Tenable Nessus** against a **Microsoft Azure Windows Virtual Machine**. It also explains the differences between both scan types, the vulnerabilities they can detect, and how to review remediation recommendations.

---

# Lab Environment

| Component | Configuration |
|-----------|---------------|
| Vulnerability Scanner | Tenable Nessus |
| Cloud Platform | Microsoft Azure |
| Target System | Windows Virtual Machine in Azure |
| Scan Types | Basic Network Scan (Unauthenticated & Authenticated) |

---

# Unauthenticated Vulnerability Scan

An unauthenticated scan evaluates a system from an external perspective without logging into the operating system. It identifies publicly exposed vulnerabilities, open services, and network misconfigurations.

---

## Step 1 – Create a Virtual Machine

Create a Windows virtual machine using your preferred cloud provider or hypervisor.

> **Note**
> This guide uses **Microsoft Azure**.

For detailed VM deployment instructions, see my Azure VM creation project:

### Azure VM Project

https://github.com/Ashok-Bashyal/Azure-VM

Configure the **Network Security Group (NSG)** to allow communication between the Nessus scanner and the target virtual machine.

<img width="1309" height="213" alt="Azure NSG Rule" src="https://github.com/user-attachments/assets/e6f60711-0833-4ff4-bfbe-9bd169268534" />

---

## Step 2 – Create a Nessus Scan

1. Sign in to **Tenable Nessus**.
2. Navigate to **Scans**.
3. Select **Create Scan**.
4. Choose **Basic Network Scan**.
5. Enter a scan name.
6. *(Optional)* Add a description.
7. Select the appropriate Nessus scanner.
<img width="1255" height="751" alt="Target IP" src="https://github.com/user-attachments/assets/b1eef114-16b8-48ee-b725-a68e1dfde4a5" />

---

## Step 3 – Configure the Target

From the Azure portal:

1. Open the virtual machine.
2. Copy the **Private IP Address**.
3. Paste the IP address into the **Targets** field within the Nessus scan configuration.

<img width="778" height="259" alt="Target Configuration" src="https://github.com/user-attachments/assets/42a7325f-a35e-4e7b-85db-55f6dc002c88" />

---

## Step 4 – Configure Discovery Settings

Open the **Discovery** section and configure the following settings:

- **Discovery Type:** Custom
- ✅ Ping the remote host
- ✅ Fast Network Discovery

<img width="717" height="458" alt="Discovery Settings" src="https://github.com/user-attachments/assets/74a53d40-92bd-4077-8f41-59d8ab81c7a2" />

---

## Step 5 – Launch the Scan

The default scan configuration is sufficient for an unauthenticated assessment.

Click:

**Save → Launch**

> **Note**
> Scan duration depends on the size of the target environment and may take up to one hour.

---

## Step 6 – Review the Results

Once the scan completes:

1. Open the completed scan.
2. Select **See All Details**.

<img width="1813" height="596" alt="Scan Results" src="https://github.com/user-attachments/assets/c7c85359-0fee-4b87-8d15-7c1421d32319" />

Each vulnerability includes:

- Vulnerability Name
- Severity
- CVSS Score
- Risk Factor
- Affected Services
- Plugin ID
- Plugin Output

### Severity Levels

- Critical
- High
- Medium
- Low
- Informational

---

## Step 7 – Review Individual Vulnerabilities

Selecting a vulnerability displays detailed information, including:

- Description
- Synopsis
- CVSS Metrics
- Risk Information
- Plugin Output
- References
- Recommended Solution

For the complete remediation guidance, open the associated **Plugin ID**.

<img width="1523" height="681" alt="Plugin Details" src="https://github.com/user-attachments/assets/03f4ce88-df9d-49a8-9854-4987e39a54bc" />

### Example Vulnerability


<img width="1195" height="885" alt="SSL Certificate Cannot Be Trusted" src="https://github.com/user-attachments/assets/2fdd9873-208e-4129-a002-4df6155534bd" />

---

# What an Unauthenticated Scan Can Detect

Because the scanner does **not** authenticate to the operating system, it evaluates the system as an external attacker would.

Typical findings include:

- Open Ports
- Running Services
- SSL/TLS Configuration Issues
- Missing HTTP Security Headers
- Outdated Services
- Weak Encryption
- Publicly Exposed Vulnerabilities
- Network Misconfigurations
- CVE-Based Vulnerabilities

---

# Limitations of an Unauthenticated Scan

Without credentials, Nessus **cannot** inspect the operating system internally.

As a result, it cannot detect:

- Missing Windows Updates
- Missing Linux Packages
- Registry Misconfigurations
- Installed Software Versions
- Patch Compliance
- Local User Permissions
- Local Security Policies
- File and Folder Permissions
- Operating System Configuration Issues

These findings require an **Authenticated Scan**.

---

# Authenticated Vulnerability Scan

An authenticated scan logs directly into the target system using valid credentials, allowing Nessus to inspect the operating system, installed applications, registry, and security configuration.

Because Nessus has administrative visibility, authenticated scans provide a much more comprehensive security assessment.

---

## Step 1 – Configure Credentials

Create another **Basic Network Scan** (or edit the existing scan).

Navigate to:

**Credentials → Windows**

Enter the Windows account credentials that have administrative privileges on the target machine.

<img width="706" height="570" alt="Windows Credentials" src="https://github.com/user-attachments/assets/d8493864-cf20-43f5-a9cb-2e431e841bfc" />

---

## Step 2 – Launch the Scan

After configuring the credentials:

1. Save the scan.
2. Launch the scan.
3. Wait for Nessus to complete the assessment.

---

## Step 3 – Review the Results

Once completed, you'll notice significantly more vulnerabilities than were detected during the unauthenticated scan.

This is because Nessus can now:

- Log into the operating system
- Inspect installed software
- Check Windows Updates
- Analyze the Windows Registry
- Review Local Security Policies
- Verify Patch Compliance
- Inspect File Permissions
- Detect Local Misconfigurations

<img width="2121" height="792" alt="Authenticated Scan Results" src="https://github.com/user-attachments/assets/7e120b60-35c9-42c0-a801-128aeda84aa9" />

---

## Step 4 – Review Remediation

Like the unauthenticated scan, every vulnerability contains detailed remediation guidance.

Selecting a vulnerability provides:

- Description
- Risk Information
- CVSS Score
- Plugin Output
- References
- Recommended Solution

<img width="2038" height="677" alt="Authenticated Vulnerability Details" src="https://github.com/user-attachments/assets/7b0a5391-aa93-47fc-b28f-b921715cf625" />

---

## Exporting Reports

Nessus allows scan results to be exported in several formats.

Reports include:

- Executive Summary
- Vulnerability Details
- Severity Ratings
- CVSS Scores
- Affected Hosts
- Plugin Information
- Recommended Remediation

<img width="1185" height="746" alt="Exported Report" src="https://github.com/user-attachments/assets/66752761-6a6b-458c-8498-4cf98227494f" />

---

# Unauthenticated vs. Authenticated Scans

| Feature | Unauthenticated | Authenticated |
|----------|-----------------|---------------|
| Requires Credentials | ❌ | ✅ |
| External Attack Surface Assessment | ✅ | ✅ |
| Detects Open Ports | ✅ | ✅ |
| Detects Running Services | ✅ | ✅ |
| Checks Windows Updates | ❌ | ✅ |
| Reviews Registry Settings | ❌ | ✅ |
| Detects Missing Patches | ❌ | ✅ |
| Reviews Installed Software | ❌ | ✅ |
| Checks Local Security Policies | ❌ | ✅ |
| Reviews File Permissions | ❌ | ✅ |
| Patch Compliance Assessment | ❌ | ✅ |
| Overall Visibility | Limited | Comprehensive |

---

# Conclusion

Unauthenticated scans provide valuable insight into vulnerabilities visible from the network and simulate what an external attacker can discover.

Authenticated scans provide a far more comprehensive assessment by logging into the operating system with administrative credentials, allowing Nessus to identify missing patches, insecure configurations, outdated software, and other internal security issues that unauthenticated scans cannot detect.

For the most complete vulnerability assessment, organizations should regularly perform both scan types as part of a comprehensive vulnerability management program.
