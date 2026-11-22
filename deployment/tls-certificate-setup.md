# TLS Certificate Setup
## Purpose

This document describes the deployment and configuration of the TLS architecture used by the homelab.

The solution utilizes:

- Cloudflare Public TLS Certificates
- Cloudflare Proxy Services
- Cloudflare Origin Certificates
- Nginx Proxy Manager

This implementation provides encrypted communications between internet clients, Cloudflare, and services hosted within the homelab while minimizing certificate management overhead.

## Prerequisites

Before beginning, verify the following:

- Domain is registered and managed through Cloudflare.
- DNS records have been created for the desired services.
- Cloudflare proxying is enabled for public services.
- Nginx Proxy Manager is installed and operational.
- Administrative access to both Cloudflare and Nginx Proxy Manager is available.

## Generate Cloudflare Origin Certificate

1. Log in to the [Cloudflare Dashboard](https://dash.cloudflare.com).
2. Select the desired domain.
3. Create the origin certificate:

   ```text
   SSL/TLS -> Origin Server
   
   Create Certificate


   Private Key Type:
   RSA (2048-bit)


   Hostnames:
   *.example.com
   example.com

   Select the desired certificate validity period.
   ```

4. Save the following securely:

   - Origin Certificate
   - Private Key

## Configure Cloudflare SSL/TLS Mode

1. Navigate to:

   ```text
   SSL/TLS -> Overview
   ```

2. Select:

   ```text
   Full (Strict)
   ```

This setting validates the origin certificate before Cloudflare establishes connections to the homelab.

## Import Certificate into Nginx Proxy Manager

1. Log in to Nginx Proxy Manager.
2. Upload the certificate:

   ```text
   SSL Certificates tab
   Add SSL Certificate -> Custom

   Upload:
   - Origin Certificate
   - Private Key
   ```
3. Save the certificate.

## Assign Certificate to Proxy Hosts

For each service:

1. Kebab menu ⁝ -> Edit.
2. Change to SSL tab:
3. Select the imported certificate.
4. Save changes.

## Validation

Verify the following:

### Browser Validation

- HTTPS loads successfully.
- No browser certificate warnings are displayed.
- Service redirects function as expected.

### Cloudflare Validation

Confirm SSL/TLS Mode: Full (Strict)

### Origin Validation

- Nginx Proxy Manager shows the imported certificate as valid and not expired.
- Proxy hosts are using the correct certificate.
- Services are reachable through Cloudflare.

## Related Documentation
- [architecture/tls-and-certificate-management.md](architecture/tls-and-certificate-management.md)
