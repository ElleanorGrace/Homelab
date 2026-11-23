# VLAN Segmentation Project

### Status : Planned

## Overview

This project introduces network segmentation through the implementation of VLANs and inter-VLAN access controls. The objective is to establish clear trust boundaries between personal devices, homelab infrastructure, and IoT devices while preserving required functionality and remote administration capabilities.

The existing environment operates as a flat network where all devices share the same trust boundary. While suitable for initial homelab deployments, this model increases the potential impact of a compromised device and provides limited control over east-west traffic.

## Objectives

- Separate trusted devices from homelab infrastructure and isolate IoT devices.
- Reduce opportunities for lateral movement following a compromise.
- Improve overall security posture through network segmentation.
- Establish clear access control boundaries between device classes.

## Current State

The environment currently operates on a single trusted network.

The following device categories share the same network and trust boundary:

- Personal computers
- Homelab servers
- Docker containers
- IoT devices
- Remote administrative connections

Under this design, devices can generally communicate with one another without network-level isolation.

## Target State

The environment will be segmented into dedicated VLANs based on device function and trust level.

### Trusted VLAN

Purpose:

- Personal devices
- Trusted guest devices

Design Goals:

- Highest trust level within the environment.
- Protection from unsolicited connections originating from other VLANs and outside traffic.
- No restrictions on outbound traffic to preserve the user experience
  
Considerations:

- A dedicated Guest VLAN was evaluated during the design phase. Due to the low number of guest devices expected on the network, the additional complexity of maintaining a separate VLAN was not considered justified.
- Access credentials are not publicly shared. Network access is granted only to individuals considered trusted by the network administrator.
- Should guest device usage increase in the future, or network access be required for individuals with a lower level of trust, implementation of a dedicated Guest VLAN may be reconsidered.

### Server VLAN

Purpose:

- Unraid
- Self-hosted applications
- Game servers

Design Goals:

- Centralized location for services.
- Segregation from personal devices.
- May not initiate connections to devices within the Trusted VLAN.
- Connections as needed into the IoT VLAN

### IoT VLAN

Purpose:

- Smart home devices

Design Goals:

- Isolation from trusted devices.
- Limited access to approved homelab services.

## Expected Benefits

- Reduced lateral movement opportunities.
- Improved separation between user devices and infrastructure resources.

## Success Criteria

The project will be considered successful when:

- Server VLAN devices cannot initiate connections to Trusted VLAN devices.
- Self-hosted services remain accessible.
- IoT devices retain required functionality.
- Pi-hole filtering functions correctly across all VLANs.

## Risks and Challenges

- Misconfigured firewall rules may interrupt communication between required services.
- Some IoT devices may require additional access exceptions to function correctly.
- Service discovery protocols may not operate across VLAN boundaries without additional configuration.
- Troubleshooting complexity increases compared to a flat network design.

## Security Considerations

VLAN segmentation reduces exposure between device classes but does not eliminate risk. Security controls implemented as part of this project should be viewed as one layer of a defense-in-depth strategy.

Key considerations include:

- A compromise of a Trusted VLAN device may still provide access to devices within the Server VLAN.
- Devices placed within the same VLAN remain within the same trust boundary.
- Misconfigured firewall rules may unintentionally expose services between VLANs or reduce intended isolation.
- The Unraid host remains a critical dependency within the environment due to its role in providing core infrastructure services. Compromise of the host may reduce the effectiveness of segmentation controls and impact multiple trust zones.

While VLAN segmentation significantly reduces opportunities for lateral movement and limits the impact of device compromise, it should be considered one component of an overall security strategy rather than a complete security solution.

