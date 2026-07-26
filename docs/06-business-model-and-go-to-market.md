# Business model and go-to-market

## Commercial thesis

ProofAgain sells confidence that a catastrophic authentication loss remains recoverable without restoring a weak support bypass.

The economic value is not storage. It is:

- fewer permanent lockouts and escalated support cases;
- safer adoption of phishing-resistant authentication;
- retained customers after device-loss events;
- standardized identity and fraud operations;
- explicit audit and recovery policy;
- continuity across applications and providers; and
- reduced pressure on application staff to make risky exceptions.

The proposed starting model is B2B2C: an application integrates ProofAgain and sponsors or resells protection to its users. Direct consumer and enterprise plans can follow.

## Buyer map

| Party | Value received | Likely concern |
| --- | --- | --- |
| Application security leader | Strong catastrophic recovery without a hidden auth bypass | Liability and trust in provider decisions |
| Support leader | Fewer improvised, high-cost escalations | Workflow complexity and recovery time |
| Product leader | Higher confidence in passkeys and security keys | Enrollment conversion |
| End user | Durable, discoverable recovery | Privacy, trust, and paying before loss |
| Enterprise IAM owner | Governed break-glass process | Integration, approvals, audit, residency |
| Security-key or identity vendor | Lower customer anxiety and support burden | Brand risk and dependency |
| Insurer or risk partner | More explicit controls and evidence | Model uncertainty and correlated loss |

The person who enrolls may not control the purchasing decision. Sales and product discovery should map economic buyer, integration owner, security approver, recovery operator, and protected user separately.

## Initial customer profile

The best design partners are expected to have:

- a paid security-oriented product;
- users who protect high-value accounts;
- existing backup codes or a rotatable recovery token;
- measurable lockout and escalation cost;
- an internal security and privacy team;
- ability to add an enrollment flow at credential creation; and
- willingness to pilot with a bounded cohort and synthetic or low-liability objects.

Password managers, developer platforms, enterprise access products, and security-hardware vendors are stronger candidates than broad consumer services whose recovery policy is intentionally instant and low friction.

## Packaging hypotheses

### Application-sponsored protection

The application pays per protected user, per active recovery object, or through a platform minimum. Basic recoveries may be included; expensive proofing is charged separately or pooled.

This aligns distribution with the moment an object is generated and avoids requiring a new direct consumer relationship before value is understood.

### Consumer and family plan

A recurring plan covers several applications and objects with a defined assurance tier. A family plan should still maintain individual identity, privacy, and release boundaries; one subscriber must not automatically control another adult's objects.

### Enterprise plan

Adds organizational identity, administrator policy, designated approvers, residency choices, audit export, service commitments, and governed break-glass objects.

### Premium assurance

Higher tiers can fund multiple independent verification providers, in-person proofing, longer manual investigation, threshold provider release, or geographically diverse providers.

### Recovery-event fee

An event fee reflects variable identity-proofing and review cost. It must be disclosed at enrollment and designed so inability to pay during a disaster does not create a surprising permanent lockout. Prepaid or application-sponsored recovery may be more trustworthy.

## Pricing research

The proposal deliberately avoids unvalidated price points. Pricing experiments should measure:

- willingness to pay for protection before a loss;
- difference between application-sponsored and direct conversion;
- whether users understand recurring protection versus storage;
- acceptable recovery-event fee and payment timing;
- premium for independent-provider threshold recovery;
- enterprise willingness to pay for policy and audit; and
- sensitivity to waiting period and assurance level.

Tests should use credible product descriptions and, once safe, a working synthetic ceremony. Survey answers alone are weak evidence for a product purchased before a rare event.

## Unit economics

### Recurring cost drivers

- encrypted storage and replication;
- key-management infrastructure;
- provider-directory and audit operations;
- periodic object and receipt validation;
- notifications and customer support;
- compliance, insurance, and security assessment; and
- long-term continuity reserves.

### Event-driven cost drivers

- document or electronic-identity checks;
- live video or in-person verification;
- biometric and fraud-vendor calls;
- manual investigation and appeals;
- independent provider fees;
- high-risk incident response; and
- post-recovery support.

### Core model

For a protected cohort:

```text
annual contribution
  = recurring protection revenue
  + expected recovery-event revenue
  - recurring service cost
  - (recovery rate x average variable recovery cost)
  - channel and support cost
  - allocated risk, insurance, and continuity cost
```

The model needs ranges for recovery frequency, fraud-review rate, false-positive investigation, provider quorum cost, and retention. A low event rate helps gross margin but makes direct consumer urgency harder; a high event rate improves visible value but may make proofing operations expensive.

## Go-to-market sequence

### Stage 1: Design partnerships

Recruit a small number of security-oriented partners. Offer threat modeling, protocol co-design, a synthetic-object integration, and analysis of their historical lockout funnel.

Commercial goal: prove the problem has a budget owner and that the partner will place ProofAgain in the credential-creation flow.

### Stage 2: Closed pilot

Protect a bounded, rotatable recovery token for employees or an invited cohort in one jurisdiction. Recoveries begin as scheduled drills, with carefully governed real events only after review.

Commercial goal: measure enrollment, ceremony completion, event cost, and effect on partner support.

### Stage 3: Embedded paid coverage

Bundle protection in an application subscription or paid security tier. Provide partner-facing lifecycle automation and status reporting.

Commercial goal: demonstrate repeatable integration, renewal, and positive contribution margin.

### Stage 4: Multi-application inventory

Let protected users discover objects from multiple compatible applications after authorization. Add direct and family plans where the existing partner relationship creates trust.

Commercial goal: increase retention and value per protected identity without creating cross-application privacy leakage.

### Stage 5: Provider network and enterprise

Add genuinely independent providers, portable threshold policies, enterprise approval, and conformance testing.

Commercial goal: support higher-assurance objects and platform economics.

## Distribution

The highest-leverage distribution points are:

- generation or rotation of backup codes;
- passkey or security-key enrollment;
- password-manager emergency-kit setup;
- enterprise break-glass configuration;
- security-product onboarding; and
- account security reviews.

Generic advertising is less compelling because catastrophic loss is rare and easy to postpone. The issuer can explain the risk at the exact moment a recoverable object exists.

## Founder-led developer distribution

Domen Kožar and Cachix would own the initial marketing motion. This is intended to be technical, product-led, and trust-building rather than a broad consumer campaign:

- publish the threat model and build the products in the open;
- teach developers how strong authentication creates a recovery responsibility;
- demonstrate complete enrollment, factor-loss, replacement, and catastrophic-recovery ceremonies;
- integrate the tools into workflows developers already use;
- invite security review and respond publicly to limitations;
- use Cachix, devenv, Nix, open-source, conference, and partner channels; and
- turn scheduled recovery drills into evidence rather than selling fear.

Cachix contributes an existing company, operating history, and developer audience. Domen contributes a recognizable technical founder voice and the ability to explain the system directly. Neither substitutes for independent security review, identity operations, or distribution beyond the current ecosystem; they make the first developer cohort more reachable and credible.

## SecretSpec as the daily product

The strategic ambition is to make [SecretSpec](https://secretspec.dev/) the best secrets tool for developers. “Best” should be earned through a clear product standard:

- declare secret requirements once without committing values;
- resolve them from local, password-manager, cloud, or enterprise providers;
- preserve the same contract across development, CI, and production;
- offer excellent SDKs and command-line ergonomics;
- make provider migration routine;
- expose least-privilege policy and useful lifecycle status;
- audit which human or AI agent accessed which secret and why; and
- integrate secure local storage and catastrophic recovery without forcing either one.

SecretSpec should remain provider-independent. ProofAgain benefits from being one compatible recovery option, not from turning SecretSpec into a captive funnel. Developer trust and protocol adoption are stronger if users can choose storage and recovery providers.

SecretSpec gives the ecosystem a frequent-use surface. Developers may never invoke ProofAgain, but they resolve secrets continually. That daily value creates adoption, feedback, and a natural moment to identify credentials whose loss would be catastrophic.

## FactorSeal as the security habit

[FactorSeal](https://github.com/domenkozar/factorseal) is the proposed secure local provider behind SecretSpec. Its target model requires:

- platform hardware such as a TPM or Secure Enclave;
- one enrolled authenticator for an ordinary unlock; and
- at least two independently enrolled authenticators so one can be lost without destroying access.

This is more precise than saying only that it “requires 2FA.” It combines two factors for use and requires authenticator redundancy for recovery. The target design refuses removal that would leave the user without a backup authenticator.

FactorSeal can popularize good recovery hygiene among developers by making multiple authenticators, factor health, replacement, and recovery drills part of the normal local-secret workflow. ProofAgain does not replace this redundancy. It covers a different failure boundary: the user has lost the platform and every enrolled authenticator, or a disaster has destroyed all local recovery paths.

At the time of this proposal, FactorSeal is an unaudited prototype and its current version does not yet enforce the complete target enrollment policy. Marketing must preserve that distinction until implementation and independent review support stronger claims.

## Three-product adoption flywheel

| Layer | Product | User value | Business role |
| --- | --- | --- | --- |
| Declare and access | SecretSpec | One portable secret contract across tools and environments | Daily adoption and integration surface |
| Store and unlock locally | FactorSeal | Hardware-bound local secrets with backup-ready multifactor protection | Makes strong authentication and factor lifecycle tangible |
| Recover after total loss | ProofAgain | Identity-gated, delayed, auditable catastrophic recovery | Recurring protection and high-assurance infrastructure |

The intended funnel is:

1. a developer adopts SecretSpec for immediate workflow value;
2. SecretSpec recommends FactorSeal when a hardware-bound local provider is appropriate;
3. FactorSeal enrollment requires backup-ready authenticator hygiene;
4. the product explains the residual all-factors-lost scenario;
5. the developer voluntarily enrolls a narrow ProofAgain recovery object;
6. periodic status checks and drills verify that every layer still works; and
7. successful open-source use becomes evidence for partner and enterprise sales.

ProofAgain enrollment should be explicit, comprehensible, and optional. It should not be bundled through a dark pattern or presented as necessary for FactorSeal to function.

## Partner strategy

ProofAgain likely depends on partners for:

- issuing applications and distribution;
- identity documents and electronic-identity verification;
- in-person or postal proofing;
- HSM, protected execution, and key operations;
- independent recovery providers;
- notifications and fraud intelligence;
- security assessment and audit;
- insurance; and
- continuity in the event of company failure.

Build-versus-buy decisions should protect independence. Outsourcing every provider's proofing to the same vendor can turn a threshold system into a shared single point of failure.

## Competitive position

ProofAgain sits between several categories:

- backup-code storage;
- password managers and encrypted vaults;
- identity-verification services;
- account-recovery vendors;
- key custody and escrow;
- social recovery; and
- physical notary or safe-deposit services.

Its proposed differentiation is the combination of:

- application-issued, narrowly scoped objects;
- recovery after total user-secret loss;
- stable person continuity rather than one expiring document;
- local encryption and destination-key-bound release;
- lifecycle automation;
- cross-application discovery after authorization;
- portable provider-independent formats; and
- threshold recovery across independent providers.

No single item is a durable moat. Execution and trust compound across the complete system.

## Defensibility

Potential defensible assets include:

- deep integrations at credential-generation and rotation points;
- audited operational history and a reputation for safe denial;
- an identity-continuity graph with strong privacy boundaries;
- recovery-specific risk signals and fraud response;
- an independent provider network;
- application and provider conformance;
- regulatory and insurance readiness;
- protocol expertise and reference implementations; and
- user trust built through transparent continuity and incident handling.

The protocol should be open enough for portability. Commercial defensibility should come from reliable implementation and network trust, not trapping users' recovery material.

## Expansion into AI identity

Identity management for AI agents is likely to become a large infrastructure category. An autonomous agent may use many secrets, operate across machines, create sub-agents, act for a person or organization, and persist longer than one runtime. Secret storage alone cannot answer:

- Which agent or agent version is acting?
- Who created, owns, and remains accountable for it?
- Which human or organization delegated its authority?
- Which secrets and actions are within scope?
- Why did it request access?
- Can its authority survive a legitimate runtime loss without enabling a clone?
- How is it suspended, rotated, transferred, or terminated?

SecretSpec already provides the natural policy surface: a declared set of secret requirements plus access reason and audit. FactorSeal can protect local agent credentials. ProofAgain can eventually provide high-assurance continuity and reissuance when an agent runtime, device, or credential is lost.

The safer recovery object is not a raw, indefinitely valid agent private key. It is a narrow authorization to register a replacement agent identity, restore a signed capability manifest, or reissue time-limited credentials after human or organizational approval. This mirrors the proposed passkey model.

AI-agent identity must use a separate profile from natural-person identity:

- humans are linked through stable person references and current identity proof;
- organizations are linked through current governance and authorized representatives;
- agents and workloads are linked through cryptographic keys, signed provenance, runtime or workload attestations, and delegation chains.

The commercial expansion could include agent identity registry, delegated capability policy, secret-access audit, emergency suspension, credential rotation, multi-party reissuance, and cross-provider continuity. These capabilities would serve AI development platforms and enterprises while reusing ProofAgain's protocol, policy, quorum, audit, and continuity investments.

## Success metrics

### Enrollment

- eligible users offered protection;
- offer-to-enrollment conversion;
- completed receipt quorum;
- enrollment abandonment by step;
- active objects per protected identity; and
- percentage of objects current versus stale.

### Recovery

- scheduled drill completion;
- legitimate recovery success;
- median and tail recovery duration by tier;
- variable cost per request;
- cancellation and freeze rate;
- false-accept and false-reject indicators;
- manual-review and appeal rate; and
- percentage rotated immediately after release.

False accepts may be rare and partly unobservable. Metrics need independent incident review, not only dashboard labels.

### Partner economics

- integration time;
- partner support escalations before and after;
- retained customers after lockout;
- revenue per protected identity;
- gross contribution by tier;
- renewal and object replacement; and
- partner expansion to additional object types.

### Trust and continuity

- receipt validation success;
- provider availability;
- time to revoke a compromised provider or key;
- migration-drill completion;
- audit findings and remediation time;
- privacy deletion compliance; and
- notification delivery across independent channels.

## Market sizing plan

Market sizing should be bottom-up:

1. identify the initial application category;
2. estimate eligible paid accounts from reliable partner or public data;
3. measure the share offered and enrolled;
4. validate annual protection revenue per enrolled account;
5. model recovery frequency and variable cost;
6. add adjacent categories only after integration and policy overlap is demonstrated; and
7. keep consumer, application, and enterprise revenue separate.

Top-down identity, cybersecurity, or passwordless market totals are too broad to support this proposal by themselves.

## Commercial red lines

- Do not subsidize adoption by selling identity or application-inventory data.
- Do not let a high-value customer buy weaker proofing during an active request.
- Do not imply insurance or guaranteed recovery without a funded, contractual mechanism.
- Do not accept an object whose authority and post-recovery rotation are not understood.
- Do not expand into bearer assets merely because storage demand is high.
- Do not make support exceptions that bypass the published recovery policy.
