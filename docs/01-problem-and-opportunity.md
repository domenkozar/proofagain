# Problem and opportunity

## The problem in one sentence

Modern authentication can prevent an attacker from getting in while also preventing the legitimate user from ever getting back in.

## What changed

Authentication has shifted from reusable knowledge toward possession and device-bound cryptography:

- hardware security keys;
- device-bound and synchronized passkeys;
- authenticator applications;
- TPM- and secure-enclave-backed credentials;
- password-manager recovery keys;
- multi-factor authentication; and
- device-specific encryption keys.

This is a security improvement. The corresponding recovery model, however, is often still a printable list, a weak support workflow, or another account protected by the same devices.

The result is a recovery trilemma:

1. the user can lose every device and retained secret;
2. no external party retains any capability related to decryption; and
3. recovery remains possible.

All three cannot be guaranteed simultaneously. If the user retains nothing, an external party or independent quorum must retain constrained capability. The product question is therefore not how to eliminate trust, but how to distribute, minimize, delay, monitor, and audit it.

## Failure scenarios

Catastrophic lockout is usually a compound event rather than a forgotten password:

- a stolen phone contains both the passkey and authenticator app;
- a laptop failure destroys the only device-bound credential;
- all registered hardware keys are kept in the same bag or building;
- a password-manager vault and its stored recovery notes become inaccessible together;
- a cloud identity suspension also blocks synchronized passkeys;
- fire, flood, displacement, or theft removes devices and paper records;
- a backup-code file exists but the user no longer remembers its location;
- old recovery codes were invalidated after rotation; or
- the primary email and telephone recovery channels fail simultaneously.

The user discovers the weakness only when the recovery event is already under way.

## Why existing alternatives are incomplete

### Printed or downloaded backup codes

They are inexpensive and provider-independent, but offer no discovery, validity checking, replacement, policy, or durable custody. They are also often lost in the same incident as primary factors.

### Cloud drives, email, and password managers

They are convenient but may share the same trust and failure domain as the account being recovered. Storing plaintext recovery material also turns an ordinary compromise into a bypass of strong authentication.

### Support-led account recovery

Support can handle exceptions, but inconsistent manual judgment is difficult to secure and scale. A flexible support process can become the weakest authentication factor.

### Trusted friends or family

Social recovery can distribute access, but relationships change, contacts become unavailable, and a trusted person may be coerced or compromised. It is better as one policy signal than as the only control.

### Attorneys, notaries, banks, and safe-deposit boxes

These can provide durable, high-assurance custody, but are local, expensive, slow to update, and poorly integrated with routine credential rotation.

### A single encrypted vault

Encryption protects content at rest, but the system must still answer who can recover the decryption capability after every user-held secret is gone. The hard problem has moved, not disappeared.

## Jobs to be done

### End user

> When I lose all of my authenticators, help me regain narrowly scoped access without having planned perfectly years earlier and without allowing ordinary personal data to impersonate me.

### Application security team

> Let us offer catastrophic recovery without building a global identity-verification operation or weakening our primary authentication.

### Support and risk team

> Replace improvised exceptions with explicit assurance policy, evidence, delay, cancellation, and audit.

### Enterprise administrator

> Preserve a governed break-glass path that survives loss of devices and individual staff turnover while requiring organizational approval.

## Customer and user segments

| Segment | Current pain | Potential value |
| --- | --- | --- |
| Password-manager customers | Loss may cascade across every account | Durable emergency-key recovery |
| Developers and administrators | Accounts control code, infrastructure, and production systems | Recovery that does not weaken daily authentication |
| Security-key and passkey users | Strong factors can all be lost together | Catastrophic-loss safety net |
| Consumer applications | Lockouts create support cost and churn | Standard recovery integration and policy |
| Enterprises | Break-glass material is hard to govern and rotate | Approval workflows, receipts, and audit |
| Identity and hardware vendors | Product adoption can be inhibited by loss anxiety | Embedded recovery assurance |

The beneficiary, buyer, and integration owner may be different parties. Product research must distinguish all three.

## Initial opportunity

The strongest initial use case has five properties:

1. the object is small;
2. losing it has meaningful but bounded impact;
3. the issuing application can rotate it after recovery;
4. the application can integrate directly; and
5. the recovery policy can be made explicit.

Two-factor backup-code sets and narrowly scoped application recovery tokens fit these constraints better than unrestricted cryptocurrency seed phrases or general private-key custody.

## Market thesis

ProofAgain is based on six hypotheses:

- stronger and more device-bound authentication increases the importance of an independent final recovery layer;
- applications prefer a specialized recovery network to maintaining country-specific identity and fraud operations;
- users will enroll before a loss event when protection is bundled into a trusted application or paid plan; and
- an open, portable protocol can support a network of differentiated providers without forcing applications to integrate each one separately;
- a developer-security ecosystem led by Domen Kožar and Cachix can create a lower-cost adoption path through SecretSpec and FactorSeal; and
- identity, delegated authority, and credential continuity for AI agents will become a major adjacent infrastructure category.

These hypotheses imply a B2B2C beachhead rather than a consumer-only launch. Distribution through an application is present at the moment recovery material is generated or rotated, when enrollment is most relevant.

The developer wedge is unusually concrete. [SecretSpec](https://secretspec.dev/) can become the daily interface through which developers declare, resolve, and audit secrets. [FactorSeal](https://github.com/domenkozar/factorseal) can make hardware-bound, backup-ready multifactor storage the secure local default. ProofAgain then protects the exceptional case that neither product can solve alone: loss of the local platform and every enrolled authenticator.

AI identity is a later expansion, not an excuse to broaden the first product. Agents and workloads need cryptographic identity and delegated organizational authority rather than government identity proof. The reusable ProofAgain assets are policy, quorum approval, lifecycle, destination-bound reissuance, revocation, continuity, and audit.

## Evidence required

No market-size number should be treated as credible until the unit of demand is clear. Early research should establish:

- annual rate and severity of unrecoverable lockout by application category;
- support cost and churn attributable to high-assurance recovery cases;
- number of users who generate but do not safely retain backup codes;
- willingness of security teams to delegate part of the recovery ceremony;
- willingness to pay by users, applications, and enterprises;
- expected recovery-event frequency and identity-proofing cost;
- which object types create unacceptable liability;
- jurisdictions suitable for a bounded pilot; and
- whether users trust a specialized recovery provider enough to enroll.

## Early validation interviews

Interview groups should include:

- people who permanently lost an important account;
- people who recovered only through an exceptional support decision;
- password-manager and security-key customers;
- authentication, trust-and-safety, support, and privacy leaders;
- cyber insurers and incident-response professionals;
- identity-verification providers;
- enterprise IAM administrators; and
- regulators or specialist counsel in the first operating jurisdiction.

Useful interview questions focus on observed behavior:

- What exactly was lost, and which recovery paths failed?
- What did recovery cost in time, money, support effort, or business interruption?
- Which exception ultimately restored access?
- What would have made that exception unsafe if used by an attacker?
- When were backup credentials last generated or tested?
- Who would be trusted to approve a recovery, and under what delay?
- What evidence would make the user or application refuse recovery?

## Opportunity boundaries

ProofAgain should not attempt to solve every form of digital custody at launch. The following should remain out of the initial market:

- cryptocurrency seed phrases and bearer assets;
- unrestricted signing keys;
- non-rotatable credentials with unlimited authority;
- large personal backups;
- everyday login or identity federation;
- recovery based on a name, identifier, document image, email, or telephone number alone; and
- applications unable to revoke or rotate recovered material.

Narrow scope makes security policy, liability, and customer expectations more legible.
