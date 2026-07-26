# Roadmap and validation plan

## Roadmap principle

ProofAgain should earn the right to handle real recovery material. Each stage increases authority only after the preceding security, demand, operational, and continuity assumptions have evidence.

Calendar estimates should be set after team formation and partner discovery. The plan therefore uses evidence gates rather than promised dates.

## Stage 0: Problem and policy discovery

### Objectives

- identify the first buyer and bounded object type;
- understand real lockout and support workflows;
- select one candidate operating jurisdiction;
- map identity-proofing, privacy, custody, and liability questions; and
- define claims the product can and cannot make.

### Work

- interview affected users and application teams;
- analyze anonymized historical lockout cases with design partners;
- map the current exception path and its security weaknesses;
- obtain specialist legal and insurance analysis;
- draft the threat model and abuse cases;
- test product language and willingness to enroll; and
- define the proposed assurance policy.

### Exit gate

Proceed only if:

- at least two credible partners will co-design or pilot;
- one object type has bounded, rotatable authority;
- a buyer acknowledges budget or measurable economic value;
- the first jurisdiction has a plausible lawful operating path; and
- no critical workflow depends on a hidden support bypass.

## Stage 1: Synthetic protocol prototype

### Objectives

- validate the complete ceremony without production secrets;
- establish local encryption and destination-key-bound release;
- prove lifecycle and receipt semantics; and
- expose usability and operational failure modes.

### Build

- reference issuer and client;
- versioned recovery-object envelope;
- managed provider prototype;
- signed provider directory and storage receipts;
- create, status, replace, revoke, expire, and delete operations;
- recovery-request state machine;
- synthetic identity-evidence adapter;
- delay, notification, cancellation, denial, and approval;
- new-device local decryption; and
- append-only event history.

### Exercises

- all devices lost;
- object ID forgotten;
- old object version presented;
- destination key substituted;
- notification channel compromised;
- identity document recently changed;
- claimant has accessibility constraints;
- provider unavailable;
- provider key rotated;
- request cancelled during the delay;
- company service restored from backup; and
- complete object migration to a replacement provider.

### Exit gate

Proceed only if:

- external reviewers find no unresolved design-level critical issue;
- the client can verify every security-relevant provider claim;
- failed replacement never invalidates the last active version;
- no administrative interface can return recovery plaintext;
- migration and restore exercises succeed; and
- representative users understand the recovery delay and trust boundaries.

## Stage 2: Closed design-partner pilot

### Scope

- one jurisdiction;
- one managed provider;
- one rotatable, non-bearer object type;
- partner employees or a small invited cohort;
- strict enrollment cap;
- scheduled recovery drills first; and
- manual review for every request.

### Operational readiness

- reviewed identity-proofing policy;
- trained reviewers and separation of duties;
- incident and contested-recovery runbooks;
- privacy notices, retention, correction, and deletion;
- key ceremonies and compromise response;
- vulnerability disclosure and external assessment;
- insurance and contractual allocation;
- customer support that cannot override policy;
- provider-exit plan; and
- pilot stop criteria.

### Exit gate

Proceed only if:

- enrollment and drills meet usability targets;
- observed verification and review cost supports a plausible price;
- partner support workflow improves rather than duplicates effort;
- privacy and evidence-retention controls work in practice;
- incidents and false rejections can be investigated and appealed;
- the partner will convert to a paid deployment; and
- independent risk review approves bounded production use.

## Stage 3: Bounded production product

### Objectives

- establish recurring application-sponsored revenue;
- automate safe lifecycle operations;
- measure real recovery performance; and
- build an auditable operating history.

### Capabilities

- production SDK and partner console;
- automated object replacement and invalidation;
- periodic recoverability and receipt checks;
- consumer status reminders;
- multiple independent notification channels;
- risk-based manual escalation;
- formal audit and transparency reporting;
- contractually defined service and recovery policy; and
- routine backup, restore, migration, and key-compromise exercises.

### Expansion gate

Add object types or jurisdictions only when:

- authority and post-recovery rotation are documented;
- fraud and liability are within approved bounds;
- identity continuity works for the new jurisdiction;
- unit economics remain viable;
- operations are staffed for peak and contested cases; and
- the existing service's safety is not diluted.

## Stage 4: Independent threshold pilot

### Objectives

- remove unilateral technical release from one provider;
- validate independent policy decisions;
- demonstrate recovery through one provider outage; and
- prove portable provider replacement.

### Work

- formal threshold protocol design and review;
- provider-set directory and independence disclosures;
- independently operated cryptographic boundaries;
- distinct identity or risk paths;
- signed authorization and release messages;
- quorum-client verification;
- provider suspension and replacement;
- malicious-provider and equivocation tests; and
- cross-provider incident exercises.

### Exit gate

The threshold product is credible only if:

- no single provider can reconstruct or release the object;
- threshold participants do not share an undisclosed critical dependency;
- the client rejects inconsistent policy, version, or destination-key responses;
- one failed provider does not prevent recovery;
- one malicious provider cannot force recovery;
- provider migration works without plaintext exposure to providers; and
- legal agreements match the technical independence claim.

## Stage 5: Protocol ecosystem

### Objectives

- support independent applications, clients, and providers;
- create portable user choice; and
- separate protocol continuity from one startup.

### Work

- publish a reviewed specification and threat model;
- release test vectors and conformance tooling;
- run interoperability events;
- define namespace and registry governance;
- publish cryptographic-suite lifecycle rules;
- establish a security advisory process;
- define a compatibility mark and revocation process; and
- recruit enterprise, regional, and specialist providers.

Open governance should follow interoperable implementation experience. Publishing early designs is valuable; freezing an immature wire standard is not.

## First 90 days

### Customer and market

- Recruit two potential design partners.
- Complete structured interviews across users, security, support, and risk.
- Obtain baseline lockout volume, exception path, support time, and churn evidence where available.
- Select one recovery object and write its exact authority and rotation behavior.
- Test enrollment positioning and pricing structure.

### Security and product

- Write a formal set of assets, actors, trust boundaries, abuse cases, and prohibited claims.
- Prototype the enrollment and recovery experience with synthetic secrets.
- Define object, receipt, request, approval, and release messages.
- Test inventory discovery without enrollment enumeration.
- Review accessibility and contested-identity flows.

### Operations and legal

- Select a candidate pilot jurisdiction.
- Map identity, privacy, biometric, breach, retention, consumer, custody, and outsourcing obligations with counsel.
- Compare proofing vendors and identify shared dependencies.
- Draft incident, cancellation, appeal, deletion, and company-exit runbooks.
- Explore insurance requirements and exclusions.

### Fundraising evidence package

- design-partner letters or signed pilot intent;
- observed problem and cost evidence;
- working synthetic ceremony;
- external architecture review;
- pilot risk boundaries;
- operating and unit-cost model;
- regulatory workstream; and
- staged use of funds tied to evidence gates.

## Validation experiments

| Hypothesis | Experiment | Strong signal | Stop or revise signal |
| --- | --- | --- | --- |
| Users will enroll before loss | Offer credible protection in a partner's backup-code flow | Meaningful completed enrollment without heavy support | Interest but little completion or major trust objections |
| Applications will pay | Partner discovery plus priced pilot proposal | Budget owner accepts pilot or contract | Security interest with no owner or economic value |
| Delay is acceptable | Prototype recovery under multiple delay explanations | Users accept delay for high-assurance objects | Users expect instant recovery regardless of risk |
| Discovery matters | Test recovery without object IDs or prior app memory | Users successfully find authorized objects | Inventory adds little value or creates unacceptable privacy risk |
| Verification can be safe enough | Red-team proofing flow using synthetic identities | Attacks are detected and uncertainty escalates | Common breached data reliably passes |
| Unit economics work | Run scheduled manual ceremonies and cost every step | Contribution remains viable at validated price | Review cost or exception rate dominates revenue |
| One-provider pilot has value | Compare with current partner recovery | Safer, more consistent workflow and lower burden | Merely duplicates support while adding a central failure |
| Threshold providers are independent | Dependency audit and outage/collusion exercises | Quorum survives one failure without shared decision path | Common vendor or operator defeats independence |

## Decision log

Founders should maintain a decision record for:

- first object type;
- first jurisdiction;
- assurance policy and waiting period;
- identity and biometric choices;
- cryptographic deployment mode;
- evidence retention;
- provider independence criteria;
- prohibited customer categories;
- incident stop conditions;
- protocol publication timing; and
- company continuity funding.

Each entry should name the evidence, decision owner, review date, and reversal conditions.

## Team requirements

The founding team needs more than application engineering:

- product leadership experienced in trust-heavy user journeys;
- applied cryptography and protocol engineering;
- identity and fraud operations;
- privacy and security engineering;
- partner integration and developer experience;
- customer support design for contested cases; and
- jurisdiction-specific legal and compliance leadership.

Independent advisors do not replace accountable internal ownership. Before live recovery, someone must directly own identity false accepts, privacy retention, cryptographic release, incident response, and provider continuity.

## Stop conditions

Pause enrollment or release when:

- identity-proofing integrity is in doubt;
- a provider key or protected boundary may be compromised;
- notifications or cancellation are materially unavailable;
- object versions or policy commitments disagree;
- audit events cannot be durably recorded;
- a partner asks staff to bypass policy;
- fraud losses exceed the approved pilot boundary;
- insurance or legal authority no longer covers operation; or
- company continuity obligations cannot be funded.

The ability to stop safely is a launch requirement.
