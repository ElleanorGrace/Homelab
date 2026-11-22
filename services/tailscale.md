# Tailscale

## Overview

Tailscale provides secure remote access to homelab services without exposing internal management interfaces directly to the internet. It is used to access self-hosted services, management consoles, and internal resources while away from the local network.

## Objectives

- Securely access homelab services from anywhere.
- Extend Pi-hole DNS filtering and ad blocking protection to trusted devices when away from home.

## Remote Access

Remote access is provided through Tailscale using separate user roles for daily use and administrative access.

### Standard User Account

The standard Tailscale account is intended for routine remote connectivity from trusted devices such as mobile phones and laptops.

Capabilities:

- Receives Pi-hole DNS filtering while away from home.
- Benefits from ad blocking and tracking protection.
- Can optionally use the homelab as an exit node for secure internet access.

Restrictions:

- No access to internal servers.
- No access to management interfaces.
- No access to subnet-routed LAN resources.
- No direct connectivity to infrastructure devices.

This account is intended to minimize risk in the event a daily-use device is compromised.

### Elevated Administrative Account

A separate administrative Tailscale account is maintained for homelab administration and troubleshooting.

Capabilities:

- Access to internal servers.
- Access to Pi-hole DNS services.
- Remote administration of self-hosted services.

The elevated account should only be used when administrative access is required.
## Security Considerations

### Strengths

- Separate Standard User and Elevated Administrative accounts enforce a least-privilege access model.
- The Standard User account provides Pi-hole DNS filtering and optional exit-node access without granting access to internal infrastructure.
- Administrative access is isolated to a dedicated Elevated Administrative account, reducing unnecessary exposure of homelab resources to daily-use devices.
- Remote access to homelab resources is provided through Tailscale, eliminating the need to expose management interfaces directly to the public internet.
- Pi-hole DNS filtering can be applied to trusted devices when away from home, providing a consistent security and privacy experience.
- Tailscale device authorization and multi-factor authentication provide additional protection against unauthorized access.

### Risks and Limitations

- A compromised device authenticated with the Elevated Administrative account will have access to internal services.
- The current network operates on a flat LAN without VLAN segmentation, allowing unrestricted communication between internal devices and the remote Administrative account.
- Security of remote access depends on the protection of Tailscale accounts, authentication methods, and enrolled devices.
- Availability of remote access is dependent on Tailscale services.
