# Product and experience

## Product definition

ProofAgain is a managed lifecycle for encrypted recovery objects. It combines:

- an application and client integration;
- local encryption;
- durable object storage;
- identity binding;
- high-assurance recovery;
- fraud controls and delayed release;
- receipt, rotation, revocation, expiration, migration, and deletion; and
- an inventory that can be rediscovered after all devices are lost.

It is not a normal login method and should rarely be used.

## Product surfaces

### Application SDK

Allows a partner application to create, encrypt, deposit, replace, revoke, and verify the status of a recovery object. The SDK returns an opaque object reference and signed storage receipts.

### User enrollment experience

Explains what is protected, which recovery policy applies, which parties participate, how long recovery will take, and what data is retained. It confirms that storage completed and gives the user a human-readable policy summary.

### Recovery client

Runs on a new device, generates an ephemeral recovery key pair, submits the public key, shows request status, receives provider responses, reconstructs any threshold key, decrypts the object locally, and guides the user through rotation.

### Provider service

Stores encrypted envelopes and participates in verification, policy evaluation, notification, approval, and release. A provider may perform only some of these functions in a multi-provider network.

### Partner and risk console

Lets authorized operators view opaque request state, evidence provenance, policy decisions, alerts, and audit events without exposing recovery plaintext.

## Primary personas

### Protected user

Wants confidence that a catastrophic event will not permanently erase access. Their primary need during enrollment is clarity; during recovery it is a predictable, respectful process under stress.

### Recovering claimant

May have no old device, email, telephone number, backup code, or memory of object identifiers. The product must not assume access to a channel whose loss triggered recovery.

### Application security owner

Needs strong guarantees about scope, revocation, auditability, and the fact that ProofAgain cannot use a recovered token for unrelated access.

### Fraud reviewer

Needs structured evidence, explicit policy, separation of duties, escalation paths, and the ability to deny or pause without handling recovery plaintext.

### Enterprise approver

Needs recovery to satisfy both identity requirements and organizational authorization.

## Enrollment journey

1. **Offer protection.** The application presents “Protect my recovery codes” when it creates or rotates recovery material.
2. **Explain the policy.** The user sees the providers, required quorum, minimum delay, notification channels, and assurance level.
3. **Confirm identity binding.** The user enrolls or links an already verified ProofAgain identity. The application receives only a pseudonymous confirmation.
4. **Encrypt locally.** The application or client generates a random data-encryption key, encrypts the object, and prepares provider-wrapped recovery capability.
5. **Deposit.** The encrypted envelope and provider payloads are uploaded.
6. **Verify receipts.** The client validates signed provider receipts before reporting success.
7. **Record the reference.** The application retains the opaque object identifier, current version, and receipts.
8. **Remind and test.** Periodic status checks confirm that the object remains active and recoverable without decrypting it.

Enrollment must never report success before the required receipts are valid and durable.

## Recovery journey

1. **Start without an object ID.** The claimant installs the recovery client and begins with an identity claim or approved electronic identity.
2. **Generate a destination key.** The client creates a temporary recovery key pair and protects the private key locally.
3. **Resolve the person record.** ProofAgain maps the claim to one stable identity reference without revealing an inventory.
4. **Collect evidence.** The claimant completes the policy's document, biometric, electronic identity, in-person, organizational, or trusted-contact steps.
5. **Assess risk.** The system evaluates evidence provenance, document history, geography, behavioral indicators, recent identity changes, and known identity-theft flags.
6. **Notify and wait.** Every registered surviving channel and existing authenticator receives a notice. A policy-defined delay begins.
7. **Allow cancellation.** Any approved surviving factor can cancel or freeze the request.
8. **Approve by quorum.** Required providers and reviewers issue signed approvals.
9. **Release to the new device.** Provider responses are encrypted to the recovery client's public key.
10. **Discover authorized objects.** The client decrypts labels and shows only objects covered by the completed policy.
11. **Recover locally.** The client reconstructs the data-encryption key and decrypts the selected object.
12. **Rotate immediately.** Where supported, the application exchanges the recovered capability for a new authenticator and invalidates the recovered object.
13. **Close and audit.** The request is sealed with a tamper-evident event record, and all parties receive an outcome notification.

The flow should make delay and review feel like evidence of protection, not unexplained friction.

## Lifecycle journey

Recovery material changes even when no recovery occurs:

- a new version replaces rotated backup codes;
- an application revokes an object after account closure;
- an object expires automatically;
- storage receipts are revalidated;
- a user moves from one provider group to another;
- a provider key or cryptographic suite is rotated;
- an abandoned subscription enters a defined retention and notice process; and
- an object is securely deleted subject to policy and legal retention.

Every state transition should be explicit, authenticated, idempotent, and visible to the issuing application.

## Inventory and discovery

Discovery is a core product benefit. A claimant who has forgotten every deposit location should still be able to find authorized objects after identity verification.

Before authorization, providers should see only minimized routing data and opaque identifiers:

```text
object-7f02a
object-a118c
object-d93b4
```

After authorization, the new device can decrypt labels:

```text
Git hosting backup codes
Password manager emergency key
Primary email recovery token
```

Inventory access itself is sensitive. The system should avoid confirming whether a person is enrolled or which applications they use until the relevant authorization threshold has been met.

## Assurance tiers

Exact policies require risk and legal review, but the product needs a comprehensible tier model.

| Illustrative tier | Suitable objects | Possible controls |
| --- | --- | --- |
| Standard | Rotatable website backup codes | Strong document/eID proof, liveness or equivalent, notifications, short mandatory delay |
| Enhanced | Password-manager or developer recovery | Two independent verification decisions, longer delay, manual risk review |
| Organizational | Enterprise break-glass token | Enhanced identity proof plus designated organizational quorum |
| Exceptional | High-impact, narrowly approved cases | In-person proofing, multi-provider threshold, extended delay and investigation |

No tier should rely on a national identifier, email, telephone number, knowledge questions, or a document image alone.

## MVP scope

### Included

- one partner application and one synthetic reference integration;
- one recovery-object type with a small size limit;
- client-side authenticated encryption;
- a managed single-provider protected-key path;
- stable internal identity references;
- one documented proofing policy in one jurisdiction;
- signed storage receipts;
- object replacement, revocation, expiration, and deletion;
- delayed recovery, notification, cancellation, and manual review;
- local decryption to a newly generated device key;
- append-only security event records; and
- a complete disaster-recovery and provider-exit exercise.

### Excluded

- cryptocurrency and bearer-asset recovery;
- arbitrary private-key custody;
- global identity coverage;
- automatic approval of high-risk cases;
- succession and inheritance;
- open enrollment by unsupported third-party clients;
- claims of zero trust or guaranteed identity;
- recovery without a waiting period; and
- a marketplace of providers before the core ceremony is proven.

## Functional requirements

- Applications can create, replace, revoke, inspect, and delete an opaque object.
- Providers sign receipts over the exact object version and policy.
- A recovery request is bound to a fresh device public key.
- Policy cannot be weakened during an active recovery.
- All approvals and releases are scoped to a request, object version, destination key, and expiry.
- Existing approved factors can cancel or freeze a request.
- A recovered token can be marked consumed and replaced.
- Applications can detect stale or superseded objects.
- Users can migrate without exposing plaintext to providers.
- Operators cannot retrieve recovery plaintext through administrative interfaces.

## Non-functional requirements

- Clear cryptographic and policy versioning.
- Algorithm agility without silent downgrade.
- Durable, independently verifiable receipts.
- Strong separation between identity data and object storage.
- High availability for status and revocation, with deliberately slower recovery.
- Accessible recovery for users under stress or with changed documents.
- Internationalization for names, identifiers, scripts, and identity systems.
- Observability that does not log secrets or unnecessary personal data.
- Tested backup, restore, key rotation, and provider-exit procedures.
- A support model that cannot bypass recovery policy.

## Product principles

- **Do not promise instant recovery.** Speed and high assurance are in tension.
- **Do not make the user remember the object identifier.** Discovery is part of the value.
- **Do not expose a person's account inventory during lookup.**
- **Do not allow support agents to improvise weaker recovery.**
- **Do not retain evidence merely because it may be useful later.**
- **Do not recover more authority than the application needs.**
- **Make status legible.** Users and applications should know whether an object is current, stale, revoked, or awaiting replacement.
- **Design the failure experience first.** Lost devices, changed names, expired documents, provider outages, accessibility needs, and contested identity must be normal test cases.
