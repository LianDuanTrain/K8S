# Install Minikube in Windows 10 via Docker Desktop - 2021 Version
## Topics
-  Precondition Check   
-  Install Docker Desktop 
-  Install Minikube    

## Precondition Check
- Enabling virtualization on computer (https://2nwiki.2n.cz/pages/viewpage.action?pageId=75202968)
- Install Windows 10, version 1903 or higher.
    - `systeminfo`  
- Enable Windows Subsystem for Linux (WSL) 2 feature on Windows (https://docs.microsoft.com/en-us/windows/wsl/install-win10).
- Download and install the Linux kernel update package(https://docs.microsoft.com/en-us/windows/wsl/install-win10#step-4---download-the-linux-kernel-update-package).

## Install Docker Desktop 
- Download
- Install
- Verification

## Install Minikube
Chocolatey is used to install kubernetes-cli and minikube
https://docs.chocolatey.org/en-us/choco/setup
- Install
  - `choco install kubernetes-cli`  
  - `choco install minikube`  
- Verification
  - `minikube start` 
  - `minikube status`  
  - `minikube dashboard`
  - `kubectl version`     


<font size=1 >Icons made by www.freepik.com</font> 

