# email-security-setup
Documenting my hands-on setup of modern email authentication and DNS security standards for my domain, using Microsoft 365 + Cloudflare DNS.

## Records Implemented
- SPF → TXT @ : `v=spf1 include:spf.protection.outlook.com -all`
- DKIM → CNAMEs for selector1 + selector2 (enabled in Microsoft 365)
- DMARC → TXT _dmarc : `v=DMARC1; p=quarantine; rua=mailto:reports@4teamhuman.org`
- MTA-STS → TXT _mta-sts : `v=STSv1; id=2025-09-11`
- TLS-RPT → TXT _smtp._tls : `v=TLSRPTv1; rua=mailto:reports@4teamhuman.org`

## Validation
- Gmail “Show original” → SPF/DKIM/DMARC: **PASS**
- MXToolbox lookups → all DNS records resolve correctly
- HTTPS → MTA-STS policy accessible at `https://mta-sts.4teamhuman.org/.well-known/mta-sts.txt`

## Lessons Learned
- How SPF, DKIM, and DMARC align to block spoofing
- How MTA-STS + TLS-RPT enforce encrypted delivery and provide visibility
- Practical use of Cloudflare DNS with Microsoft 365 mail flow
