# Bonafide™ Specification

**User-Sovereign Encrypted Data Vault Architecture**

An open specification for quantized, encrypted, privacy-first data sovereignty.

---

## What Is Bonafide?

Bonafide is an open specification that replaces the broken trust model of centralized data storage with user-sovereign encrypted vaults. Instead of trusting institutions to protect your data behind their walls, Bonafide encrypts every piece of personal data independently, gives users the only master keys, and distributes encrypted fragments across institutions — with each institution able to see only what the user has authorized.

**No passwords.** Authentication is passwordless multi-factor: biometric processed on-device within a hardware secure element, combined with a user-chosen root secret stored in the device enclave. The derivation is stateless — there is no stored "correct answer," no error on failure, no oracle for an attacker to probe.

**No centralized honeypots.** Data is decomposed into atomic units (quanta) that are independently encrypted. Compromise of one reveals nothing about any other. Breaching an institution's network yields only ciphertext.

**No backdoors.** Lawful access works through scoped, audited, purpose-specific mechanisms — not master keys or content scanning.

---

## Whitepaper

| Document | Pages | Description |
|----------|-------|-------------|
| [Architectural Whitepaper](whitepaper/Bonafide-Whitepaper-V1.0.pdf) | 17 | Executive overview of the full architecture, suitable for technical and non-technical audiences |

---

## Specification V1.0

The specification is organized into 13 parts. Each part is self-contained with its own section numbering.

| Part | Title | Pages | Scope |
|------|-------|-------|-------|
| [Part 1](spec/BF-V1-Part-01-Foundation.pdf) | Foundation & Core Architecture | 11 | Vault hierarchy, quantum model, design principles, participation models, security levels, ledger |
| [Part 2](spec/BF-V1-Part-02-Cryptographic-Foundation.pdf) | Cryptographic Foundation | 10 | Composable root derivation, gesture system, biometric processing, key hierarchy, encryption, Merkle integrity |
| [Part 3](spec/BF-V1-Part-03-Security-Authentication.pdf) | Security Levels & Authentication | 11 | Level system, MFA compliance mapping, auth flows, elevation, session management, duress |
| [Part 4](spec/BF-V1-Part-04-PII-Protection.pdf) | PII Protection & Privacy | 10 | Proxy identity, privacy scoring, canary detection, watermarking, data minimization, erasure, portability |
| [Part 5](spec/BF-V1-Part-05-Blind-Validation.pdf) | Blind Validation Network | 9 | ZK proof system, trust scoring, validator selection, BFT consensus, Sybil resistance |
| [Part 6](spec/BF-V1-Part-06-Infrastructure.pdf) | Infrastructure & Portfolio | 8 | Database packages, cloud coordination, ExaScale integration, namespace, products, revenue |
| [Part 7](spec/BF-V1-Part-07-Personas-Identity.pdf) | Personas & Identity | 8 | Multi-persona architecture, duress protection, focus profiles, content neutrality, persona lifecycle |
| [Part 8](spec/BF-V1-Part-08-Ecosystem-Governance.pdf) | Open Ecosystem & Governance | 7 | Ecosystem philosophy, federated relay, certification program, governance evolution, adoption strategy |
| [Part 9](spec/BF-V1-Part-09-Network-Security.pdf) | Network Security & Abuse Prevention | 12 | Threat model, transport security, DoS defense, validator protection, traffic analysis resistance |
| [Part 10](spec/BF-V1-Part-10-Enclave-Devices.pdf) | Enclave Architecture & Device Classes | 11 | Enclave tiers, device profiles, peripherals, biometric input, server hardware, cross-device sync |
| [Part 11](spec/BF-V1-Part-11-Privacy-Classifications.pdf) | Privacy Classifications | 10 | S/A/B/C/U definitions, audit methodology, upgrade path, score integration |
| [Part 12](spec/BF-V1-Part-12-Institutional-Runtime.pdf) | Institutional Runtime & Data Governance | 16 | Runtime architecture, three-path keys, third-party access framework, revocation, anti-duplication, HAL |
| [Part 13](spec/BF-V1-Part-13-Compliance-Profiles.pdf) | Compliance Profiles & Global Deployment | 11 | Open/Regulated profiles, market tiers, regulatory mapping, data residency, compliance evolution |

**Total: 134 pages across 13 parts**

---

## Core Architecture at a Glance

### Three-Path Key Separation

Every quantum's encryption key (DEK) is wrapped independently for each authorized key path:

- **User key** — Sovereign. Derived from the user's Bio Root. Only the user holds it. Works across all institutions.
- **Institutional key** — Sacrosanct. Licensed exclusively for user-authorized operations. Cannot serve third-party access. The institution literally cannot use its key to comply with a warrant — the protocol doesn't allow it.
- **Third-party key** — Purpose-specific. Generated on demand for sharing, verification, legal access, or emergency. Scoped, time-bounded, recipient-bound, and derived from the authorization that created it.

### Third-Party Access Categories

| Category | Authorization | Key Lifetime | Data Exposure |
|----------|--------------|--------------|---------------|
| User sharing | User's explicit action | Minutes to permanent | User's choice |
| Institutional verification | User pre-authorization rules | Seconds to minutes | Ghost quanta (default) |
| Legal / audit | Validated legal instrument | Days to months | Per instrument |
| Emergency | Pre-configured profile | Hours | Medical/identity only |

### Privacy Classifications

| Grade | Key Isolation | Hardware | Revocation |
|-------|--------------|----------|------------|
| **S** — Sovereign | FPGA fabric / PUF | Dedicated FPGA or SE | Absolute |
| **A** — Attested | Hardware TEE | TEE-capable CPU or DPU | Effective |
| **B** — Bounded | Software process | Optional HSM/TPM | Operational |
| **C** — Compliant | Runtime only | None required | Partial |
| **U** — Unclassified | Not audited | Not verified | Unknown |

### Passwordless Multi-Factor Authentication

```
Bio Root = Hash( biometric || root_secret_hash || manual_passphrase )
```

- **Biometric** (inherence) — multi-modal, on-device, in hardware secure element
- **Device + root secret** (possession) — attested enclave with stored root_secret_hash
- **Passphrase** (knowledge) — optional, selects alternate personas

Exceeds NIST 800-63 AAL3, PSD2 SCA, FIDO2/WebAuthn, HIPAA, and PCI-DSS v4.0.

---

## Compliance

Bonafide maps to 13 regulatory frameworks:

GDPR (Articles 5, 17, 20, 25, 32) · CCPA · HIPAA · PCI-DSS v4.0 · PSD2 SCA · NIST 800-63 AAL2/AAL3 · FIDO2/WebAuthn · eIDAS 2.0

See [Part 13](spec/BF-V1-Part-13-Compliance-Profiles.pdf) for the full mapping.

---

## Related Repositories

This repository contains the specification documents only. Implementation repositories in the [bonafide-id](https://github.com/bonafide-id) organization:

| Repository | Description |
|------------|-------------|
| `bonafide-core` | Reference implementation of vault protocol, key derivation, ledger, validation client |
| `bonafide-db-postgres` | PostgreSQL database package with transparent per-quantum encryption |
| `bonafide-db-oracle` | Oracle database package |
| `bonafide-db-sqlserver` | SQL Server database package |
| `bonafide-db-mysql` | MySQL database package |
| `bonafide-db-mongodb` | MongoDB database package |
| `bonafide-sdk-*` | Developer SDKs (JavaScript, Java, Python, Swift, Kotlin, Rust, Go, C) |
| `bonafide-gateway` | API gateway with tiered authentication |
| `bonafide-validator` | Reference validator node implementation |
| `bonafide-relay` | Reference relay operator implementation |
| `bonafide-cert` | Certification test suites |
| `bonafide-personal` | Consumer vault application |

---

## Repository Structure

```
bonafide-spec/
├── whitepaper/          # Architectural whitepaper (PDF)
├── spec/                # Specification parts 1–13 (PDF, canonical)
├── docx/                # Source .docx files (for contributors)
├── diagrams/            # Architecture diagrams (SVG)
├── rfcs/                # Specification change proposals
└── versions/            # Archived prior versions
```

---

## Contributing

Bonafide is currently in **Phase 1 (Stewardship)** — Sly Technologies develops the specification with community input.

- **Report issues:** Open a GitHub issue for errors, ambiguities, or gaps in the specification.
- **Propose changes:** For substantive changes, open a discussion first. If consensus forms, submit an RFC in the `rfcs/` directory following the template.
- **Minor corrections:** Typos, formatting, and clarifications can be submitted as pull requests directly.

See [CONTRIBUTING.md](CONTRIBUTING.md) for details.

---

## Governance

| Phase | Status | Decision Model |
|-------|--------|----------------|
| **Phase 1 — Stewardship** | **Current** | Sly Technologies publishes updates with 30-day community comment |
| Phase 2 — Foundation | Pending | Independent Foundation with governing board; Sly Technologies retains transitional veto |
| Phase 3 — Community | Pending | Full RFC process with community vote; no single-entity veto |

Transition criteria are defined in [Part 8, Section 6](spec/BF-V1-Part-08-Ecosystem-Governance.pdf).

---

## License

The Bonafide specification is released under [CC BY-SA 4.0](LICENSE). You are free to share and adapt the specification for any purpose, including commercial use, provided you give appropriate credit and distribute derivative works under the same license.

The specification is free. Reference implementations are open source. No one pays to implement the protocol.

---

## Contact

- **Web:** [bonafide.id](https://bonafide.id)
- **Specification & Governance:** [bonafideid.org](https://bonafideid.org)
- **Organization:** [github.com/bonafide-id](https://github.com/bonafide-id)
- **Developed by:** [Sly Technologies Inc.](https://slytechs.com)

---

<p align="center">
  <strong>Bonafide™ — Privacy by architecture, not by promise.</strong><br>
  <em>Your Data. Your Keys. Your Vault.</em>
</p>
