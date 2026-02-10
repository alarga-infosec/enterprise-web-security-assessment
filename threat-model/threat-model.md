# Threat Model

## Overview
This threat model identifies realistic threats against a simulated enterprise
telecom web application, focusing on abuse scenarios relevant to large-scale environments.

## Threat Actors
- External attacker
- Authenticated malicious user
- Compromised CSR account
- Insider with excessive privileges

## Attack Surfaces
- Public-facing web application
- Authentication and session management
- Authorization logic and role separation
- Backend API endpoints
- CSR/admin management interface

## Key Assets
- Customer personal data (PII)
- Billing and subscription information
- User and CSR account integrity
- Audit logs and security events

## STRIDE Analysis
| Threat | Example |
|------|--------|
| Spoofing | Session hijacking or token reuse |
| Tampering | Unauthorized modification of customer data |
| Repudiation | Insufficient logging of CSR actions |
| Information Disclosure | IDOR exposing other users’ data |
| Denial of Service | Rate limit bypass leading to service degradation |
| Elevation of Privilege | User gaining CSR-level access |
