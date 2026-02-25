# WSUS Deployment with Downstream Autonomous Server (Windows Server 2022)

## Overview
This lab demonstrates the deployment of a Windows Server Update Server (WSUS) infrastructure in a domain environment using:

-Windows Server (Primary WSUS Server)

-Windows Server (Domain Controller)

-Windows Server Core (Downstream WSUS - Autonomous Mode)

-2 Windows 10 Clients

*All machines are joined to an Active Directory Domain. --> (images/Computers-Join-to-Domain.PNG)

## Lab Environment 

-Hypervisor: Microsoft Hyper-V

-WSUS Port: 8530(HTTP)

-Clients configured via Domain Group Policy


## Design

### Primary WSUS Server

-Installed on Windows Server 2022 (Desktop Experience)

-Configured for:

   -Products & Classification 

   [Products] --> images/Installed-Products.PNG
   
   
   -Synchronization manually --> images/Synchronization-Schedule.PNG
   
   -Update Approvals --> images/Approved-Updates.PNG
   
   
### Downstream WSUS (Server Core)

-Installed on Windows Server Core

-Configured as **Autonomous Downstream Server** --> images/Set-WSUS2CORE-as-Autonomous.PNG

-Synchronizes updates from Primary WSUS

-Managed remotely through WSUS Console installed on Desktop Experience Server --> images/Console-WSUS2Core.PNG


### Domain Controller

-Manages Active Directory

-Applies Group Policy to clinets for WSUS Configuration 

### Windows 10 Clients

-Joined to Domain

-Receive WSUS configuration via Group Policy 

-Download Updates from Primary WSUS Server --> images/Connceted-Clients.PNG

## Group Policy Configuration

Clinets are configured through Domain Group Policy:

Computer Configuration -> Administrative templates -> Windows Components -> Windows Update 

Enabled settings:

**Specify Intranet Microsoft Update Servive Location**:

WSUS Server: http://WSUS-Server.Domain-Name.com:8530 --> --> images/GPO-Config-Win1&Win2.PNG
