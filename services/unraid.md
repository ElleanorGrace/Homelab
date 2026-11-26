# Unraid

## Overview

Unraid functions as the foundation for the homelab and hosts the entirety of self-managed services.

## Objectives

- Host applications, containers, and supporting infrastructure.
- Provide Network attached storage for devices
- Simplify system administration and maintenance.
- Support future growth of the homelab environment.

## Core Services

### Storage

Capabilities:

- Network-accessible file shares
- Protection against single-drive failure through parity.

### Application Hosting

Capabilities:

- Supports containerized workloads through Docker.
- Supports virtual machines.
- Provides centralized application management through a web interface.

### Management

Capabilities:

- Centralized administration of storage and hosted services.
- Monitoring of system health and resource utilization.
- Management of user shares and storage allocation.

## Security Considerations

### Strengths

- Supports containerization, helping isolate applications from one another.
- Administrative interfaces can remain inaccessible from the public internet.
- Provides parity protection against single-drive failure.
- Consolidates monitoring, management, and maintenance activities.

### Risks and Limitations

- Unraid represents a central point of failure for hosted services and stored data.
- A compromise of the Unraid host may impact multiple applications and services.
- Parity protection does not replace a dedicated backup strategy.
- Availability of dependent services is directly tied to the availability of the Unraid host.
