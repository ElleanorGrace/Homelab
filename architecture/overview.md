# Homelab Architecture Overview 
## Goals 
This homelab was created to support several self-hosted services while providing a practical environment for developing technical skills in systems administration, networking, infrastructure management, and containerized application deployment.
### Primary Services
- A Tailscale mesh VPN used to protect network traffic on mobile and laptop devices while connected to public Wi‑Fi and other untrusted networks and securely access internal services remotely.
- A Pi-hole DNS server providing network-wide ad and tracker blocking.
- A Kali Linux virtual machine used for cybersecurity training, security tool familiarization, network analysis, and controlled security testing within the homelab environment.
- An Emby-based media platform supported by the Arr suite for content discovery and media management automation.
- A Foundry Virtual Tabletop (Foundry VTT) deployment used to facilitate online tabletop role-playing games (TTRPGs).
- Dedicated game servers hosted and managed through Pterodactyl Panel.
### Technical Objectives
- Develop practical experience deploying and managing Docker containers and supporting application services.
- Learn Linux system administration and day-to-day server operations.
- Implement and manage reverse proxy and ingress solutions using Nginx Proxy Manager.
- Configure and manage DNS, TLS certificates, and secure remote access through Cloudflare and Tailscale.
- Develop familiarity with database administration through the deployment and maintenance of MariaDB and Redis.
- Gain experience administering network services, including DNS filtering and network management platforms.
- Develop familiarity with common cybersecurity tools, vulnerability assessment techniques, and network analysis workflows in a controlled lab environment.
- Develop troubleshooting, maintenance, and operational documentation practices.
- Apply security concepts such as encrypted communications, centralized ingress control, and layered defense.

## Technology Stack

### Infrastructure & Networking

- Unraid
- UniFi Controller
- Docker
- Nginx Proxy Manager
- Tailscale
- Pi-hole


### Application Hosting & Data Services

- MariaDB
- Redis
- Adminer

### Media Platform

- Emby
- Sonarr
- Radarr
- Bazarr
- Prowlarr
- Deluge

### Gaming & Community Services

- Foundry Virtual Tabletop (Foundry VTT)
- Pterodactyl Panel
