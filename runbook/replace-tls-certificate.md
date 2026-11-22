# Replace Cloudflare Origin Certificate

## Purpose

This runbook documents the process for replacing a Cloudflare Origin Certificate used by Nginx Proxy Manager.

Use this procedure when:

- An origin certificate is approaching expiration.
- A certificate has been revoked.
- Private key material is suspected to be compromised.
- TLS validation errors occur between Cloudflare and the origin server.

## Preparation

Before beginning:

- Verify administrative access to Cloudflare.
- Verify administrative access to Nginx Proxy Manager.
- Identify all proxy hosts currently using the certificate.

## Generate New Cloudflare Origin Certificate

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

## Import New Certificate into Nginx Proxy Manager

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

## Delete old Certificate

1. Navigate to SSL Certificates tab.
2. Select old certificate and select delete

## Validation

Verify the following:

### Browser Validation

- HTTPS loads successfully.
- No browser certificate warnings are displayed.
- Service redirects function as expected.

### Cloudflare Validation

- SSL/TLS Mode is set to Full (Strict).
- DNS records remain proxied through Cloudflare.

### Origin Validation

- Nginx Proxy Manager shows the imported certificate as valid and not expired.
- Proxy hosts are using the correct certificate.
- Services are reachable through Cloudflare.


## Related Documentation
- [deployment/tls-certificate-setup.md](../deployment/tls-certificate-setup.md)
- [architecture/tls-and-certificate-management.md](../architecture/tls-and-certificate-management.md)
