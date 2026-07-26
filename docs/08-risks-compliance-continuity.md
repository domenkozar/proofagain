# Risks, compliance, and continuity

## Purpose

ProofAgain combines encrypted custody, identity verification, fraud decisions, and account-recovery capability. That creates security, privacy, operational, legal, and reputational risk even if providers cannot normally read recovery objects.

This document is a planning framework, not legal advice or a conclusion about regulatory status. Obligations must be assessed for each jurisdiction, provider role, customer type, and recovery-object category before launch.

## Principal risk register

| Risk | Why it matters | Initial mitigation | Expansion gate |
| --- | --- | --- | --- |
| False identity acceptance | Can cause irreversible account takeover | Multiple signals, delay, notification, manual review, narrow rotatable object | Observed and red-team performance within approved threshold |
| False rejection | Legitimate user remains locked out | Appeals, alternative proofing, trained reviewers, document-history continuity | Measured accessibility and appeal outcomes |
| Single-provider compromise | Initial provider may have technical release authority | Protected keys, dual control, scoped authorization, audit, strict object limits | Independent threshold providers for higher-value objects |
| Correlated provider failure | Nominal quorum may share vendors or operators | Dependency disclosure and policy checks | Demonstrated operational, legal, and technical independence |
| Insider abuse | Staff may target a person or alter decisions | Separation of duties, just-in-time access, behavioral monitoring | Independent review and tested investigation |
| Privacy breach | Identity and application inventory are highly sensitive | Separation, pseudonyms, minimization, short raw-evidence retention | Privacy assessment and deletion verification |
| Provider or company failure | Users may lose the last recovery path | Receipts, migration, continuity reserve, contractual exit | Tested transfer or replacement-provider exercise |
| Credential invalidity | Stored object may be stale when needed | Automated replacement, status checks, expiration, reminders | Partner lifecycle integration |
| Legal compulsion | A provider may be ordered to release or retain data | Narrow data, independent jurisdictions where lawful, due process, transparency | Counsel-confirmed multi-provider policy |
| Recovery harassment | Requests and alerts can be abused against a person | Rate limits, cooldown, safe notification, freeze policy | Abuse monitoring and response |
| Liability concentration | One false release may cause broad downstream harm | Bounded rotatable capabilities, contract limits, insurance, exclusions | Loss experience and insurer approval |
| Demand timing | Users must buy before a rare event | Application bundling and security-plan distribution | Demonstrated paid enrollment and renewal |
| Protocol flaw | A systemic flaw can affect every object | Staging, external review, crypto agility, limited cohorts | Independent implementations and conformance |
| Vendor dependency | Proofing, HSM, cloud, or messaging failure may halt safety controls | Multiple vendors, exit terms, documented substitution | Successful dependency-loss exercise |
| AI identity scope creep | Agent recovery may clone authority or blur human accountability | Separate principal profile, fresh-key reissuance, explicit controllers and delegation | Independent AI threat model and bounded enterprise pilot |
| Reputation loss | One incident can undermine the category | Conservative claims, incident transparency, user-centered remediation | Governance and funded response capacity |

## Compliance workstreams

### Privacy and data protection

Assess:

- lawful basis for enrollment, verification, fraud prevention, and retention;
- controller, processor, and joint-controller roles;
- handling of national identifiers and special-category or sensitive data;
- biometric processing and alternatives;
- cross-border transfers and localization;
- access, correction, deletion, objection, and appeal;
- automated decision-making and meaningful human review;
- breach notification;
- retention by case state; and
- data-protection impact assessment requirements.

Architecture should minimize data regardless of the eventual legal label.

### Identity verification

Determine whether identity-proofing or trust-service rules apply, how electronic identities may be relied upon, and what assurance claims are permitted. Vendor assertions such as “verified” must be translated into specific evidence, checks, limitations, and contractual responsibility.

### Custody, escrow, and financial regulation

Analyze whether holding or enabling release of particular objects is regulated custody, key escrow, a trust service, money transmission, virtual-asset activity, or another licensed function.

This is a major reason to exclude cryptocurrency seed phrases and bearer assets from the initial product.

### Consumer protection

Terms and product language must accurately describe:

- which party has technical recovery authority;
- whether recovery is guaranteed;
- delays and possible denial;
- event fees;
- evidence retention;
- supported countries and documents;
- object expiration and validity;
- provider dependencies;
- cancellation and refund; and
- what happens if ProofAgain stops operating.

The user should understand at enrollment what will happen during a disaster years later.

### Security and incident obligations

Map contractual, statutory, partner, insurer, and certification requirements for:

- security program and access control;
- vulnerability management;
- penetration testing and independent assessment;
- incident response and notification;
- logging and audit retention;
- cryptographic key management;
- vendor oversight;
- business continuity; and
- government or law-enforcement demands.

### Records and evidence

Audit records may later be used to resolve a contested recovery. Define authenticity, retention, access, legal hold, redaction, and disclosure. Avoid treating indefinite raw evidence retention as the default answer.

### Accessibility and nondiscrimination

Identity methods can fail for people with disabilities, older documents, changed appearance, limited mobility, weak connectivity, uncommon naming systems, or no access to a supported government identity. The product needs accessible alternatives, appeal, and measured outcome review.

### Enterprise and employment

Enterprise break-glass recovery must distinguish personal identity from organizational authority. Employment, role, and approval must be current at recovery time; proving that a claimant is a named employee does not prove they remain authorized.

### AI agents and delegated authority

A future AI identity product requires separate analysis of agent accountability, automated decisions, software and model provenance, workplace monitoring, audit, intellectual property, cross-border operation, and the authority of human or organizational controllers. ProofAgain should reissue narrow capabilities to a fresh agent identity rather than copy an old key, and it must preserve an explicit chain from every agent to current accountable principals.

### Death, incapacity, and legal representatives

Ordinary recovery policy should not silently extend to heirs, executors, guardians, or attorneys-in-fact. Succession needs separate object consent, authority validation, delay, dispute handling, and jurisdictional analysis.

## Jurisdiction-selection framework

The first operating jurisdiction should be chosen using:

- availability and quality of stable identity references;
- government or qualified electronic identity coverage;
- privacy and biometric obligations;
- feasibility of in-person fallback;
- clarity of provider and custody classification;
- cross-border transfer and localization constraints;
- enforceability of consumer terms and liability allocation;
- availability of insurance;
- partner and customer concentration; and
- credible specialist counsel and fraud operations.

A small, well-supported jurisdiction is a safer pilot than nominal global coverage based on document scanning.

## Liability strategy

Liability cannot be solved only in terms of service. Product architecture should reduce the maximum loss:

- accept rotatable and narrowly scoped objects;
- limit release to one object version and destination key;
- require immediate exchange for a new normal authenticator;
- prohibit provider use of the recovered capability;
- cap pilot cohort and recovery frequency;
- use manual approval for every early request;
- define partner responsibilities for token scope and revocation;
- maintain insurance aligned with actual object categories; and
- reserve high-impact categories for separately capitalized and governed offerings.

Contracts should allocate duties among issuer, application, proofing vendor, storage provider, recovery provider, and user without contradicting the protocol's real trust boundaries.

## Incident classes

Runbooks should distinguish:

1. suspected fraudulent request before release;
2. confirmed false release;
3. provider key or share compromise;
4. proofing-vendor integrity failure;
5. identity or biometric data breach;
6. object ciphertext loss or corruption;
7. receipt or audit inconsistency;
8. application-issued invalidation failure;
9. provider outage or insolvency;
10. coercive or unlawful internal request;
11. notification and cancellation failure; and
12. protocol vulnerability affecting many objects.

Each runbook needs authority to pause, user and partner communications, evidence preservation, containment, provider suspension, object rotation, external notification, restitution analysis, and safe restart criteria.

## Long-term continuity

Recovery material may remain dormant for years. Continuity is therefore a security feature.

### Provider exit plan

Every provider should maintain:

- a current inventory of supported object and protocol versions;
- signed receipts and independently verifiable key history;
- funded operation or transition during wind-down;
- a replacement-provider or application reissuance path;
- customer and issuer notification procedures;
- protected key and share transfer or destruction procedures;
- legal handling of retained identity and audit data;
- support for pending and contested requests; and
- final deletion and attestation where applicable.

### Company continuity

ProofAgain should consider:

- a segregated continuity reserve;
- contractual step-in or wind-down arrangements;
- independent custody of protocol specifications, build material, and key-transition instructions;
- restrictions on acquisition that would collapse provider independence;
- continuity coverage in insurance and partner agreements; and
- governance that keeps the open protocol usable if the company fails.

Continuity mechanisms themselves are sensitive and must not create a master bypass.

### Cryptographic continuity

Maintain:

- a cryptographic-suite registry and deprecation schedule;
- signed provider-key transitions;
- object inventory by suite and key version;
- client and issuer notification of required migration;
- tested rewrap or application reissuance;
- protection against downgrade and rollback; and
- emergency response for primitive or implementation failure.

Objects should not depend on a library, device platform, or encoding that cannot be reproduced years later.

### Provider failure scenarios

Exercise:

- temporary outage during enrollment;
- outage during the waiting period;
- permanent provider loss before recovery;
- lost or suspected-compromised provider key;
- bankrupt provider with uncooperative management;
- provider withdrawal from a country;
- one provider issuing inconsistent state;
- common proofing vendor outage; and
- two providers revealed to share a controlling owner.

Threshold policy is valuable only if these scenarios have defined outcomes.

## Governance

### Internal

Establish accountable owners for:

- security architecture;
- cryptographic key operations;
- identity and fraud policy;
- privacy and retention;
- recovery operations;
- provider risk;
- application acceptance;
- incident command;
- continuity; and
- accuracy of public claims.

High-risk policy changes need documented review across these owners.

### Provider network

Provider participation should require:

- disclosed ownership and dependencies;
- security and proofing controls;
- key-management evidence;
- incident and government-demand processes;
- audit and transparency commitments;
- interoperability testing;
- continuity and exit capability;
- financial and insurance criteria; and
- suspension and removal rules.

### Protocol

Protocol governance should define:

- decision rights;
- public review;
- registries and namespaces;
- backward compatibility;
- emergency security changes;
- conformance;
- intellectual-property terms;
- conflict-of-interest handling; and
- continuity outside the company.

## Recovery guarantees and service commitments

Availability targets should distinguish:

- enrollment and lifecycle API availability;
- revocation and cancellation availability;
- recovery-status availability;
- minimum and maximum policy delay;
- proofing and manual-review time;
- provider quorum availability; and
- object durability.

A conventional uptime percentage does not describe whether a user can safely recover. Service commitments should cover state integrity, receipts, response deadlines, migration assistance, and incident communication.

## Due-diligence evidence

Before a real-money or high-impact deployment, stakeholders should expect:

- architecture and data-flow diagrams;
- threat model and abuse-case review;
- protocol and implementation assessment;
- key-management policy and ceremony evidence;
- proofing-vendor performance and dependency analysis;
- privacy impact and retention schedules;
- penetration and social-engineering test results;
- incident, appeal, and continuity exercises;
- provider ownership and jurisdiction map;
- insurance scope and exclusions;
- customer and provider contracts;
- observed pilot false-reject and review data; and
- clear documentation of residual trust and risk.

## Non-negotiable launch conditions

ProofAgain should not launch a recovery category unless:

- the object's authority is understood and bounded;
- the issuing application can revoke or rotate it;
- the identity policy has independent review;
- a mandatory delay and cancellation path exist;
- the recovery response is bound to a fresh device key;
- no support role can bypass the policy;
- audit records are durable;
- evidence retention and user rights are operational;
- incident and provider-exit plans have been exercised; and
- public claims match the actual deployment mode.
