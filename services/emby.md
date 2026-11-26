# Emby

## Overview

Emby is the primary media streaming platform within the homelab. It provides access to movies and television shows.

Documentation related to media acquisition, library management, and supporting automation services is maintained separately in media-management.md.

## Objectives

- Support media streaming to devices.
- Enable secure remote access.
- Integrate with supporting services that manage media organization and availability.

## Media Access

Emby serves as the primary interface for consuming media hosted within the homelab environment.

Capabilities:

- Stream media to supported devices.
- Organize content into centralized libraries.
- Maintain watch history and playback progress.
- Support multiple user profiles.
- Provide access to media stored on the Unraid server.
- Administrative login is restricted to internal access only

## Security Considerations

### Strengths

- Administrative interfaces locked behind local only accounts.
- User access can be restricted through application-level permissions.
- Media libraries are centrally managed.

### Risks and Limitations

- Availability of media services depends on the availability of the Unraid host.
- Misconfigured network access controls may expose media services to unintended devices.
- Service availability is dependent on the underlying storage infrastructure remaining operational.
