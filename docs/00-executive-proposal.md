# Executive proposal

## Company

**ProofAgain** would provide universal, identity-gated recovery infrastructure for the passwordless internet.

Its promise is simple:

> **Prove who you are. Recover what is yours.**

## Problem

Passkeys, security keys, authenticator applications, TPM-backed credentials, and password managers make account takeover harder. They can also make legitimate recovery impossible. A person who loses every registered device and recovery method may be permanently locked out of an important account.

Most applications respond by issuing one-time backup codes and asking the user to print or safely store them. That leaves the hardest parts to the user:

- keeping the codes safe for years;
- remembering where they are after a crisis;
- knowing whether they are still valid;
- replacing them after rotation;
- protecting them from the same event that destroys the primary authenticators; and
- surviving the failure of the application or storage provider.

Backup codes are recovery material without a recovery system around them.

## Solution

ProofAgain would let applications deposit small recovery objects through a common protocol. The application or recovery client encrypts each object locally. The encrypted object is bound to a stable identity reference for one uniquely distinguishable person and stored with one or more recovery providers.

If every normal recovery path later fails, the claimant:

1. installs a recovery client on a new device;
2. generates a fresh recovery key pair;
3. completes an assurance process appropriate to the object;
4. waits through a fraud-detection and notification period; and
5. receives re-encrypted recovery capability from an approved provider quorum.

The client reconstructs and decrypts the object locally. The recovered credential is then rotated or replaced.

The identity reference identifies *which person's* objects are in scope. It is never a password or sufficient proof. Release depends on current identity evidence, independent risk signals, policy, and time for a legitimate user to object.

## Initial product

The first product would protect small, high-importance objects:

- two-factor backup codes;
- password-manager emergency keys;
- website and developer-account recovery tokens;
- enterprise break-glass credentials; and
- narrowly scoped authorizations to register a replacement passkey.

The consumer experience would resemble a safety-deposit service built for encrypted digital recovery material. The developer product would offer a client SDK, storage API, signed receipts, lifecycle operations, and a hosted recovery workflow.

An initial managed provider could use HSM- or confidential-computing-protected re-encryption. This would constrain employee and application access but would still place technical recovery authority in one provider. The target for high-value objects is threshold recovery across genuinely independent providers, so no single provider can decrypt or authorize release.

## Beachhead

The proposed wedge is security-conscious applications whose users already experience costly lockouts:

- password managers;
- developer platforms;
- security-key and identity vendors;
- enterprise access products; and
- services that have removed weak support-led recovery.

These partners have a direct incentive to reduce permanent lockout and support burden without quietly weakening authentication. Their existing paid plans also create a natural business-to-business-to-consumer distribution channel.

The first end users are people with a clear reason to care before disaster occurs: developers, administrators, password-manager customers, security-key users, and small-business owners.

## Founder-led distribution advantage

Domen Kožar and Cachix would lead marketing through products and communities that already serve developers. The objective is to make [SecretSpec](https://secretspec.dev/) the best secrets tool for developers: one portable declaration and policy layer across local machines, CI, production secret stores, language SDKs, and AI agents.

[FactorSeal](https://github.com/domenkozar/factorseal) supplies the complementary local-security story. Its target design is a hardware-bound keyring with mandatory, backup-ready multifactor unlock: platform hardware is required alongside an authenticator, and a completed vault maintains at least two independently enrolled authenticators. FactorSeal therefore teaches the right first behavior—strong factors plus a tested backup—while ProofAgain addresses the residual disaster in which the computer and every enrolled authenticator are lost.

The proposed adoption loop is:

1. developers adopt SecretSpec to declare and resolve application secrets;
2. they use FactorSeal as a secure local provider;
3. FactorSeal makes multiple independent authenticators and their lifecycle visible;
4. ProofAgain is offered as an optional catastrophic-recovery policy; and
5. recovery drills, signed receipts, and rotation turn the concept into a practiced security habit.

This is a credible product-led distribution channel because ProofAgain appears inside a real secret-management workflow rather than as an abstract insurance product. FactorSeal is currently an unaudited prototype and does not yet enforce its complete target policy, so the combined story is a roadmap and validation strategy, not a claim about production readiness.

## Business model

The primary model is recurring protection revenue, with possible recovery-event fees for expensive verification.

Potential offers include:

- application-sponsored coverage per protected user or active object;
- consumer and family subscriptions;
- enterprise plans with organizational approval policies;
- assurance tiers based on verification and provider threshold; and
- premium in-person or multi-provider recovery.

Storage is inexpensive because objects are small. The economic challenge is not bytes; it is identity proofing, fraud operations, support, secure key infrastructure, compliance, insurance, and maintaining a credible service for many years. Pricing and packaging must therefore be validated against expected recovery frequency and cost per recovery, not against commodity storage.

## Why this can become infrastructure

ProofAgain becomes more valuable if it is application-independent:

- users can discover recovery objects without remembering each deposit location;
- applications can integrate once instead of building country-specific identity recovery;
- providers can specialize in custody, verification, risk, or geographic coverage;
- portable formats and receipts reduce provider lock-in; and
- independent providers make stronger recovery policies possible.

The defensible asset would not be ciphertext storage alone. It would be the protocol, integrations, trusted provider network, audited recovery operations, identity-continuity records, risk data, and reputation for refusing fraudulent recovery.

## Why now

Authentication is becoming more secure and more device-bound, while support desks and ad hoc backup codes remain the fallback. As applications reduce password-based recovery, the gap between strong authentication and durable recovery becomes more visible.

ProofAgain's opportunity is to provide a standardized final layer without converting normal account support into a bypass around strong authentication.

AI agents make the identity layer more strategically important. Autonomous tools increasingly need secrets and delegated capabilities, but an agent also needs a stable answer to “which principal is acting, who controls it, what may it access, why, and how is its authority revoked or safely reissued?” SecretSpec already creates a natural policy and audit surface for agent secret access. ProofAgain can eventually extend the same continuity, approval, recovery, and audit concepts to cryptographically identified AI agents and workloads.

The AI expansion should not change the initial promise or weaken its identity model. Natural people continue to use high-assurance identity proofing. AI agents would use a separate protocol profile based on cryptographic identity, workload provenance, organizational control, delegated authority, and human accountability.

## Major risks

The startup succeeds only if it addresses difficult, coupled risks:

- a false-positive identity decision can become an account takeover;
- identity documents, biometrics, email, telephone numbers, and personal data can all be compromised;
- a provider or provider quorum may be coerced, breached, or dishonest;
- the service holds highly sensitive identity data even when it cannot read object contents;
- recovery obligations and liability vary by jurisdiction and object type;
- a failed company could strand users unless portability and exit are designed from the start; and
- demand may be strongest only after loss, while customers must pay before the event.

These are product fundamentals, not later compliance tasks.

## Staged company-building thesis

1. **Validate the pain and buyer.** Interview application security teams and users who have experienced high-impact lockout.
2. **Prove the workflow with synthetic objects.** Build local encryption, signed receipt, replacement, revocation, and delayed recovery without handling production secrets.
3. **Pilot low-liability objects with one provider.** Use a tightly bounded recovery capability, independent security review, and manual fraud operations.
4. **Demonstrate partner economics.** Measure enrollment, support reduction, recovery cost, cancellation, and willingness to pay.
5. **Add independent providers.** Implement interoperable threshold release and test provider failure and migration.
6. **Open the protocol.** Separate the standard and compatibility program from any single commercial provider.

## Proposed seed-stage objective

The first financing milestone should be evidence that trusted recovery can be both safer than support-led exception handling and usable enough for voluntary enrollment. A credible seed-stage deliverable would include:

- two design partners;
- an externally reviewed protocol prototype;
- a complete synthetic recovery ceremony;
- a jurisdiction-specific identity and compliance plan;
- measurable demand from protected users;
- a cost model based on observed verification operations; and
- a tested continuity and provider-exit mechanism.

Market size, price points, recovery frequency, and regulatory classification remain validation items. They should not be presented as settled facts until supported by primary research and counsel.
