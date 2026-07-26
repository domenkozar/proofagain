# Identity, security, and privacy

## Security premise

ProofAgain exists for the moment when ordinary proof of possession has disappeared. That makes identity verification its primary operational security responsibility.

The system must assume an attacker may already know or possess:

- the victim's name, date and place of birth, address, and nationality;
- a national identifier;
- scans or photographs of government documents;
- access to email or a telephone number;
- breached passwords and personal history;
- realistic synthetic audio or video; and
- a corrupted, coerced, or careless insider.

No single piece of personal information is sufficient for recovery.

## Identity reference versus identity proof

### Identity reference

A stable record indicates which unique person owns the recovery objects. Where a country provides a permanent or long-lived government identifier, it may contribute to this reference using a country and identifier namespace:

```text
SI:EMSO:<identifier>
```

The raw identifier is neither secret nor authorization. It should be protected as sensitive personal data but designed as if an attacker can know it.

### Identity proof

Identity proof is the current evidence that a claimant corresponds to that person. It can combine:

- government-issued identity documents;
- government or qualified electronic identity;
- in-person examination;
- live supervised video;
- biometrics with appropriate liveness and anti-injection controls;
- previously enrolled strong authenticators;
- independent identity-proofing providers;
- trusted-contact or organizational approval; and
- manual investigation.

The proofing policy should evaluate provenance, independence, freshness, consistency, and known compromise—not merely the number of checks.

## Continuity across changing identity

A person outlives any one document. ProofAgain must preserve continuity across:

- passport and identity-card expiration;
- replacement after loss or theft;
- name and gender-marker changes;
- corrected dates or places of birth;
- changes of nationality or residence;
- government identifier changes in exceptional circumstances; and
- differences in scripts, transliterations, and naming conventions.

An individual passport number should generally be evidence history, not the permanent person reference.

Continuity records require strong correction and appeal mechanisms. A false merge between two people can be more dangerous than a duplicate record, so matching should surface uncertainty rather than silently combining records.

## Recovery assurance policy

Policy is object-specific. It should define:

- accepted proofing methods and required independent sources;
- provider quorum;
- waiting period;
- notification and cancellation channels;
- geographic and behavioral conditions;
- handling of recently issued or changed documents;
- manual-review triggers;
- organizational or trusted-contact approval;
- maximum attempts and cooldown;
- allowed destination client and key properties;
- recovery capability scope;
- expiration of approval and release; and
- mandatory post-recovery rotation.

Policy should be committed to at enrollment. It may be strengthened later with suitable authorization, but must not be weakened during an active recovery request.

## Recovery safety controls

### Delay

High-risk recovery should be intentionally slow. The waiting period gives legitimate users and providers time to detect impersonation. Riskier object types, identity changes, or recovery from a new country should extend review.

### Notification

Notify every surviving registered channel:

- existing devices and authenticators;
- application account sessions;
- email addresses and telephone numbers;
- trusted contacts; and
- enterprise security administrators.

Notifications are warnings, not proof. Compromised email or telephone access must not authorize release.

### Cancellation and freeze

An approved surviving authenticator should be able to cancel. A report of identity theft, disputed request, provider inconsistency, or suspicious evidence should freeze release pending investigation.

Cancellation itself needs abuse controls so an attacker cannot permanently deny recovery by repeatedly objecting through a compromised weak channel.

### Independent decisions

Threshold cryptography is strongest when providers make independent verification and risk decisions. Three providers using the same proofing vendor, risk engine, operators, and parent company create correlated failure despite separate brands.

### Narrow release

Approval applies only to named object versions and a request-specific device key for a short period. It must not create a reusable identity credential or reveal the full inventory unless policy permits it.

### Audit and transparency

Record who requested, verified, approved, denied, cancelled, and released; which policy and evidence commitments were used; and which code and key versions acted. Publish aggregate recovery, denial, fraud, government-demand, and provider-availability statistics where lawful.

## Threat model

### Protected assets

- plaintext recovery material;
- provider key shares and rewrap keys;
- identity records and raw proofing evidence;
- the confidentiality of a person's application inventory;
- integrity of object versions, policy, receipts, and audit events;
- destination device private keys;
- availability of revocation, cancellation, and recovery; and
- the legitimacy and independence of provider decisions.

### Adversaries

- remote account-takeover attacker;
- identity thief with breached personal data and document images;
- attacker controlling email, telephone, or a trusted contact;
- malicious or compromised application;
- malicious recovery client;
- insider at a provider or identity-verification vendor;
- compromised provider infrastructure or protected key environment;
- colluding provider quorum;
- coercive legal or political actor;
- abusive family member, employer, guardian, or fiduciary;
- attacker attempting denial of service or inventory discovery; and
- future attacker exploiting deprecated cryptography or abandoned infrastructure.

### Representative threats and controls

| Threat | Consequence | Principal controls |
| --- | --- | --- |
| Stolen identity data passes proofing | Fraudulent release | Multiple independent evidence sources, liveness/anti-injection, delay, notifications, manual review |
| Compromised email or telephone | Fake approval or hidden alert | Never use as sole approval; notify multiple channels; require stronger proof |
| Malicious support agent | Policy bypass | No administrative plaintext path; signed policy engine decisions; separation of duties |
| One provider compromise | Share theft or false approval | Independent threshold providers, scoped shares, audit and rapid suspension |
| Provider quorum collusion | Unauthorized recovery | Legal/technical independence, diverse jurisdictions, transparency, user cancellation |
| Malicious application swaps content | Wrong or overbroad recovery object | Signed inner object, clear user display, object-type constraints |
| Destination-key substitution | Attacker receives approved material | Bind key to request/client ceremony and all provider signatures |
| Rollback to older backup codes | Invalid or unsafe recovery | Monotonic versions, application receipts, supersession and revocation |
| Inventory enumeration | Privacy exposure and targeting | Non-enumerable references, rate limits, no enrollment confirmation before authorization |
| Recovery-request spam | Harassment or denial of service | Rate limits, cooldown, proof-of-intent controls, safe notification design |
| Provider disappearance | Permanent loss | Threshold redundancy, migration, escrowed continuity procedures, exit plan |
| Algorithm or key compromise | Broad decryption risk | Crypto agility, compartmentalized keys, rewrap/migration, compromise exercises |
| Coercive recovery | Release against user interest | Multi-jurisdiction quorum where lawful, due process, transparency, narrowly defined policy |

## Abuse cases beyond external hacking

The system must account for:

- an abusive partner using shared documents and devices;
- a former employee claiming enterprise break-glass access;
- a guardian or caregiver exceeding their authority;
- coercion of the claimant during video or in-person proofing;
- recovery attempted immediately after identity-document replacement;
- an insider repeatedly targeting a high-value person;
- a user trying to recover an object they transferred or agreed not to control; and
- disputes after death or incapacity.

Succession, guardianship, and incapacity should not be inferred from ordinary identity proof. They require a separate product, policy, and legal basis.

## Privacy architecture

### Data minimization

Collect only what is needed for uniqueness, current verification, fraud defense, and legal obligations. “Potential future usefulness” is not a sufficient retention purpose.

### Separation

Keep raw identity records, derived verification results, encrypted object storage, application pseudonyms, and audit data in separately controlled systems. Avoid a single query that produces a person's complete identity and application inventory.

### Pseudonymity

Applications should receive a provider- or application-specific reference such as:

```text
recovery_identity_reference: rp_7fa9c2...
unique_person_verified: true
```

They should not receive the underlying national identifier, documents, biometric evidence, or unrelated enrollment history.

### Evidence retention

Delete raw document images, video, and biometric samples as soon as the defined verification, dispute, fraud, and legal purposes allow. Prefer signed derived results and provenance over retained raw evidence where risk permits.

Retention schedules must distinguish:

- unsuccessful enrollment;
- successful enrollment;
- ordinary recovery;
- contested or fraudulent recovery;
- legal hold; and
- account closure.

### Purpose limitation

Identity data collected for recovery should not become an advertising identifier, credit signal, generalized login identity, or cross-application activity profile.

### User rights and corrections

Provide access, correction, deletion where applicable, appeal, and an auditable way to update identity history without severing continuity. Privacy requests must not silently destroy evidence needed to prevent fraudulent recovery; the legal basis and limits should be transparent.

## Biometrics

Biometrics may strengthen continuity, but they are sensitive, probabilistic, and difficult to revoke. Before use, the product must define:

- whether matching is one-to-one or one-to-many;
- where templates are generated and stored;
- presentation-attack, injection, and deepfake defenses;
- demographic and accessibility performance;
- human-review and appeal paths;
- retention and deletion;
- vendor reuse prohibitions;
- breach consequences; and
- alternatives for users who cannot or will not use biometrics.

Biometrics should contribute to a decision, not become an unchangeable recovery password.

## Security operations

- Recovery reviewers and key administrators must be different roles.
- High-impact actions require dual control and just-in-time access.
- Production access is recorded and regularly reviewed.
- Evidence exports are minimized, watermarked where appropriate, and time limited.
- Insider targeting and unusual reviewer behavior generate alerts.
- Red-team exercises cover identity proofing and human process, not only software.
- Providers rehearse false approval, false denial, key compromise, corrupt receipt, and total-region-loss scenarios.
- A vulnerability disclosure process and independent assessment are required before live pilots.

## Security claims that should be prohibited

Until specifically proven for a deployment, ProofAgain should not claim:

- identity verification is certain;
- no external party has recovery authority;
- zero knowledge across the whole system;
- threshold providers are independent merely because they have different names;
- confidential computing eliminates provider trust;
- deletion is instantaneous across every legal backup;
- biometrics cannot be spoofed; or
- recovery is guaranteed under every provider or state failure.

Precise limitations are part of earning trust.
