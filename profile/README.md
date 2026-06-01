# 0trust

"Have zero trust in closed source; have zero trust security in open source."

## Overview

0trust is an Open-Core ZTNA (Zero Trust Network Access), log management, and IdP (Identity Provider) platform designed to provide a secure, scalable architecture.

## Split-Plane Tech Stack

The platform utilizes a two-tier architecture to manage security and data:

* **0trust.cloud (Control Plane)**: An administrative portal, SSO dashboard, and compliance audit vault.
* **0trust.services (Data Plane)**: A distributed mesh client deployed as an edge proxy.This provides the ingress for downsteam OIDC/SAML apps and upstream telementry for ingesting.
  
### Core Components

* **ultimate_db**: Custom transaction engine with fixed 32KB pages and optimistic concurrency control (no locking).
* **ELK-like Stack**: A native observability pipeline capturing logs and metrics using BM25 sharding across peer networks for unstructured logs.
* **auth_provider**: Manages WebAuthn handshakes and live tail telemetry over WebSocket streams.
* **identity_provider**: Manages OIDC/SAML authentication along with provisioning of users.
* **secure_policy**: Creates ABAC/RBAC policies for services.
* **secure_bootstrap**: Provisions cryptographically validated edge identities via TPM 2.0 or FIDO hardware.
* **secure_network**: High-throughput QUIC tunnel mesh that completely bypasses standard public routing paths.
* **Data-in-Transit**: Zero-configuration default encryption using custom cryptographic frames.

## Security & Compliance

0trust is engineered to meet rigorous security standards out of the box:

* **Perimeter Security**: Routing all network ingress through the `secure_network` overlay closes public perimeters and eliminates open internet ports.
* **Safe Transmission**: Dynamic edge connections use native frames over authenticated QUIC tunnels, removing packet-sniffing vulnerabilities.
* **Security Monitoring**: Immutable logs are natively captured down to the disk storage level via `ultimate_db` upon any security event or policy evaluation.

---

*Open-source core available at [https://0Trust.codes](https://0Trust.codes).*
