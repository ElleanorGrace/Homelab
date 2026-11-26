# Pi-hole

## Overview

Pi-hole provides network-wide DNS filtering, advertisement blocking, and tracker protection for devices connected to the homelab. It serves as the primary DNS resolver for trusted devices and integrates with Tailscale to extend DNS filtering when away from home.

## Objectives

- Provide network-wide advertisement and tracker blocking.
- Improve privacy by preventing communication with known tracking domains.
- Centralize DNS management for homelab devices.
- Extend DNS filtering to trusted remote devices through Tailscale.

## DNS Services

Pi-hole functions as the primary DNS resolver for supported devices on the network.

### Local Network

Capabilities:

- Network-wide advertisement blocking.
- Tracker and telemetry domain filtering.
- Centralized DNS logging and visibility.
- Custom DNS records for internal services.

## Security Considerations

### Strengths

- Blocks known advertising, tracking, and malicious domains before connections are established.
- Supports custom DNS records for internal service discovery without exposing those services publicly.

### Risks and Limitations

- DNS filtering is not a substitute for endpoint security, safe browsing practices, or network segmentation.
- False positives may occasionally block legitimate services and require manual review.
- Availability of DNS services depends on the Pi-hole host remaining operational.
