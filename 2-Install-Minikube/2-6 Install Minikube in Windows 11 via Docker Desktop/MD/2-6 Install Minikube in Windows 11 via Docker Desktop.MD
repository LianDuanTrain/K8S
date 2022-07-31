# Install Minikube in Windows 11 via Docker Desktop  
## Topics
-  Precondition Check    
-  Install and Verify Docker Desktop  
-  Install Chocolatey 
-  Install and Verify Minikube     

## Precondition Check
- Enabling virtualization on the computer (https://2nwiki.2n.cz/pages/viewpage.action?pageId=75202968)
- My demo box is on Microsoft Windows 11 Pro (10.0.22000).
    - `systeminfo` 

## Install and Verify Docker Desktop 
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



