# Install Minikube in Windows 10 with Hyper-V - 2022v
## Topics
-  M    
-  Enable Hyper-V  
-  Install Chocolatey 
-  Install and Verify Minikube     

## Precondition Check
- Enabling virtualization on the computer (https://2nwiki.2n.cz/pages/viewpage.action?pageId=75202968)
- Install Windows 10, version 10.0.19044 or higher.
    - `systeminfo`  
- Windows 10 64-bit version 
    - Enterprise
    - Pro
    - Education

## Enable Hyper-V 
- Enable Hyper-V     
  -Open a PowerShell console as Administrator. 
  ```
    Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
  ```
- Restart Box

## Install Chocolatey
Chocolatey is used to install kubernetes-cli and minikube   
- Install Chocolatey    
  - https://docs.chocolatey.org/en-us/choco/setup      
  - Open a command prompt console as Administrator.       
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
  - `minikube start --driver=hyperv`   
      - Drivers(https://minikube.sigs.k8s.io/docs/drivers/)
  - `minikube config set driver hyperv`   
  - `minikube status`    
  - `minikube dashboard`      



