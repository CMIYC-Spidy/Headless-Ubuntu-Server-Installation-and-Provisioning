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

<p align="center">
My Text: <br/>
<img src="My Image"/>
<br />
<br />
My Text:  <br/>
<img src="My Image"/>
<br />
<br />






<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
