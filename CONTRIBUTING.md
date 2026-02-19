# Contributing to the Bonafide Specification

Thank you for your interest in improving Bonafide. This document explains how to participate in the specification's development, what kinds of contributions are welcome, and how the process works at each governance phase.

---

## Current Governance Phase

Bonafide is in **Phase 1 — Stewardship**. Sly Technologies develops and publishes the specification with community input. Substantive changes go through a comment period before adoption. This phase prioritizes coherence and velocity while building the contributor base needed for Phase 2.

---

## Types of Contributions

### Bug Reports and Clarifications

If you find an error, ambiguity, inconsistency, or gap in the specification:

1. Check [existing issues](https://github.com/bonafide-id/bonafide-spec/issues) to avoid duplicates.
2. Open a new issue with a clear title and description.
3. Reference the specific part, section, and page number (e.g., "Part 12, Section 4.3, page 9").
4. Describe what the spec says, what you believe it should say, and why.

### Minor Corrections

Typos, formatting errors, broken cross-references, and minor wording improvements can be submitted as pull requests directly against the `docx/` source files. No RFC required.

### Substantive Changes

Changes that alter the specification's technical content — new mechanisms, modified protocols, changed security properties, additional requirements — require the RFC process described below.

### Diagrams

Architecture diagrams, flow charts, and visual aids are welcome. Submit SVGs to the `diagrams/` directory. Diagrams should be clean, monochrome-friendly, and use labels consistent with specification terminology.

### Regulatory and Jurisdictional Input

Part 13 (Compliance Profiles & Global Deployment) benefits from jurisdiction-specific expertise. If you have knowledge of a regulatory framework not yet mapped, or if an existing mapping is inaccurate, open an issue or submit an RFC with the correction and supporting legal references.

---

## RFC Process

### When an RFC Is Required

An RFC is required for any change that:

- Adds, removes, or modifies a cryptographic mechanism
- Changes the key architecture or derivation model
- Adds or removes a participation model (vault holder, institution, validator, etc.)
- Modifies the privacy classification definitions or audit methodology
- Changes the third-party access protocol
- Adds or removes a compliance profile
- Alters the security level system or enclave tier requirements
- Modifies the governance model or transition criteria

### RFC Format

Create a new file in `rfcs/` using the naming convention `NNNN-short-title.md` where `NNNN` is the next available number. Use `rfcs/0000-template.md` as the starting point.

An RFC must include:

- **Title** — concise description of the change
- **Author(s)** — name and contact
- **Status** — Draft, Comment, Accepted, Rejected, or Withdrawn
- **Affected Parts** — which specification parts are modified
- **Summary** — one paragraph describing the change and its motivation
- **Problem Statement** — what the current spec gets wrong or doesn't address
- **Proposed Change** — precise description of what changes, including specific section references
- **Security Analysis** — how the change affects the specification's security properties, including any new attack surfaces or mitigations
- **Compatibility** — whether existing deployments need to change and how migration works
- **Alternatives Considered** — other approaches and why they were rejected

### RFC Lifecycle

**Phase 1 (current):**

1. Author submits RFC as a pull request.
2. Sly Technologies reviews for completeness and assigns a tracking number.
3. RFC enters a 30-day community comment period. Comments are submitted as PR reviews or linked issues.
4. Sly Technologies evaluates the RFC and community feedback.
5. Decision: Accepted (merged and scheduled for next spec version), Rejected (with written rationale), or Revision Requested (author revises and resubmits).

**Phase 2 (Foundation):**

1. Author submits RFC as a pull request.
2. Foundation technical committee reviews for completeness.
3. 60-day community comment period.
4. Technical committee recommendation to the governing board.
5. Board vote. Sly Technologies retains transitional veto on changes that compromise security architecture.

**Phase 3 (Community):**

1. Author submits RFC as a pull request.
2. 60-day community comment period.
3. Community vote. Security-critical changes require two-thirds supermajority. No single entity holds veto power.

---

## Specification Boundary

The following boundary is permanent and not subject to RFC modification. Changes in this category will be rejected regardless of process:

- **No master keys.** The specification will never include a key that decrypts all or a broad category of vault data.
- **No bulk access.** The specification will never include a mechanism for accessing data across multiple users in a single operation.
- **No content scanning.** The specification will never include content inspection, filtering, or classification by vault infrastructure.
- **No silent access.** The specification will never include access that is not recorded in the immutable ledger and eventually visible to the data owner.
- **No backdoors.** The specification will never include capabilities that bypass the three-path key architecture.

These boundaries define the specification's identity. They exist to protect the global user base from pressure applied in any single jurisdiction or by any single entity, including Sly Technologies.

---

## Working with the Source Files

### File Formats

- **Canonical format:** PDF files in `spec/` are the authoritative specification. These are what people cite and link to.
- **Source format:** DOCX files in `docx/` are the editable source. Pull requests that modify specification content should target these files.
- **Diagrams:** SVG files in `diagrams/`. Use a vector editor (Inkscape, Illustrator, Figma) and ensure text is legible at standard zoom.

### Branching

- `main` — current released specification version
- `dev` — work in progress for next version
- `rfc/NNNN-short-title` — branches for active RFCs

### Pull Request Guidelines

- One logical change per PR. Don't bundle unrelated fixes.
- Reference the issue or RFC number in the PR description.
- For spec content changes, describe which parts and sections are affected.
- For cross-cutting changes (terminology, formatting), list all affected files.
- Ensure DOCX files open correctly in Microsoft Word and LibreOffice.

---

## Style Guide

### Terminology

Use specification terminology consistently:

| Term | Usage |
|------|-------|
| Quantum (plural: quanta) | The atomic data unit. Not "record," "entry," or "item." |
| Bio Root | The cryptographic root derived from biometric + root_secret + passphrase. Two words, both capitalized. |
| Root secret | The user-chosen gesture-derived hash stored in the device enclave. Lowercase. |
| DEK | Data Encryption Key. Always abbreviated after first use in a section. |
| Ghost quantum | A privacy-preserving derived representation. Not "ghost data" or "phantom." |
| Vault holder | A device that computes Bio Root and performs vault operations. Two words. |
| Peering | The process of establishing a user-institution relationship. Not "linking" or "connecting." |
| Third-party key | Purpose-specific key generated by the Bonafide API. Always hyphenated. |
| Privacy classification | The S/A/B/C/U grade. Not "privacy level" (which could be confused with security level). |
| Security level | The extensible unsigned integer determining key depth and enclave requirements. Not "security tier." |
| Enclave tier | The hardware security tier (S, 1, 2, 3, 4). Not "enclave level." |

### Writing Style

- Write in present tense and active voice.
- Be precise. "The runtime derives the DEK" not "the DEK gets derived."
- Define acronyms on first use in each part.
- Use "the specification" not "this document" when referring to Bonafide as a whole.
- Use "the user" not "the customer" or "the data subject."
- State what the system does, then why. Architecture first, rationale second.

### Cross-References

Reference other parts by number and section: "the third-party access protocol (Part 12, Section 4)" not "as described elsewhere." Every cross-reference should be specific enough that a reader can find it without searching.

---

## Code of Conduct

Contributors are expected to engage respectfully and constructively. The specification addresses sensitive topics (surveillance, coercion, duress, government access) where reasonable people disagree. Contributions should be technically grounded and argue from security properties, not political positions.

- Critique ideas, not people.
- Assume good faith.
- Back claims with technical analysis or regulatory citations.
- Acknowledge when you're uncertain.

Sly Technologies reserves the right to moderate discussions and remove contributions that violate these principles.

---

## Recognition

All accepted RFC authors are credited in the specification's changelog. Significant contributors are acknowledged in the specification's front matter beginning with the Phase 2 Foundation transition.

---

## Questions

If you're unsure whether a contribution needs an RFC, or which part of the specification your feedback applies to, open a [Discussion](https://github.com/bonafide-id/bonafide-spec/discussions) and ask. We'd rather help you contribute effectively than have good ideas get lost in process.

---

<p align="center">
  <strong>Bonafide™ — Privacy by architecture, not by promise.</strong>
</p>
