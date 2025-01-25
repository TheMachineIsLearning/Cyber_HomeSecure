# Home Network Security Hardening Guide

## Introduction
This repository contains comprehensive guides for securing your home network environment. As cyber threats continue to evolve, protecting your digital assets has become increasingly important. These guides provide step-by-step instructions for implementing security measures on your Windows 11 computer and WiFi router.

## Guides Available

### Windows 11 Security ([WINDOWS_COMPUTER.md](WINDOWS_COMPUTER.md))
A detailed guide for hardening Windows 11 systems, including:
- Disabling unnecessary system services
- Configuring remote access restrictions
- Implementing network security measures
- Setting up secure DNS
- Configuring Group Policy settings
- Managing network adapter protocols

This guide is designed for home users and provides clear explanations for each security measure without requiring advanced technical knowledge.

### WiFi Router Security ([WIFI.md](WIFI.md))
A comprehensive guide for securing home WiFi networks, covering:
- Router administration security
- WiFi network configuration
- Disabling vulnerable features
- Network segmentation
- Port forwarding management
- Firmware maintenance

Based on recommendations from routersecurity.org, this guide helps protect your network's first line of defense.

## Implementation Notes
- Create system restore points before making system changes
- Test system functionality after implementing security measures
- Some applications may require re-enabling specific features
- Document any exceptions you need to make for your use case

## Regular Maintenance
To maintain security:
1. Review and apply Windows updates regularly (always install security updates, I generally wait a few weeks before installing updates with feature changes only as these do sometimes cause problems that take a few days or weeks to resolve fully)
2. Check router firmware updates quarterly
3. Audit enabled services and ports periodically
4. Update security configurations as needs change

## License
[Apache 2.0](LICENSE)

## Acknowledgments
- Router security recommendations adapted from routersecurity.org
- Community security best practices
- Windows security documentation

## Security Notice
While these guides enhance system and network security, no system is completely secure. Always:
- Keep software updated
- Use strong, unique passwords
- Enable multi-factor authentication where available
- Back up important data regularly
- Monitor system and network activity for unusual behavior
