# TLS and Certificate Management

## Purpose

TLS (Transport Layer Security) is used throughout the homelab to provide encrypted communications between clients, Cloudflare, and services published through Nginx Proxy Manager.

The objectives of this implementation are:

- Encrypt all internet-facing traffic.
- Protect network communications from interception or tampering while in transit.
- Centralize HTTPS configuration and routing through Nginx Proxy Manager.
- Simplify certificate lifecycle management through Cloudflare-managed public certificates and Cloudflare Origin Certificates.
- Improve the security posture of internet-facing services through the use of Cloudflare proxy services and TLS encryption.
## TLS Architecture

```text
User
  │
  ▼
Cloudflare Public Certificate
  │
  ▼
Cloudflare Proxy
  │
  ▼
Cloudflare Origin Certificate
  │
  ▼
Nginx Proxy Manager
  │
  ▼
Services
```

### Public TLS

Cloudflare provides publicly trusted TLS certificates presented to end users accessing services through proxied DNS records.

Benefits include:

- Automatic certificate management.
- Publicly trusted certificate chain.
- No browser trust warnings for end users.

### Cloudflare Proxy

All publicly accessible services are published through proxied Cloudflare DNS records, allowing Cloudflare to act as the intermediary between clients and the homelab.

Benefits include:

- Conceals the origin server from direct public access.
- Integrates with Cloudflare security features such as traffic filtering, DDoS protection, and Web Application Firewall (WAF) capabilities.
  
### Origin TLS

Traffic between Cloudflare and the homelab uses a Cloudflare Origin Certificate installed in Nginx Proxy Manager.

Benefits include:
- Encrypts traffic between Cloudflare and the homelab origin server.
- Integrates directly with Nginx Proxy Manager without requiring additional certificate management applications.
- Long certificate lifetime significantly reduces maintenance requirements compared to frequently renewed public certificates.

### Design Rationale

This architecture was selected to simplify certificate management, improve the security of internet-facing services, and reduce operational overhead. Cloudflare manages public-facing TLS certificates, acts as the ingress point for externally accessible services, and provides security features such as DDoS mitigation and traffic filtering. A Cloudflare Origin Certificate maintains encrypted communications between Cloudflare and the homelab while eliminating the need for separate certificate automation tooling and frequent certificate renewals.

## Nginx Proxy Manager Integration

Nginx Proxy Manager acts as the TLS termination point for the homelab. It presents the Cloudflare Origin Certificate, handles HTTPS connections from Cloudflare, and routes requests to the appropriate backend services.

Responsibilities:

- Certificate presentation to Cloudflare
- HTTPS termination
- Reverse proxy routing


## Security Considerations
### Strengths
- Public-facing TLS certificates are managed by Cloudflare, reducing the risk of certificate expiration or misconfiguration.
- Cloudflare acts as the public ingress point for internet-facing services, providing additional protections such as DDoS mitigation, traffic filtering, and Web Application Firewall (WAF) capabilities.
- Cloudflare is configured to use Full (Strict) SSL/TLS validation, ensuring origin certificates are validated before connections are established.
- Traffic between Cloudflare and the homelab is encrypted using a Cloudflare Origin Certificate.
- Centralized ingress through Nginx Proxy Manager simplifies access management and reduces the number of directly exposed services.

### Risks and Limitations
- External access to public services is dependent on Cloudflare availability and configuration.
- Misconfiguration of Cloudflare SSL/TLS settings may reduce certificate validation or weaken the intended security posture.
- The long lifetime of Cloudflare Origin Certificates reduces maintenance requirements but increases the importance of protecting private key material.
- Security controls provided by Cloudflare do not replace the need for proper access controls, system hardening, monitoring, and regular maintenance within the homelab environment.
