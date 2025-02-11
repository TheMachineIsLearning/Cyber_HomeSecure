# WiFi Router Security Guide
*Adapted from recommendations at routersecurity.org*

## Introduction
Securing your WiFi router is crucial as it's often the first line of defense for your home network. This guide provides essential steps to protect your router and network from common security threats.

## Essential Security Measures

### 1. Router Administration
- Change the default administrator password for router access
  - Use a strong password not found in any dictionary
  - Make it unique from your WiFi password
- Verify Remote Administration is disabled
  - Check router web interface settings
  - Note: Cloud-managed routers may require specific steps to disable remote access

### 2. WiFi Network Configuration
- Change default WiFi network name (SSID)
  - Avoid using personal information in the name
  - Don't use names that reveal router brand/model
- Set a strong WiFi password
  - Minimum 16 characters
  - Change default password even if it appears random
  - [This tool](https://github.com/TheMachineIsLearning/Cyber_ParanoidAndroid) allows home uses to easily implement strong passwords across multiple devices
- Configure proper encryption
  - Use WPA2 with AES encryption (not TKIP)
  - Use WPA3 if available
  - If your router supports WPA3, disable maximum compatibility if possible

### 3. Disable Vulnerable Features
- Turn off WPS (WiFi Protected Setup)
  - WPS has a critical vulnerability in its 8-digit PIN system, which can be easily cracked through brute force attacks since the PIN is verified in two separate 4-digit parts. 
  - This design flaw means attackers only need to try around 11,000 combinations instead of 100 million. 
  - Once compromised, WPS gives attackers access to the full WPA/WPA2 password, making the feature's convenience not worth its security risk.
- Disable UPnP (Universal Plug and Play)
  - Universal Plug and Play (UPnP) should be disabled because it automatically opens ports on your router without any verification, allowing devices to configure themselves on your network. 
  - This convenience comes at a security cost, as malware can exploit UPnP to open ports and create backdoors into your network. 
  - Since UPnP doesn't have authentication, any device on your network can make these potentially dangerous port-forwarding changes.

### 4. Network Segmentation
- Set up a separate Guest Network
  - Password protect it
  - Use it for visitors
  - Connect IoT devices to guest network instead of main network
  - Keeps potentially vulnerable devices isolated from your primary network

### 5. Additional Security Measures
- Review Port Forwarding
  - Check for and remove unnecessary port forwarding rules
  - Each forwarded port is a potential security risk
  - Document any ports you need to keep open and why
- Firmware Management
  - Check for router firmware updates regularly

### 6. IPv6 Considerations
- Consider disabling IPv6 if not needed
  - Most home users don't require IPv6
  - If router can't disable IPv6, ensure IPv6 firewall is enabled
  - Refer to NSA guidance (Feb 2023) for more on IPv6

## Regular Maintenance Checklist
- Monthly:
  - Check for firmware updates
  - Review connected devices list
  - Verify guest network settings
- Quarterly:
  - Change WiFi passwords
  - Review port forwarding rules
  - Check security settings

## Warning Signs to Watch For
- Unexpected devices on your network
- Strange port forwarding rules you didn't create
- Disabled security settings you previously enabled
- Unusual network activity or slowdowns

## When to Replace Your Router
- No firmware updates for over a year
- Unable to support current security standards (WPA2/WPA3)
- Showing signs of hardware failure
- Over 5 years old
- When a brand is declared unsafe by a recognized authority 

## Additional Resources
- Visit routersecurity.org for detailed guidance, refer to the LONG LIST for even more steps
- Consult your router manufacturer's security documentation
- Check for model-specific security recommendations

## Note
This guide provides general recommendations. Specific steps may vary depending on your router model and manufacturer. Always consult your router's documentation for detailed instructions.
