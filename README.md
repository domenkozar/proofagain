# ProofAgain

> **Prove who you are. Recover what is yours.**

ProofAgain is a startup concept for identity-gated recovery infrastructure. It is intended to help people recover small, critical digital recovery objects after every ordinary authenticator, device, and backup method has been lost.

Applications encrypt recovery objects on the user's device and deposit them with one or more recovery providers. A claimant must later complete high-assurance identity verification, risk review, notifications, and a waiting period before providers release encrypted recovery capability to a newly generated device key. In the target architecture, plaintext recovery material appears only on the recovering user's device.

ProofAgain does not replace authentication, store ordinary passwords, or make identity verification infallible. It is the final recovery layer for catastrophic lockout.

## Proposal documents

The documents are ordered for a first read, but each can stand on its own.

| Document | Purpose | Primary audience |
| --- | --- | --- |
| [00 — Executive proposal](docs/00-executive-proposal.md) | One-page view of the company, product, wedge, and investment thesis | Investors, partners, recruits |
| [01 — Problem and opportunity](docs/01-problem-and-opportunity.md) | Customer pain, alternatives, market thesis, and validation needs | Product, investors |
| [02 — Product and experience](docs/02-product-and-experience.md) | Users, workflows, MVP scope, and product requirements | Product, design, engineering |
| [03 — Technical architecture](docs/03-technical-architecture.md) | System components, cryptographic flows, trust boundaries, and evolution | Engineering, security reviewers |
| [04 — Identity, security, and privacy](docs/04-identity-security-privacy.md) | Identity model, assurance policy, threat model, safety controls, and data minimization | Security, risk, privacy |
| [05 — Protocol and integrations](docs/05-protocol-and-integrations.md) | Recovery-object format, lifecycle, application integration, and interoperability | Platform and partner engineering |
| [06 — Business model and go-to-market](docs/06-business-model-and-go-to-market.md) | Customers, pricing hypotheses, distribution, economics, and metrics | Founders, investors, sales |
| [07 — Roadmap and validation plan](docs/07-roadmap-and-validation.md) | Staged execution plan, experiments, decision gates, and team needs | Founders, operators |
| [08 — Risks, compliance, and continuity](docs/08-risks-compliance-continuity.md) | Principal risks, regulatory workstreams, governance, and provider exit planning | Founders, legal, risk, investors |
| [09 — Developer ecosystem and AI identity](docs/09-developer-ecosystem-and-ai-identity.md) | Founder-led distribution through SecretSpec and FactorSeal, followed by AI identity expansion | Founders, developer relations, investors |

## Core thesis

Strong authentication has created a new category of catastrophic failure: a legitimate user can lose every device-bound credential and every recovery method at once. Backup codes address the cryptographic requirement for recovery, but not durability, discovery, verification, rotation, revocation, provider failure, or long-term continuity.

ProofAgain proposes a managed lifecycle around recovery material:

1. An application creates a narrowly scoped recovery object.
2. The user's device encrypts it before upload.
3. One or more independent providers hold ciphertext and constrained recovery capability.
4. A claimant proves that they correspond to the object's stable person reference.
5. Fraud controls, notifications, and a delay create time to stop an impersonator.
6. Approved recovery capability is delivered to a fresh device key.
7. The credential is decrypted locally and then rotated, replaced, archived, or deleted.

## Design principles

- **Recovery is exceptional.** Treat every request as a high-risk security event, not a login convenience.
- **Identity reference is not identity proof.** A stable identifier locates the right person's record; it never authorizes release by itself.
- **Encrypt before deposit.** Applications and clients should protect sensitive content locally.
- **Minimize authority.** Recovery objects should grant the narrowest capability needed to restore access.
- **Distribute trust.** High-value recovery should require independent providers, systems, and decisions.
- **Make attacks observable.** Delays, notifications, cancellation, audit trails, and transparency are first-class controls.
- **Manage the full lifecycle.** Receipt, replacement, revocation, expiration, migration, and deletion matter as much as storage.
- **Plan for decades.** Algorithm agility, provider exit, and portability are part of the security model.

## Scope

The proposed initial scope is:

- two-factor authentication backup-code sets;
- password-manager emergency keys;
- application recovery tokens;
- developer-account recovery credentials;
- enterprise break-glass tokens; and
- small encrypted emergency documents.

The initial scope explicitly excludes cryptocurrency seed custody, unrestricted private-key custody, large-file backup, everyday authentication, and recovery based only on knowledge of personal data.

## Strategic distribution

[Domen Kožar](https://github.com/domenkozar) and [Cachix](https://www.cachix.org/) would lead founder-driven marketing to developers. The strategy is to make [SecretSpec](https://secretspec.dev/) the best secrets tool for developers, use [FactorSeal](https://github.com/domenkozar/factorseal) to make backup-ready multifactor protection a normal part of local secret management, and introduce ProofAgain as the catastrophic recovery layer when every enrolled authenticator is gone.

The three products address different layers:

- **SecretSpec:** the portable declaration, resolution, policy, and audit layer for developer and AI-agent secrets;
- **FactorSeal:** the hardware-bound local storage and multifactor-unlock layer; and
- **ProofAgain:** the identity-gated last resort after normal authenticators and backups fail.

This developer wedge can later expand into AI identity infrastructure. AI agents need stable identities, named human or organizational controllers, narrowly delegated authority, secret-access policy, audit, revocation, rotation, and safe reissuance after a runtime or credential is lost. That future profile must remain distinct from natural-person identity proofing: an AI agent is identified by cryptographic provenance and delegated authority, not by a government identifier.

## Status

This repository contains a concept proposal, not a deployed system or finalized security protocol. Cryptographic choices require independent review. Identity-proofing policy, privacy design, insurance, and regulatory obligations require jurisdiction-specific legal and operational analysis before a pilot handles real recovery material.

## Vocabulary

- **Recovery object:** Small encrypted payload or authorization used to restore access.
- **Identity reference:** Stable, namespaced record indicating which unique person owns an object.
- **Identity proof:** Evidence and process used to determine whether a claimant is that person.
- **Provider:** Organization that stores encrypted objects, participates in verification, or releases a recovery share.
- **Recovery client:** Trusted software on the claimant's new device that generates keys and decrypts locally.
- **Threshold recovery:** A policy requiring a quorum, such as two of three independent providers.
- **Storage receipt:** Provider-signed evidence that a particular encrypted object version was accepted.
