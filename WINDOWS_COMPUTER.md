# Windows 11 Security Hardening Guide for Home Users

## Introduction

As cyber threats continue to evolve and become more sophisticated, securing your Windows 11 system has never been more important. This guide provides step-by-step instructions for home users to enhance their system security through service management, network configuration, and policy adjustments. These measures help protect against common attack vectors while maintaining system usability.

## Security Measures

### 0. Disable Network Discovery and File Sharing

#### Steps:
1. Open Control Panel
2. Navigate to Network and Sharing Center
3. Click "Change advanced sharing settings"
4. For all network profiles (Private and Public):
   - Turn off network discovery
   - Turn off file and printer sharing
   - Turn off Public folder sharing
5. Click "Save changes"

#### Why:
Network discovery and file sharing are convenient for home networks but can be exploited if your computer is connected to untrusted networks. Disabling these features prevents unauthorized access to your files and makes your computer invisible to network scanning.

### 1. Disable Unnecessary Services

#### Steps:
1. Open Services (Press Windows + R, type `services.msc`, press Enter)
2. For each service listed below, right-click and select Properties
3. Set "Startup type" to "Disabled"
4. Click "Stop" if the service is running
5. Click "Apply" and "OK"

Services to disable:
- AllJoyn Router Service
- Secure Socket Tunneling Protocol (SSTP)
- SSDP Discovery
- UPnP Device Host
- Wi-Fi Direct Services
- Connected User Experiences and Telemetry (DiagTrack)
- Remote Desktop Configuration
- Remote Desktop Services
- Remote Registry
- Windows Remote Management
- Xbox Live Authentication Manager
- Xbox Live Game Save
- Xbox Live Networking Service

#### Why:
Each disabled service reduces your system's attack surface. For example, SSTP (Secure Socket Tunneling Protocol) operates on port 443, the same port used for secure web browsing. If compromised, malicious traffic could blend in with normal encrypted web traffic, making attacks harder to detect. Similarly, services like UPnP (Universal Plug and Play) and SSDP (Simple Service Discovery Protocol) can be exploited for network attacks if left enabled when not needed.

### 2. Configure DNS over HTTPS (DoH)

#### Steps:
1. Open Settings
2. Navigate to Network & Internet > Wi-Fi or Ethernet (depending on your connection)
3. Click on your active network connection
4. Under "DNS server assignment", click "Edit"
5. Change "Automatic (DHCP)" to "Manual"
6. Enable "IPv4"
7. Add preferred DNS servers (e.g., Cloudflare: 1.1.1.1 or Google: 8.8.8.8)
8. Enable "DNS over HTTPS"

#### Why:
DNS (Domain Name System) converts human-readable website names into IP addresses. DNS over HTTPS encrypts these queries, protecting against DNS poisoning attacks where attackers redirect you to malicious websites by intercepting and manipulating DNS requests.

### 3. Group Policy Security Settings

#### Steps:
1. Open Group Policy Editor (Press Windows + R, type `gpedit.msc`, press Enter)
2. Navigate through the following settings:

For Reverse Shell:
- Computer Configuration > Windows Settings > Security Settings > Local Policies > Security Options
- Find "Network security: Restrict clients allowed to make remote calls to SAM"
- Enable and deny all

For Windows Remote Shell:
- Computer Configuration > Administrative Templates > Windows Components > Windows Remote Shell
- Find "Allow Remote Shell Access"
- Disable

For LLMNR:
- Computer Configuration > Administrative Templates > Network > DNS Client
- Find "Turn off multicast name resolution"
- Enable

For Logging:
- Computer Configuration > Administrative Templates > Windows Components > Windows PowerShell
- Enable "Turn on PowerShell Script Block Logging"
- Enable "Turn on PowerShell Transcription"

#### Why:
- Disabling reverse shell capabilities prevents attackers from establishing unauthorized remote connections to your computer
- Disabling LLMNR (Link-Local Multicast Name Resolution) prevents a common attack where adversaries can intercept local network name resolution requests
- Enhanced logging helps detect and investigate potential security incidents

### 4. Disable Remote PowerShell Access

#### Steps:
1. Open PowerShell as Administrator
2. Run the following commands in order:

```powershell
# Disable PowerShell remoting
Disable-PSRemoting -Force

# Stop and disable the Windows Remote Management service
Stop-Service WinRM -PassThru
Set-Service WinRM -StartupType Disabled -PassThru

# Disable Windows Firewall rules for WinRM
Set-NetFirewallRule -DisplayName 'Windows Remote Management (HTTP-In)' -Enabled False

# Clear trusted hosts
Set-Item WSMan:\localhost\Client\TrustedHosts -Value "" -Force
```

#### Why:
These commands provide multiple layers of protection:
- Disables PowerShell remoting to prevent remote command execution
- Stops and disables the Windows Remote Management service that handles remote connections
- Blocks the network ports used for remote management through the firewall
- Removes any trusted hosts that might have been previously configured

This comprehensive approach helps ensure that attackers cannot use PowerShell or Windows Remote Management to gain unauthorized access to your system. For home users, remote management capabilities are rarely needed, so disabling them reduces your attack surface without impacting normal computer use.

### 5. Additional Service Configurations

#### Steps:
1. Open Services (Press Windows + R, type `services.msc`, press Enter)
2. For each service listed below, right-click and select Properties
3. Set "Startup type" to "Disabled"
4. Click "Stop" if the service is running
5. Click "Apply" and "OK"

Additional services to disable:
- IP Helper (iphlpsvc) - IPv6 transition technologies
- Net.Tcp Port Sharing Service
- Routing and Remote Access
- WebClient
- Downloaded Maps Manager
- Geolocation Service (if you don't use location-based apps)
- Windows Mobile Hotspot Service (if you don't share your internet connection)
- Function Discovery Provider Host and Resource Publication
- Windows Connect Now

#### Why:
These additional services are rarely needed by home users and can present security risks:
- IP Helper and Net.Tcp Port Sharing services can be exploited for network attacks
- WebClient service could allow remote file system access
- Routing and Remote Access could be exploited for network pivoting
- Location services can be a privacy concern if not needed
- Discovery services can leak information about your system to the network

### 6. Configure Network Adapter Protocols

#### Steps:
1. Open Network Connections (Press Windows + R, type `ncpa.cpl`, press Enter)
2. For each network adapter (Wi-Fi, Ethernet):
   - Right-click the adapter and select Properties
   - Uncheck all items except:
     - "Internet Protocol Version 4 (TCP/IPv4)"
     - "Link-Layer Topology Discovery Mapper I/O Driver" (needed for network troubleshooting)
   - Specifically ensure these are disabled:
     - "Internet Protocol Version 6 (TCP/IPv6)"
     - "Client for Microsoft Networks"
     - "File and Printer Sharing for Microsoft Networks"
     - "Microsoft LLDP Protocol Driver"
     - "QoS Packet Scheduler"
   - Click "OK" to save changes

#### Why:
- IPv6 is often unnecessary for home users and can be exploited if misconfigured
- Removing unused protocols reduces the attack surface
- Disabling file sharing protocols at the adapter level provides an additional layer of security
- QoS and LLDP protocols are typically only needed in enterprise environments

### 7. Block SMB Ports

#### Steps:
1. Open Windows Defender Firewall with Advanced Security
2. Create new outbound rules for TCP ports 445 (SMB) and 137-139 (NetBIOS)
3. Block these ports unless specifically needed for home network file sharing

#### Why:
SMB (Server Message Block) is a protocol used for file sharing but is also commonly exploited in attacks. Blocking these ports helps prevent unauthorized file sharing and protects against various SMB-based attacks.

## Important Notes

- Test system functionality after implementing these changes
- Some services might be required for specific applications or games
- Create a system restore point before making these changes
- Regular system updates remain crucial for security

## Contributing

Feel free to submit issues and enhancement requests. Security is a community effort, and your input helps improve this guide for everyone.

## License

[MIT License](LICENSE)
