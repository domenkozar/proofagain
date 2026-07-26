# Protocol and integrations

## Protocol objective

Applications should integrate once and allow users to choose a compatible recovery deployment: a managed provider, an independent threshold provider group, or an enterprise-managed group.

The protocol should standardize:

- provider and key discovery;
- recovery-object envelopes;
- provider-specific recovery payloads;
- identity-binding references;
- signed storage receipts;
- object state and lifecycle operations;
- recovery-request authorization;
- destination-key registration;
- delay, cancellation, approval, and release;
- provider migration;
- audit commitments; and
- secure deletion attestations where meaningful.

The protocol must not standardize all providers into one risk model. Providers can support different jurisdictions and assurance capabilities while using interoperable messages.

## Roles

| Role | Responsibility |
| --- | --- |
| Issuer | Creates the recovery material and can validate, rotate, or revoke it |
| Client | Encrypts at enrollment and decrypts at recovery |
| Storage provider | Persists envelopes and returns receipts |
| Recovery provider | Holds or can transform a recovery share |
| Identity verifier | Produces signed proofing results |
| Policy authority | Defines and evaluates release requirements |
| Application | Exchanges recovered capability for restored account access |
| Auditor | Verifies controls, logs, and provider conformance |

One organization may fill several roles initially, but the wire model should keep them distinct.

## Provider discovery

A signed provider document should publish:

```text
provider_id
display_name
legal_operator
jurisdictions
protocol_versions
cryptographic_suites
public_keys_and_purposes
assurance_capabilities
identity_verification_methods
supported_threshold_roles
service_endpoints
status_endpoint
key_transition_proofs
policy_documents
```

Clients need an authenticated root for discovery. Domain TLS alone may not be sufficient for long-term key continuity; the specification should define pinned trust, signed directory updates, and emergency key transition.

## Recovery-object model

### Inner object

The encrypted application-independent payload should support:

- format version;
- application and object type;
- account hint;
- creation and expiration;
- recovery material;
- rotation or consumption instructions;
- display label and content type; and
- application signature.

The account hint and label should normally remain encrypted because they reveal where the person has accounts.

### Outer envelope

The storage envelope should contain only:

- protocol and cryptographic versions;
- opaque object and version identifiers;
- provider-set and policy references;
- ciphertext and provider payload references;
- operational expiration;
- integrity commitments; and
- issuer authentication.

Providers must reject unknown critical fields and ambiguous encodings.

## Object types

The initial registry could define:

| Type | Expected post-recovery behavior |
| --- | --- |
| `backup_code_set` | Consume one code or rotate the entire set |
| `application_recovery_token` | Exchange once for a new authenticator |
| `password_manager_emergency_key` | Restore access and rotate key material |
| `passkey_registration_authorization` | Register one replacement passkey, then expire |
| `enterprise_break_glass_token` | Require organizational approval and immediate replacement |
| `small_emergency_document` | Display locally under explicit retention policy |

Extensible types should include authority and lifecycle semantics, not merely a MIME type.

## Application integration flow

1. The application requests a supported provider-set document.
2. The user selects a recovery option and reviews its policy.
3. The application generates a narrow recovery object.
4. The SDK encrypts the object locally and uploads the envelope.
5. Providers return signed storage receipts.
6. The SDK validates the receipt quorum.
7. The application stores the opaque object ID, current version, policy digest, and receipts.
8. The application periodically validates status.
9. Rotation creates a new monotonic version and supersedes the old one.
10. Account closure revokes or deletes the object under an authenticated lifecycle request.

An application must not treat a successful upload without valid receipts as protected.

## Illustrative application API

The final API may differ, but the resource model should be small and idempotent:

```text
GET    /provider-sets/{provider_set_id}
POST   /objects
GET    /objects/{object_id}/status
PUT    /objects/{object_id}/versions/{version}
POST   /objects/{object_id}/revoke
POST   /objects/{object_id}/delete
POST   /objects/{object_id}/migrate
```

Recovery is intentionally separate:

```text
POST   /recovery-requests
POST   /recovery-requests/{request_id}/destination-key
GET    /recovery-requests/{request_id}/status
POST   /recovery-requests/{request_id}/cancel
POST   /recovery-requests/{request_id}/evidence
POST   /recovery-requests/{request_id}/approvals
GET    /recovery-requests/{request_id}/responses
```

Operations that mutate state should accept an idempotency key and return a signed state commitment where appropriate.

## Receipt semantics

A receipt should let a client prove:

- which provider accepted the object;
- the precise envelope and policy digests;
- the accepted object version;
- when acceptance occurred;
- which provider key signed; and
- how long the receipt is expected to remain valid.

A receipt should not imply that the underlying application credential is still valid. Application-issued status and invalidation messages remain authoritative for that credential.

## Version replacement

Replacement should be transactional:

1. upload and receive receipts for the new version;
2. verify that the required provider quorum accepted it;
3. atomically mark the new version active;
4. mark the prior version superseded;
5. notify the issuer and user of the resulting state; and
6. retain or delete prior ciphertext according to policy.

If the flow fails before quorum, the previous active version remains unchanged.

## Revocation and deletion

Revocation prevents future release and should be fast, durable, and independently visible. Deletion removes retained material according to policy and legal constraints and may be delayed.

The protocol should distinguish:

- **revoked:** cannot be recovered;
- **deletion pending:** removed from active systems but still within a defined retention process; and
- **deleted:** provider attests that covered copies and key material are no longer retained, subject to explicitly disclosed exceptions.

The product must not promise cryptographic erasure unless key and backup architecture actually provides it.

## Recovery request

A request should be scoped to:

- one claimant identity reference;
- one destination public key;
- a policy and minimum assurance;
- an object set or permitted discovery scope;
- initiation, not-before, and expiration times;
- specific provider participants; and
- a unique request nonce.

Providers sign every approval or denial. The client accepts recovery responses only if it can validate the full policy quorum and destination-key binding.

## Application handoff

The safest object is a one-time, minimum-authority capability. For a non-exportable passkey, the application can deposit authorization to:

- register one new passkey;
- reset a defined set of authenticators;
- enter a restricted account-repair session; or
- exchange for a short-lived recovery session.

The capability should expire quickly, be single-use, and require the application to create fresh normal authenticators. ProofAgain does not need to extract hardware-bound private keys.

## Application privacy boundary

The application may receive:

```text
unique_person_verified: true
recovery_identity_reference: rp_7fa9c2...
assurance_policy: enhanced-v1
```

It should not receive:

- national identifiers;
- identity-document images or numbers;
- biometric samples or templates;
- unrelated ProofAgain applications;
- proofing-vendor raw results; or
- the claimant's full identity history.

Likewise, an identity verifier does not need application labels or recovery plaintext.

## Provider independence metadata

A provider set should disclose relationships that can create correlated failure:

- legal ownership;
- key-hosting operator;
- cloud and region;
- identity-proofing vendor;
- risk-decision service;
- audit firm;
- critical subcontractors; and
- jurisdiction.

A client or policy engine can then reject a nominal threshold whose members share too many dependencies.

## Compatibility and conformance

An open protocol needs more than a published document. It should include:

- reference test vectors;
- a deterministic parser test suite;
- malicious and ambiguous message cases;
- provider and client conformance profiles;
- cryptographic-suite lifecycle policy;
- interoperability events;
- a compatibility mark with revocation rules; and
- public security advisories.

Conformance should describe what was tested. It must not imply that a provider's identity decisions or operations are universally trustworthy.

## Governance direction

The commercial company can develop the first implementation, but long-term adoption may benefit from:

- a publicly reviewable specification;
- transparent change proposals;
- independent security participation;
- intellectual-property terms that allow compatible implementation;
- clear control of registries and namespaces;
- an emergency security-update process; and
- eventual governance not dependent on the survival of one provider.

Opening the protocol too early can freeze mistakes. The staged approach should publish design and threat assumptions early, validate the ceremony, then stabilize wire compatibility after independent implementations exist.
