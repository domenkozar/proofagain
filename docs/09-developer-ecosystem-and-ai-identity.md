# Developer ecosystem and AI identity

## Strategic thesis

ProofAgain does not need to begin as an unfamiliar consumer insurance product. It can grow from a developer-security ecosystem led by Domen Kožar and Cachix:

- [SecretSpec](https://secretspec.dev/) becomes the best secrets tool for developers;
- [FactorSeal](https://github.com/domenkozar/factorseal) makes hardware-bound, backup-ready multifactor protection a normal local default; and
- ProofAgain provides the final identity-gated recovery layer after the platform and every ordinary authenticator are gone.

This creates a progression developers can understand:

```text
declare and resolve secrets
        SecretSpec
             |
store and unlock them safely
        FactorSeal
             |
recover after total factor loss
        ProofAgain
```

Each product delivers standalone value. Their integration creates a distribution and education advantage without requiring them to share one security boundary.

## Why Domen and Cachix matter

Domen and Cachix would lead the initial marketing motion. The advantage is not merely access to a mailing list. It is the combination of:

- an established developer-facing company;
- experience shipping infrastructure that developers must trust;
- open-source credibility;
- existing relationships in the Nix and devenv ecosystems;
- a technical founder who can explain design tradeoffs directly;
- products that can demonstrate recovery rather than only describe it; and
- an audience likely to understand the cost of losing keys, tokens, and infrastructure access.

Founder-led marketing is especially important for ProofAgain because the product asks users to trust a service before a rare and stressful event. Deep technical writing, public threat models, reproducible demos, transparent prototype warnings, and visible responses to review are more credible than generic security advertising.

The initial channel should be treated as a beachhead, not the total market. ProofAgain still needs distribution through password managers, developer platforms, identity vendors, enterprises, and compatible independent providers.

## Make SecretSpec the best secrets tool for developers

The ambition for SecretSpec should be explicit: become the default portable interface between an application and the secrets it needs.

That means excelling across the full developer workflow:

- one committed declaration of secret names and requirements without committed values;
- consistent resolution across laptops, CI, production, and ephemeral environments;
- provider choice without application rewrites;
- reliable migration between providers;
- first-class SDKs and predictable command-line behavior;
- types, validation, composition, and safe generation;
- strong local defaults and enterprise backends;
- access policy, reason capture, and audit for humans and AI agents;
- lifecycle information for rotation, expiration, and revocation; and
- optional recovery integration for credentials whose loss would be catastrophic.

SecretSpec should remain open and provider-independent. Its claim to be the best should come from interoperability, developer experience, and trustworthy behavior—not from locking users into FactorSeal, ProofAgain, or Cachix.

SecretSpec is the frequent-use product in the portfolio. A developer may invoke ProofAgain only once in a lifetime, but SecretSpec can resolve secrets every day. That creates an ongoing relationship, a place to show object health, and an opportunity to discover which secrets lack a tested recovery policy.

## FactorSeal as the bridge from security to recovery

FactorSeal is designed as a hardware-bound local keyring. Its target policy combines:

```text
platform hardware
       AND
one enrolled authenticator
```

with a separate availability rule:

```text
minimum enrolled authenticators = 2
```

An ordinary unlock therefore uses real multifactor protection, while the enrollment minimum ensures that loss of one phone or security key does not immediately destroy the vault. The factors remain independently enrolled rather than cloning one private key.

This model can popularize several habits among developers:

- enroll a backup before the vault becomes active;
- verify every authenticator independently;
- label and inspect factor state;
- replace a lost factor atomically;
- refuse downgrade to platform-only unlock;
- practice loss scenarios before an emergency; and
- distinguish ordinary redundancy from catastrophic recovery.

ProofAgain belongs after those controls, not instead of them. The ProofAgain event begins only when the user has lost the relevant platform and all normal FactorSeal authenticators or recovery methods.

The exact FactorSeal recovery object still requires design and security review. Safer candidates include a narrow authorization to enroll a replacement factor or a protected recovery share with mandatory rotation. Depositing a raw reusable vault key would create broader authority and should not be the default.

At the time of this proposal, FactorSeal is explicitly an unaudited prototype. Its current v2 behavior does not yet enforce the complete target two-authenticator enrollment policy. Public demonstrations must describe target architecture and shipped behavior separately until implementation and independent assessment close that gap.

## The developer adoption loop

1. **Solve today's problem.** A developer adopts SecretSpec to remove duplicated `.env` contracts and use secrets consistently across tools.
2. **Offer a safer local provider.** FactorSeal protects local values with platform hardware and backup-ready multifactor unlock.
3. **Teach lifecycle.** Enrollment, health, replacement, and drills make factor loss visible and manageable.
4. **Name the remaining risk.** The product explains what happens if a disaster destroys the computer and every enrolled authenticator.
5. **Offer ProofAgain.** The developer can protect a narrowly scoped recovery object under a clear identity, delay, notification, and release policy.
6. **Verify durability.** SecretSpec can surface signed receipts, object status, rotation needs, and scheduled recovery drills without reading recovery plaintext.
7. **Expand through evidence.** Successful open-source use and drills become credible case studies for partner and enterprise integrations.

This is education through product behavior. ProofAgain should not manufacture fear or make its enrollment a hidden requirement for FactorSeal.

## Founder-led marketing program

### Technical narrative

Publish a coherent series:

- why `.env` is not a secret-management contract;
- why strong authentication creates catastrophic lockout risk;
- why two enrolled authenticators and catastrophic recovery are different;
- why a national identifier locates a record but never authorizes release;
- why recovery necessarily retains constrained external trust;
- how destination-key-bound and threshold recovery distribute that trust; and
- how the same principles apply to AI agents.

### Demonstrations

Show complete ceremonies rather than isolated encryption:

- SecretSpec resolving the same declaration from different providers;
- FactorSeal enrollment with primary and backup authenticators;
- loss and atomic replacement of one authenticator;
- loss of the machine and all authenticators;
- a synthetic ProofAgain identity-verification and waiting period;
- cancellation of a fraudulent request;
- local recovery and immediate credential rotation; and
- migration away from a failed provider.

### Community

Use open design discussions, conference talks, Nix and devenv integrations, security reviews, issue trackers, Discord, partner content, and scheduled public recovery drills. The strongest marketing artifact is a system that fails safely under scrutiny.

### Conversion

Measure movement from:

```text
SecretSpec user
  -> secure provider user
  -> backup-ready FactorSeal vault
  -> completed ProofAgain enrollment
  -> successful scheduled drill
  -> team or enterprise adoption
```

Stars, page views, and newsletter subscribers are useful reach signals but not proof that recovery is protected.

## Why AI identity management will be large

AI agents change identity from a login concern into an operating-system and infrastructure concern. An agent can:

- act across many services;
- request and use high-value secrets;
- create or supervise other agents;
- move between local devices, CI, cloud runtimes, and customer environments;
- change model, prompt, tools, or code while retaining a logical role;
- operate for a person, team, or company; and
- outlive one process or credential.

Organizations therefore need answers to more than “is this API key valid?”:

- Which agent and version is acting?
- Who controls and remains accountable for it?
- What chain of delegation gave it authority?
- Which capabilities and secrets are within scope?
- Why is access necessary for this task?
- Which runtime and software provenance are present?
- How can authority be revoked everywhere?
- How is legitimate continuity restored after a runtime or key is lost?
- How do we prevent recovery from creating an unauthorized clone?

This makes agent identity, authorization, secret access, audit, revocation, and continuity a likely major infrastructure category.

## The combined AI identity stack

### SecretSpec

Defines which secrets an agent may request, resolves them without hard-coding a storage backend, requires an access reason, and records audit metadata without recording secret values.

### FactorSeal

Protects local developer or agent-bootstrap credentials using platform hardware and independent authenticators. It can provide a strong boundary for local supervised agents.

### ProofAgain

Provides exceptional continuity: approved reissuance after the identity key, runtime, or controlling device is lost; multi-party recovery for critical agents; emergency suspension; and portable audit of the recovery decision.

Together, the products can connect daily secret use with durable identity governance:

```text
human or organization
        delegates
cryptographic agent identity
        requests under policy
SecretSpec secret capability
        protected locally by
FactorSeal
        recoverable exceptionally through
ProofAgain quorum and reissuance
```

## Agent identity is not human identity

The initial ProofAgain design identifies unique natural people and verifies claimants through government identity, biometrics, electronic identity, in-person checks, and risk review.

An AI agent has none of those properties. Its stable reference should instead be based on:

- a cryptographic public key or key history;
- controller organization and accountable human sponsors;
- signed creation and delegation records;
- software, model, prompt, and tool provenance where relevant;
- workload or runtime attestations;
- capability-policy commitments;
- status, version, expiration, and revocation; and
- links between predecessor and replacement identities.

The protocol can share envelope, receipt, policy, quorum, waiting, audit, migration, and release machinery across principal types. It must keep their proof methods and assurance claims separate.

## Safe AI recovery

Copying an old agent private key may create an undetectable clone with inherited authority. A better recovery flow is:

1. a new runtime generates a fresh identity key;
2. current human and organizational controllers authorize a narrowly scoped request;
3. policy verifies provenance, delegation, workload evidence, and incident state;
4. a waiting period or security review applies when impact is high;
5. a provider quorum issues authorization to the fresh key;
6. dependent services rotate or reissue time-limited capabilities;
7. the predecessor identity is revoked or explicitly marked superseded; and
8. the transition is recorded in an auditable identity history.

Possible recovery objects include:

- authorization to register a replacement agent key;
- a signed capability manifest with strict expiry;
- permission to reissue selected provider credentials;
- organization-approved bootstrap material;
- an emergency suspension or rollback authorization; and
- a threshold share for a narrowly governed agent role.

Raw production secrets and unrestricted signing keys should remain outside the default model.

## Expansion sequence

### Phase 1: Developer secrets

Make SecretSpec excellent, complete FactorSeal's target safety model, and validate ProofAgain with synthetic developer recovery objects.

### Phase 2: Human-supervised agents

Use SecretSpec policy and audit for coding and operations agents whose human operator remains present. Validate identity labels, reasons, scope, and revocation.

### Phase 3: Enterprise agent identity

Add organization-controlled agent registries, delegation chains, workload evidence, short-lived credentials, and emergency suspension.

### Phase 4: Agent continuity

Pilot multi-party reissuance and recovery for a bounded, replaceable agent identity. Prove that a lost runtime can be restored without silently cloning its authority.

### Phase 5: Interoperable identity infrastructure

Support provider-independent agent identity, policy, recovery receipts, cross-platform rotation, and continuity across organizational and runtime boundaries.

Each phase must produce standalone customer value. The AI thesis should not delay or blur the initial human recovery product.

## Measures of success

### Developer ecosystem

- active SecretSpec projects and repeat use;
- provider and SDK reliability;
- SecretSpec-to-FactorSeal activation;
- completed backup authenticator enrollment;
- FactorSeal loss and replacement drills;
- ProofAgain enrollment and receipt completion;
- scheduled catastrophic-recovery drills;
- open-source contributors and independent reviews; and
- application and enterprise design partners sourced from the ecosystem.

### AI identity

- agents with an explicit controller and delegation chain;
- secret requests with policy-compliant reason and audit;
- time to suspend and rotate an agent identity;
- successful fresh-key reissuance without predecessor reuse;
- detected attempts to clone or exceed delegated authority;
- enterprise willingness to pay for agent lifecycle and recovery; and
- interoperability across secret providers and agent runtimes.

## Strategic boundaries

- SecretSpec remains useful without FactorSeal or ProofAgain.
- FactorSeal's normal redundancy is not marketed as identity-gated recovery.
- ProofAgain does not weaken FactorSeal's multifactor policy.
- Prototype behavior is never presented as audited production behavior.
- AI agents do not receive human identity references.
- A human sponsor is accountable but does not automatically own every agent action.
- Recovery reissues narrow authority; it does not silently clone old keys.
- AI expansion follows customer evidence and separate threat review.
- Open protocols and provider choice take priority over ecosystem lock-in.
