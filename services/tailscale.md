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

Access to the Trusted VLAN is intentionally denied. This prevents administrative sessions, servers, and potentially compromised infrastructure services from initiating connections to personal devices while still allowing management of homelab resources.

Capabilities:

- Access to Server VLAN resources.
- Access to Pi-hole DNS services.
- Remote administration of self-hosted services.

The elevated account should only be used when administrative access is required.

### Access Control

Tailscale ACLs are used to enforce the access boundaries defined by the Standard User and Elevated Administrative account models described above.
In addition to controlling what remote devices can access, Tailscale ACLs are configured to prevent homelab servers from initiating connections to remote Tailnet devices.

This ensures that administrative access remains user-initiated and helps reduce the risk of lateral movement from infrastructure systems to trusted remote devices.

## Security Considerations

### Strengths

- Separate Standard User and Elevated Administrative accounts enforce a least-privilege access model.
- The Standard User account provides Pi-hole DNS filtering and optional exit-node access without granting access to internal infrastructure.
- Administrative access is isolated to a dedicated Elevated Administrative account, reducing unnecessary exposure of homelab resources to daily-use devices.
- Access to the Trusted VLAN is intentionally denied for administrative sessions, helping maintain separation between infrastructure services and personal devices.
- Remote access to homelab resources is provided through Tailscale, eliminating the need to expose management interfaces directly to the public internet.
- Pi-hole DNS filtering can be applied to trusted devices when away from home, providing a consistent security and privacy experience.
- Tailscale device authorization and multi-factor authentication provide additional protection against unauthorized access.
- Tailscale ACLs prevent homelab servers from initiating connections to remote Tailnet devices, reducing the risk of lateral movement from infrastructure systems to trusted user devices.
  
### Risks and Limitations

- A compromised device authenticated with the Elevated Administrative account will have access to internal services on the server VLAN.
- Security of remote access depends on the protection of Tailscale accounts, authentication methods, and enrolled devices.
- Availability of remote access is dependent on Tailscale services.
- Incorrectly configured ACL policies may result in unintended access to internal resources or prevent legitimate administrative workflows.
