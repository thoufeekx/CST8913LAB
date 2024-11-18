

# VM Migration Lab 10 Report

## Overview

In this lab, the task was to set up a virtualized environment using VMware Workstation, install and configure a Windows Server OS, deploy a basic "Hello World" web application, and migrate the virtual machine (VM) to Azure using Azure Migrate. Post-migration, we validated the application functionality and performed a failover test to ensure resilience.

## Table of Contents

1. [Milestone 1: Environment Setup](#milestone-1-environment-setup)
2. [Milestone 2: OS Installation](#milestone-2-os-installation)
3. [Milestone 3: Application Deployment](#milestone-3-application-deployment)
4. [Milestone 4: Migration Assessment](#milestone-4-migration-assessment)
5. [Milestone 5: VM Migration Execution](#milestone-5-vm-migration-execution)
6. [Milestone 6: Validation and Failover Testing](#milestone-6-validation-and-failover-testing)
7. [Conclusion and Reflection](#conclusion-and-reflection)

---

## Milestone 1: Environment Setup

### Task: Install VMware Workstation and Create a New VM

The first step in the lab was to set up VMware Workstation, which allows you to run virtualized environments on a local machine. This was followed by the creation of a new virtual machine (VM).

**Steps:**
1. Download VMware Workstation from the official website.
2. Install VMware Workstation on the local machine.
3. Open VMware Workstation and create a new virtual machine, specifying the hardware settings such as CPU, RAM, and disk size. We configured the VM with 2 GB of RAM and 60 GB of storage.

**Expected Outcome:**  
A fully configured VMware Workstation with a new virtual machine ready for the installation of the operating system.

---

## Milestone 2: OS Installation

### Task: Install Windows Server OS on the VM

After setting up VMware, the next step was to install the Windows Server OS on the VM.

**Steps:**
1. Select the Windows Server ISO file to the virtual machine option.

3. Configure the network settings, and set up administrator credentials after the installation completes.

**Expected Outcome:**  
A Windows Server instance running on the VM with initial configurations such as networking and user setup completed.


![VM with Two VMs](images/2.png)  
*VM Workstation with Two Virtual Machines Configured*

---

## Milestone 3: Application Deployment

### Task: Deploy a “Hello World” Web Application on the Windows Server

Once the Windows Server OS was installed,deployed a simple "Hello World" web application to verify that the VM was functioning correctly and could serve web content.

**Steps:**
1. Install IIS (Internet Information Services) via the "Add Roles and Features" wizard.
2. Create a simple HTML file with the text "Hello World" and save it in the IIS root directory (`C:\inetpub\wwwroot`).
3. Open a web browser within the VM and access `http://localhost/` to confirm the application was deployed successfully.

**Expected Outcome:**  
The "Hello World" web page should be accessible via the internal network of the VM.

![Hello worlds](images/index.png)  
*Hello World inside the localhost sever*

---

## Milestone 4: Migration Assessment

### Task: Use Azure Migrate to Perform an Assessment of the VM

Azure Migrate was used to assess the readiness of the VM for migration to Azure. This tool evaluates the compatibility of on-prem virtual machines with Azure, identifying potential issues and recommendations.

**Steps:**
1. Install the Azure Migrate appliance on the on-prem VM.
2. Set up the discovery process by connecting the on-prem environment to Azure Migrate.
3. Initiate the assessment process, selecting the VM to assess.

**Expected Outcome:**  
A migration readiness assessment report that provides compatibility results, highlighting any issues that might require attention before migration.

![Azure Migrate Installed in On-Prem VM](images/3.png)  
*Azure Migrate Installation in the On-Prem VM*

![Connectivity to Azure](images/4.png)  
*Connectivity to Azure for Migration Assessment tool*

### Task: Discovery of Sources

The next step was to discover the on-prem VM that would be migrated to Azure.

**Steps:**
1. In Azure Migrate, configure the discovery of the on-prem VMs by linking the VMware environment.
2. Run the discovery process to identify the VMs available for migration.

**Expected Outcome:**  
A list of discovered VMs that are ready for migration to Azure.

![Credentials of Sources](images/5.png)  
*Adding credentials of Sources such as IP address, username, friendly name*

![Discovery Sources](images/6.png)  
*Discovery Sources for Migration Process*

![Assessment Sources](images/6.1.png)  
*Assessment done on Discovered Sources for Migration Process*

### Task: Installing Replication appliance

1. VM2(Site Replicantion VM) the migration tools The replication appliance (Configuration Server) is installed using azure migrate

2. Installing prerequisite such us mysql server, network selection, IIS

![Replication appliance](images/7.png)  
*Download replication appliance and register key*

![Pre requisite to run configuration server](images/8.png)  
*All Pre requisite installed to run configuration server*

![Finish installation](images/9.png)  
*Complete installation of replication appliance*

---

## Milestone 5: VM Migration Execution

### Task: Replicate the Discovered VM

The next phase of the lab involved replicating the on-prem VM to Azure using Azure Site Recovery (ASR). This ensures that the VM can be migrated safely to Azure.

**Steps:**
1. Install the Azure Site Recovery Unified Agent(ASR) agent / Mobility agent on the on-prem VM.
2. Provide configuration server Ip and passphrase.


![Download Application in Replication VM](images/11.png)  
*Download and Install Application in the Replication VM*

![Download Application in Replication VM](images/12.png)  
*Seleting and start Replication VM*

![Download Application in Replication VM](images/13.png)  
*Settings to choose for Replication*

### Task: Execute Initial Migration Phase

With replication complete, the initial migration phase was started.

**Steps:**
1. Start the migration process in Azure Migrate, selecting the replicated VM.
2. Monitor the migration progress to ensure no issues occur during the process.

**Expected Outcome:**  
The VM is successfully migrated to Azure, with all necessary settings applied.

![Initial Migration Phase](images/16.png)  
*Initial Migration Phase from On-Prem to Azure*

![Initial Migration Phase](images/17.png)  
*Health status of migration vm*

![Initial Migration Phase](images/20.png)  
*Test migration of vm*

![Initial Migration Phase](images/18.png)  
*Clean up of Test migration*


![Initial Migration Phase](images/19.png)  
*Migrated VM inside resource group*

---

## Milestone 6: Validation and Failover Testing

### Task: Validate the Migrated VM's Functionality

Once the migration was complete, we needed to verify that the VM and the "Hello World" application were working properly in Azure.

**Steps:**
1. Use Remote Desktop Protocol (RDP) or SSH to access the migrated VM in Azure.
2. Open a browser and verify that the "Hello World" application is accessible, similar to how it was on the on-prem VM.
3. Conduct a failover test by simulating a failure in the Azure environment and ensuring the VM recovers using secondary resources.

**Expected Outcome:**  
The migrated VM should function properly, and the application should remain accessible after failover.

![Migrated VM](images/23.png)  
*Failover testing completed for replicated vm*

![Migrated VM](images/21.png)  
*Creating an NSG group for inbound and outbound rules*

![Migrated VM](images/22.png)  
*Creating public for RDP connection*


![RDP and SSH Port on NSG](images/24.png)  
*RDP connection to migrated VM*

![RDP and SSH Port on NSG](images/25.png)  
*Migrated VM with hello world server*

### Fail over testing


### **Complete Migration**  
The first step in the failover testing process is to complete the migration of the VM. By selecting **Complete Migration** in the **Recovery Services Vault**, you finalize the process, ensuring that the VM is fully migrated and prepared for disaster recovery testing.

![complete migration](images/26.png)  
*Completed migration for failover testing*

### **Failover Settings Choose**  
Once migration is complete, configure the failover settings. This involves selecting a recovery point, such as **Latest Processed** or **Application Consistent**, and choosing a test network to simulate the failover scenario without affecting the production environment.

![complete migration](images/27.png)  
*Failover settings page*


### **Complete Failover**  
After configuring the failover settings, initiate the **Complete Failover** process. This step transitions the VM to the recovery environment, testing whether it can successfully switch to the secondary site under disaster recovery conditions.

![complete failover](images/28.png)  
*Failover settings page*

### **Failover Test VM**  
Following the complete failover, perform a **Test Failover**. This step spins up the VM in the test environment to verify that the failover process works as expected and the system is functional in the new environment.

![complete failover](images/29.png)  
*Failover test vm inisde resource group*


### **Hello World in Failover Testing**  
Finally, "Hello World" application on the VM during the test. This verifies that the failover VM is operational and all configurations are correct, ensuring the environment is ready for real disaster recovery scenarios.

![complete failover](images/30.png)  
*Hello world in failover test vm*


---

## Conclusion and Reflection

### Reflection on the Migration Process

The migration process was relatively smooth, but there were challenges such as ensuring compatibility between the on-prem environment and Azure. The Azure Migrate tool provided an insightful assessment, identifying key areas that required attention, such as network configurations and storage options. The replication process was straightforward, but the failover test proved essential in verifying the VM's resilience in a cloud environment.

The entire process demonstrated the importance of thorough testing, both before and after migration, to ensure minimal downtime and ensure business continuity.



---



