# Install Minikube in Windows 10 via Docker Desktop - 2022v
## Topics
-  Precondition Check    
-  Install Docker Desktop  
-  Install Chocolatey 
-  Install and Verify Minikube     

## Precondition Check
- Enabling virtualization on computer (https://2nwiki.2n.cz/pages/viewpage.action?pageId=75202968)
- My demo box is on Windows 10 (10.0.19044).
    - `systeminfo` 

- Windows 10 version Less then 10.0.19044
    - Enable Windows Subsystem for Linux (WSL) 2 feature on Windows (https://docs.microsoft.com/en-us/windows/wsl/install-win10).
    - Download and install the Linux kernel update package(https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi).

## Install Docker Desktop 
- Download
    - https://docs.docker.com/desktop/install/windows-install/
- Install
- Verification

## Install Chocolatey
Chocolatey is used to install kubernetes-cli and minikube   
- Install Chocolatey   
https://docs.chocolatey.org/en-us/choco/setup       
``` 
@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "[System.Net.ServicePointManager]::SecurityProtocol = 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
```
- Upgrade Chocolatey
   - choco upgrade chocolatey   
[<image src="./images/upgrate.jpg" width="50%">]   

## Install and Verify Minikube  

- Install
  - `choco install kubernetes-cli`  
  - `choco install minikube`  
- Verify
  - `minikube start` 
  - `minikube status`  
  - `minikube dashboard`
  - `kubectl version`     



