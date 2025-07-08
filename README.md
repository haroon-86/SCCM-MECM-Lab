# 📦 Skype for Business Deployment via Microsoft Endpoint Configuration Manager



## 📘 Overview
This guide documents the step-by-step process for creating and deploying **Skype for Business** using **Microsoft Endpoint Configuration Manager** (formerly SCCM). The deployment targets users across a network environment by leveraging an MSI installer, setting up deployment configurations, and validating installation via client systems.

---

## 🛠️ Step-by-Step Process

### 1. Preparing the Installation Files
- Located the Skype for Business MSI installer:  
  `C:\Packages\Skype for Business\Skype-8.92.0.401.msi`
- Verified proper permissions on the folder:
  - **Domain Computers** have _Read & execute_ permissions
  - Other necessary groups (**LabAdmin**, **Domain Users**, **Administrators**) have appropriate access

![Figure 1: Read & Execute Permissions](1.%20Read%20&%20Execute%20is%20On.png)

---

### 2. Creating the Application
- Navigated to:  
  `Software Library > Application Management > Applications`
- Right-clicked and selected **Create Application**

![Figure 2: Create Application Menu](2.%20Create%20Application.png)

- Selected **Windows Installer (*.msi file)** as the application type

![Figure 2.1: MSI File Type Selection](2.1%20Create%20Application.png)

- Specified the UNC path to the MSI file:  
  `\\<server>\Packages\Skype for Business\Skype-8.92.0.401.msi`  
  ⚠️ _Note: Must use a UNC path (not a local path like C:\) for proper network deployment._

  ### 3. Deploying the Application
- Right-clicked application and selected **Deploy**

![Figure 3: Deploy Menu](3.%20Deploy.png)

#### Deployment Settings:
- **Collection:** All Users and User Groups  
- **Action:** Install  
- **Purpose:** Available (user-initiated)  
- **Content Distribution:** Corp Distribution Points (DP group)  

![Figure 3.1: General Deployment Settings](3.1%20Deploy.png)
![Figure 3.2: Content Distribution](3.2%20Deploy.png)
![Figure 3.3: Deployment Behavior](3.3%20Deploy.png)

#### User Experience:
- Display in Software Center with all notifications  
- Show dialog window for required changes  
- Allow software installation outside maintenance windows  

![Figure 3.4: User Experience Settings](3.4%20Deploy.png)

#### Alert Configuration:
- Set success/failure thresholds  
- Enabled Operations Manager alerts  

![Figure 3.5: Alert Settings](3.5%20Deploy.png)

#### Configured Application Details:
- **Name:** Skype 8.92  
- **Publisher:** Microsoft  
- **Version:** 8.92  
- **Comments:** "This is Skype for Business"

![Figure 2.3: Application Configuration](2.3%20Create%20Application.png)

![Configuration Manager Deployment](4.%20Configuration%20Manager.png)

![Skype Installed](5.%20Skype%20Installed.png)

#### Installation Command:
```bash
msiexec /i "Skype-8.92.0.401.msi" /q 
```
