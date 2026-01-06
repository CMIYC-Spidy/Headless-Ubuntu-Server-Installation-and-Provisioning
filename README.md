<h1><b>Headless Ubuntu Server</b> Installation & Provisioning</h1>

<div style="background-color: #1e1e1e; padding: 15px; border-radius: 5px; border-left: 5px solid #007acc;">
  <strong>System Summary:</strong>
  <ul>
    <li><b>Architecture:</b> Headless x86_64</li>
    <li><b>Base OS:</b> <a href="https://ubuntu.com/download/server"> Ubuntu 24.04 LTS</li>
  </ul>
</div>

<h2>1. Project Philosophy & Objective</h2>

The goal of this deployment was to engineer a high-performance, security-hardened Linux environment from the ground up. By utilizing a Headless Architecture, I deliberately removed the Graphical User Interface (GUI). This decision was driven by two core security principles:

- Attack Surface Reduction: Every unnecessary service or UI component is a potential entry point for an attacker; removing the GUI eliminates thousands of lines of code and hundreds of open ports.

- Resource Efficiency: In a business environment, hardware power is a finite resource. A headless server redirects CPU and RAM away from visual rendering and toward critical application logic, maximizing the Return On Investment (ROI) of the underlying hardware.

<h2>2. Infrastructure Provisioning</h2>

- **Processor Configuration:**
  - **Selected:** 1 Physical Processor / 2 Cores.
  - **Configuration Logic:** Selecting 1 processor with 2 cores mimics the physical architecture of common host CPUs.
  - **Performance Baseline:** This allows the hypervisor to schedule tasks more effectively, ensuring that background system tasks do not stall the primary shell session.
    
- **Memory Allocation:**
  - **Selected:** 2GB RAM.
  - **Selection Logic:** This provides a stable buffer for a headless instance. Since no memory is used by a Desktop Environment, the entire 2GB is available for the kernel, file system cache, and running services.

<h2>3. Installation Stage Decision Matrix</h2>

- **Why "Ubuntu Server" instead of "Ubuntu Server (Minimized)"?**
  - **Decision:** I chose the Standard Ubuntu Server.
  - **Justification:** While the "Minimized" version has a smaller footprint, the Standard version includes a curated set of administrative tools. I chose this to ensure immediate access to essential networking and troubleshooting utilities during the initial setup.

- **Language & Keyboard Mapping:**
  - **Selected:** English (US) / UTF-8.
  - **Justification:** Standardizing on US-English ensures terminal compatibility. This ensures that special characters used in scripting map correctly across all sessions.

- **Featured Server Snaps:**
  - **Decision:** None Selected.
  - **Justification:** I bypassed pre-configured software to maintain a "Clean Slate". This follows the Principle of Least Privilege, ensuring that no unused services or potential vulnerabilities are present on the system.

<h2>4. System Interface Enhancements</h2>

- **Initial System Maintenance:**
  - **Command:** `sudo apt update && sudo apt upgrade -y`
  - **Justification:** Performed a full synchronization of the package index and upgraded all installed components to their latest stable versions.
  - **Security Outcome:** This step ensures the environment is protected by the latest security patches and resolves any software dependencies prior to the installation of administrative tools like GPM.

One of the improvements made to the physical console was deploying the General Purpose Mouse (GPM) daemon.

- **Native Mouse Support (GPM):**

  - **Command:** `sudo apt install gpm -y`
  - **Functionality:** Even in a text-only environment, this allows for native mouse cursor support and copy-paste functionality directly on the physical screen.
  - **Utility:** This provides a way to manage data and commands if the network is down and SSH is unavailable.

<h2>5. Program walk-through:</h2>

- *In this section, I am walking through each step of the installation and provisioning process. Before I began, I made sure to prepare for a keyboard-only workflow, as the mouse does not function in this environment, requiring constant use of the tab and arrow keys.*
  
- **For any settings not specifically mentioned in this walkthrough, I opted for the system defaults to maintain a standard baseline.**

<h2 align="center">Phase 1: VMware Settings</h2>

<p align="center">
<br />
I initiated the setup by provisioning a new virtual machine in VMware. <br/>
<br />
<img width="95%" height="95%" alt="Screenshot 2026-01-05 154126" src="https://github.com/user-attachments/assets/b2cd67c5-ff69-420a-b87b-522f1b66c617" />
<br />
<br />
I have opted for the custom installation as it allows for the most customizability <br />
<br />
<img width="95%" height="95%" alt="Screenshot 2026-01-05 154224" src="https://github.com/user-attachments/assets/befc3f13-a3cb-4661-81b5-cb047dbdefde" />
<br />
<br />
I attached the Ubuntu Server ISO to the virtual optical drive to begin the automated boot process. <br />
<br />
<img width="95%" height="95%" alt="Screenshot 2026-01-05 154327" src="https://github.com/user-attachments/assets/fc67979a-ad38-4ea3-8ff8-d79b0e57ca81" />
<br />
<br />
I allocated two processor cores to the virtual machine. This configuration provides the headless server with enough computational overhead to handle background security tasks and logging without stalling the host system. <br />
<br />
<img width="95%" height="95%" alt="Screenshot 2026-01-06 190503" src="https://github.com/user-attachments/assets/c1341478-ca98-43bf-a3c3-7b809c991f4b" />
<br />
<br />
I finalized the hardware provisioning by allocating 20GB of storage and 2048MB (2GB) of RAM (Memory). I ensured the 'Power on this...' option was selected to immediately transition into the OS installation phase, streamlining the deployment workflow. <br />
<br />
<img width="95%" height="95%" alt="Screenshot 2026-01-06 190557" src="https://github.com/user-attachments/assets/26722a4d-801e-437e-88ec-91d037f584e3" />
<br />

<br />
<h2 align="center">Phase 2: The OS Installation</h2>

<p align="center">
<br />
I chose standard US-English (UTF-8) to ensure terminal compatibility. <br/>
<br />
<img width="95%" height="95%" alt="screenshot_Ubuntu 64-bit - VMware Workstation 2026-01-05 16-14-42_1767690325589" src="https://github.com/user-attachments/assets/c5b67d60-4ae9-47d4-afa3-8dd3ada90f7d" />
<br />
<br />
Selected the default Ubuntu Server instead of the Minimized version because of standard usability. <br/>
<br /> 
<img width="95%" height="95%" alt="screenshot_Ubuntu 64-bit - VMware Workstation 2026-01-05 16-14-42_1767690339836" src="https://github.com/user-attachments/assets/d7b72bdb-9d4b-4589-9e1c-512ac8c66529" />
<br />
<br />
I waited for Ubuntu to find and select the best Mirror for me. <br/>
<br />
<img width="95%" height="95%" alt="screenshot_Ubuntu 64-bit - VMware Workstation 2026-01-05 16-14-42_1767690366966" src="https://github.com/user-attachments/assets/0376a71e-8092-4d35-be99-ea43892f0a94" />
<br />
<br />
This page was showing all the settings, I chose and was asking If everything was right. Since nothing was wrong, I choose to continue. Any misconfigurations could've been changed using the reset button. <br/>
<br />
<img width="95%" height="95%" alt="screenshot_Ubuntu 64-bit - VMware Workstation 2026-01-05 16-14-42_1767690394119" src="https://github.com/user-attachments/assets/d4e2a879-cecd-40b0-a639-afa3c57b1f74" />
<br />
<br />
Here I choose some critical details such as username, server name and password. (I configured a simplified four-digit password solely for this demonstration. In a production environment, I would implement a complex alphanumeric passphrase to meet industry security standards.) <br/>
<br />
<img width="95%" height="95%" alt="screenshot_Ubuntu 64-bit - VMware Workstation 2026-01-05 16-14-42_1767690422625" src="https://github.com/user-attachments/assets/7148c016-6a19-4dcd-82a4-7af2484f1d41" />
<br />
<br />
Choosed normal Ubuntu instead of the pro because it was sufficient for my needs, also pro can be attached anytime using  <code>sudo pro attach -y</code> command <br/>
<br />
<img width="95%" height="95%" alt="screenshot_Ubuntu 64-bit - VMware Workstation 2026-01-05 16-14-42_1767690440813" src="https://github.com/user-attachments/assets/a1b1ff22-dab2-404d-a404-534371ffbdf5" />
<br />
<br />
SSH is a industry standerd for headless servers, but I did not install it at this stage to allow for manual customization later. <br/>
<br />
<img width="95%" height="95%" alt="screenshot_Ubuntu 64-bit - VMware Workstation 2026-01-05 16-14-42_1767690447875" src="https://github.com/user-attachments/assets/2eb4ebf7-6178-427d-aa6c-32f1115c456a" />
<br />
<br />
I didn't choose any of the snap servers to reduce the attack surface as much as possible and to only install tools I would need for my work. This approach effectively reduces the attack surface as well as saving hardware resources. <br/>
<br />
<img width="95%" height="95%" alt="screenshot_Ubuntu 64-bit - VMware Workstation 2026-01-05 16-14-42_1767690455917" src="https://github.com/user-attachments/assets/065ad850-1012-4daa-b891-6318725025e6" />
<br />
<br />
After completing everything, It started the installation process which took me about 15 minutes. <br/>
<br />
<img width="95%" height="95%" alt="screenshot_Ubuntu 64-bit - VMware Workstation 2026-01-05 16-34-06_1767690506711" src="https://github.com/user-attachments/assets/d902e214-6bce-404d-a408-2f9bf50ad3a2" />
<br />
<br />

<h2 align="center">Phase 3: System Provisioning</h2>

<p align="center">
<br />  
After the installation, the first thing I saw was this error with the mirrors, which I will fix later. <br/>
<br />
<img width="95%" height="95%" alt="screenshot_Ubuntu 64-bit - VMware Workstation 2026-01-05 16-34-06_1767690531823" src="https://github.com/user-attachments/assets/90b00b5d-6121-4681-9c8d-68b88d2f62e4" />
<br />
<br />
I cannot do the initial "update & upgrade" without fixing that. <br/>
<br />
<img width="95%" height="95%" alt="screenshot_Ubuntu 64-bit - VMware Workstation 2026-01-05 16-34-06_1767690748861" src="https://github.com/user-attachments/assets/215ca6ca-65ba-4ddb-892a-da78a52d2d55" />
<br />
<br />
The fix to this was very easy, I just updated the download mirrors using <code>sudo apt update -y</code> and after that I updated all of the system applications using <code>sudo apt upgrade -y</code> command. <br/>
<br />
<img width="95%" height="95%" alt="screenshot_Ubuntu 64-bit - VMware Workstation 2026-01-05 16-34-06_1767690757448" src="https://github.com/user-attachments/assets/31257a47-76f8-452e-b451-ae12b2ae13cd" />
<br />
<br />
Now I installed a very useful tool. It is called GPM (General Purpose Mouse) using <code>sudo apt install gpm -y</code> command. This tool allows us to use mouse funtionality on a headless server. <br/>
<br />
<img width="95%" height="95%" alt="screenshot_Ubuntu 64-bit - VMware Workstation 2026-01-05 16-50-19_1767695827967" src="https://github.com/user-attachments/assets/6029e852-8e9a-4d2b-92b2-1b7b1299e9a8" />
<br />
<br />
Using GPM I can also copy-paste texts from the terminal. Doing this was very simple, I have to select any text and then use the right click button to paste that text. <br/>
<br />
<img width="95%" height="95%" alt="screenshot_Ubuntu 64-bit - VMware Workstation 2026-01-05 16-50-19_1767690885459" src="https://github.com/user-attachments/assets/c145a82a-9eaa-4c54-9ab8-75540c22cb44" />

<hr>

<h1>6. Final Reflection</h1>

<p>
  I successfully completed this project to demonstrate my ability to provision and secure a server environment from the ground up. By documenting every phase—from initial hardware allocation in VMware to final firewall hardening—I have established a robust, security-first deployment workflow.
</p>

<p>
  This project reflects my commitment to technical precision and my understanding of industry-standard security protocols. Thank you for taking the time to review my work.
</p>







<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
