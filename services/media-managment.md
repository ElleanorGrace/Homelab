# Media Management

## Overview

Media Management consists of the supporting services responsible for media discovery, acquisition, organization, and library maintenance within the homelab environment.

These services operate behind the scenes to maintain media libraries that are ultimately consumed through Emby. Documentation related to media streaming, user access, and media consumption is maintained separately in emby.md.

## Objectives

- Automate media acquisition workflows.
- Reduce manual media organization tasks.
- Maintain consistent file naming and library structure.

## Core Services

The media management platform consists of several specialized applications that work together to automate media workflows.

### Sonarr

Purpose:

- Television series management and automation.

Capabilities:

- Monitor series for new episodes.
- Automatically import downloaded content.

### Radarr

Purpose:

- Movie management and automation.

Capabilities:

- Monitor movie collections.
- Automate movie acquisition workflows.

### Prowlarr

Purpose:

- Centralized indexer management.

Capabilities:

- Manage indexer configuration from a single interface.
- Synchronize indexers across supported applications.
- Simplify administration of media acquisition services.

### Download Clients

Purpose:

- Retrieve requested content for processing and library import.

Capabilities:

- Download content requested by media management services.
- Integrate with automated import workflows.
- Transfer completed downloads to managed media libraries.


## Workflow

Media management services follow an automated workflow:

1. A request is submitted through a media management application.
2. Prowlarr provides configured indexer information.
3. A supported download client retrieves the requested content.
4. Sonarr or Radarr processes and organizes completed downloads.
5. Content is moved into the appropriate media library.
6. Emby detects and makes the media available to users.

## Security Considerations

### Strengths

- Centralized administration simplifies maintenance.
- Containerized deployments help isolate services from one another.
- Integration between applications reduces manual intervention.
- Nothing is exposed to the public internet.

### Risks and Limitations

- Service availability depends on the availability of the Unraid host.
- Misconfigured automation rules may result in incorrect downloads or library organization.
- Media acquisition services often require access to external sources that may change or become unavailable.
- Storage capacity limitations can affect long-term library growth.
- Failure of supporting services may interrupt automated workflows.
