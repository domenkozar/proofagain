# Technical architecture

## Architecture goals

The system should:

- preserve recovery after all user-held devices and secrets are lost;
- keep recovery-object plaintext off provider application systems;
- prevent one provider from unilaterally releasing high-value objects in the target architecture;
- bind every release to a specific approved request and newly generated device key;
- separate identity, storage, policy, and cryptographic responsibilities;
- support receipt, replacement, revocation, migration, and deletion;
- make security-relevant actions independently auditable; and
- survive provider, key, and algorithm changes over a multi-decade horizon.

These goals reduce and distribute trust; they do not remove it. Any system that recovers after the user has retained no secret necessarily gives an external party or quorum some recovery capability.

## Trust statement

ProofAgain should make three different claims for three different deployment modes:

| Mode | Technical authority | Appropriate claim |
| --- | --- | --- |
| Client-encrypted storage only | User retains the only recovery secret | Provider cannot recover after total user-secret loss |
| Managed single provider | Protected provider environment can rewrap or decrypt | Employee and application access is constrained, but the provider has recovery authority |
| Independent threshold providers | A quorum holds sufficient recovery shares | No single provider can recover; a sufficient quorum still can |

Marketing, contracts, and user interfaces must not collapse these modes into a generic “zero knowledge” or “trustless” claim.

## Logical components

### Issuing application

Creates or rotates the underlying recovery material and defines its narrow recovery capability. It keeps an opaque object reference and validates provider receipts. It should not receive government identifiers, evidence images, biometrics, or provider private keys.

### Enrollment client or SDK

Generates a data-encryption key, encrypts the object and sensitive metadata, prepares provider-specific key material, verifies receipts, and returns only the necessary integration state to the application.

### Recovery client

Generates the destination key pair, protects the private key locally, participates in the approved request, verifies signed responses, reconstructs the data-encryption key, decrypts locally, and guides post-recovery rotation.

### Object store

Stores opaque encrypted envelopes and version state. It should not share an administrative plane or direct identifiers with the identity system.

### Identity service

Maintains the link between an internal person reference and verified identity history. It supports continuity across document expiration, reissue, name changes, nationality changes, and provider migrations.

### Verification and risk orchestrator

Collects evidence from approved proofing channels, evaluates recovery policy, coordinates manual review, sends notifications, applies delays, and produces signed decisions.

### Cryptographic release service

Performs protected unwrap/rewrap or threshold-share release only after validating a complete authorization package. Its interface should be narrow and incapable of modifying recovery policy.

### Audit and transparency service

Records append-only security events, anchors or signs checkpoints, supports independent review, and emits aggregate transparency reporting without exposing object contents.

### Provider directory

Publishes provider identities, supported protocol and cryptographic versions, public encryption keys, jurisdictions, assurance capabilities, status, and key-transition proofs.

## Data classes and separation

| Data class | Examples | Preferred boundary |
| --- | --- | --- |
| Recovery ciphertext | Encrypted backup codes or recovery token | Object store |
| Provider recovery payload | Wrapped data key or encrypted key share | Provider-specific storage |
| Identity record | Internal person reference, identity history | Identity service |
| Raw evidence | Document images, video, biometric sample | Short-lived proofing boundary |
| Derived evidence | Validation result, issuer, timestamps, confidence and provenance | Verification record |
| Policy state | Assurance tier, quorum, delay, allowed proofing methods | Policy service |
| Application metadata | Encrypted label and account hint | Inside object ciphertext |
| Audit event | Request, decision, release, cancellation, rotation | Append-only audit service |

Access should be separately authorized and logged. A storage operator should not be able to browse identity records; an identity verifier should not learn object contents or unnecessary application labels.

## Cryptographic objects

### Recovery object plaintext

An application-independent inner object may include:

```text
format_version
application_identifier
account_hint
created_at
expires_at
object_type
recovery_material
rotation_policy
display_label
application_signature
```

The entire structure is sensitive unless a field is explicitly required for outer-envelope routing.

### Encrypted envelope

An illustrative outer envelope may include:

```text
protocol_version
object_id
object_version
provider_set_id
policy_id
ciphertext
encryption_suite
provider_payload_references
created_at
operational_expiry
issuer_key_id
issuer_signature
```

The envelope should disclose only what providers need to store, route, expire, and revoke it. Exact encoding, canonicalization, associated data, size limits, and signature semantics belong in a versioned specification.

### Storage receipt

Each provider signs a commitment to at least:

```text
protocol_version
provider_id
object_id
object_version
envelope_digest
policy_digest
accepted_at
receipt_expiry
provider_key_id
```

Receipts prove acceptance, not perpetual availability. Status checks and continuity mechanisms remain necessary.

## Target threshold enrollment

1. The client obtains a signed provider-set description and verifies provider keys and policy.
2. It creates the recovery-object plaintext and a cryptographically random data-encryption key (DEK).
3. It encrypts the object with an approved authenticated-encryption scheme, binding immutable outer fields as associated data.
4. It divides recovery capability into an approved threshold, for example two of three provider shares.
5. It encrypts each share to the corresponding provider's current public key.
6. It uploads the common envelope and provider-specific encrypted share payloads.
7. Each provider validates format and policy, persists its material, and returns a signed receipt.
8. The client validates the complete receipt quorum before declaring enrollment successful.
9. The issuing application stores the opaque object ID, version, policy reference, and receipts.
10. The client destroys transient plaintext and key material according to the platform's capabilities.

Threshold construction, share verification, commitment scheme, randomness, and key encapsulation require expert selection and independent cryptographic review. A familiar primitive does not by itself make the composed protocol safe.

## Target threshold recovery

1. The recovery client generates a fresh, request-specific destination key pair.
2. The claimant begins a request without needing to know object IDs.
3. The identity service resolves the claimed stable person record without disclosing enrollment.
4. Verification services collect policy-required evidence and signed results.
5. The risk orchestrator creates an authorization package containing request ID, claimant reference, destination public key, policy, scope, timestamps, and evidence commitments.
6. Notifications are sent and the mandatory waiting period begins.
7. Cancellation, identity-theft reports, policy changes, or risk signals can freeze the request.
8. After the delay, independent providers validate the authorization package and make independent approval decisions.
9. Each approving cryptographic service releases only its request-scoped response, encrypted to the destination public key.
10. The client verifies provider signatures and policy quorum, decrypts the responses, reconstructs the DEK, and decrypts the object locally.
11. The issuing application rotates or exchanges the recovered credential.
12. Providers mark the request closed and record whether the object was consumed, superseded, or retained.

Every provider response must be non-replayable and bound to the object version, request, destination key, policy, and expiration.

## Initial single-provider architecture

An initial managed product can reduce implementation complexity:

1. The protected cryptographic environment generates a non-exportable recovery key.
2. Clients encrypt or wrap recovery material to its public key.
3. Ciphertext is stored outside the protected boundary.
4. A completed authorization package and fresh device public key are submitted.
5. The protected environment validates authorization, decrypts and immediately re-encrypts or rewraps to the device key.
6. The response is returned to the recovery client.

Required controls include:

- HSM or confidential-computing attestation where meaningful;
- dual control for policy and key-administration changes;
- no general-purpose plaintext output path;
- request-, policy-, destination-, and time-bound authorization;
- rate limits and immutable audit events;
- tested key backup and restore;
- externally reviewed code at the protected boundary; and
- explicit disclosure that the provider has technical recovery authority.

This is a product stage, not the target security architecture for the highest-value objects.

## Recovery authorization package

A provider should not accept an informal “verification passed” flag. The authorization package should be signed, versioned, and contain enough commitments for independent evaluation:

```text
request_id
person_reference_commitment
object_scope
object_versions
destination_public_key
policy_id_and_digest
verification_result_references
risk_decision
not_before
expires_at
cancellation_status
approver_identities
authorization_signatures
```

Raw documents or biometrics should not be copied into this package. Providers receive only the minimum evidence and provenance needed for their decision.

## Identity-reference binding

External identifiers should be normalized into a namespaced form such as:

```text
SI:EMSO:<identifier>
```

The raw value should not become an object lookup key or public username. A better internal model uses:

- a protected canonical identity record;
- provider-specific pseudonymous references;
- versioned links to historical identity documents;
- authenticated merge and correction procedures; and
- a separate application-facing pseudonym.

The design must address duplicate enrollment and erroneous merges. Merging two people is potentially more dangerous than failing to match the same person, because it can expose one person's inventory to another.

## Key hierarchy

A full design should distinguish:

- root and intermediate provider signing keys;
- provider directory and key-transition keys;
- provider share-encryption or rewrap keys;
- per-object data-encryption keys;
- request-specific destination keys;
- audit checkpoint keys; and
- application signing keys.

Each key class needs a documented owner, storage boundary, rotation interval, revocation process, compromise response, cryptoperiod, and recovery plan. One provider master key should not silently serve every purpose.

## State machines

### Object

```text
pending -> active -> superseded -> revoked -> deletion_pending -> deleted
                     \-> expired
```

### Recovery request

```text
initiated -> proofing -> risk_review -> waiting -> provider_approval
    -> released -> consumed -> closed
```

Terminal alternatives include:

```text
denied | cancelled | frozen | expired | failed
```

Transitions must be authenticated, append-only in audit history, and safe to retry. “Released” must not be inferred from a support ticket status.

## Migration

Provider migration cannot depend on plaintext exposure. Possible paths include:

- the user authorizes client-side decrypt and immediate re-enrollment while still authenticated;
- old and new provider quorums participate in a constrained cryptographic rewrap;
- a planned provider exit temporarily supports a signed migration protocol; or
- the application issues a replacement recovery object directly to the new provider set.

The last option is simplest when the user still has normal account access. Periodic migration drills should occur before a provider crisis.

## Security engineering requirements

- Use only reviewed, versioned cryptographic suites with explicit downgrade rules.
- Use a cryptographically secure random source and platform-appropriate protected key storage.
- Bind ciphertext to context with authenticated associated data.
- Canonically encode signed structures and reject ambiguous parsing.
- Make create, replace, revoke, approve, and release operations idempotent.
- Protect against rollback to a superseded object version or weaker policy.
- Avoid secret or identity data in logs, traces, metrics, crash reports, and support exports.
- Separate production access, key administration, fraud review, and software deployment.
- Test malicious clients, malicious providers, provider equivocation, and partial outages.
- Commission protocol, implementation, infrastructure, and operational reviews before handling live secrets.

## Decisions deliberately left open

The proposal does not yet select:

- the authenticated-encryption and key-encapsulation suites;
- the threshold construction;
- canonical wire encoding;
- identity-proofing vendors or biometric methods;
- confidential-computing versus HSM boundary;
- audit-log construction;
- exact data-retention periods; or
- which operations are centralized in the first release.

Those choices should follow threat modeling, jurisdiction selection, partner constraints, prototyping, and independent review—not precede them.
