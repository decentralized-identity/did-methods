# DID method recommendation proposal: did:cid

This is a proposal to include `did:cid` in the set of DID methods recognized and
recommended by the DIF DID Methods WG.

## Description

The `did:cid` method leverages **Content IDentifiers (CIDs)** — self-describing,
cryptographic hashes used by IPFS and other content-addressable systems — to
create updatable, globally unique, instantly available decentralized identifiers
with zero blockchain transaction costs at creation time.

### Core Innovation: Separation of Creation and Updates

The fundamental insight behind `did:cid` is that DID **creation** and DID
**updates** have fundamentally different requirements:

| Requirement      | Creation               | Updates              |
| ---------------- | ---------------------- | -------------------- |
| Speed            | Immediate              | Can tolerate latency |
| Cost             | Must be zero/near-zero | Can tolerate fees    |
| Decentralization | No gatekeepers         | Consensus acceptable |
| Finality         | Not required           | Required             |

By separating these concerns, `did:cid` achieves optimal characteristics for
each:

- **Identity Creation (CAS)**: Instant (<1 second), zero cost,
  content-addressed, globally available, no gatekeepers
- **Identity Updates (Registry)**: Ordered by registry, cryptographically signed,
  consensus-verified, auditable history, finality guarantees

### Multi-Registry Architecture

Rather than mandating a single consensus mechanism, `did:cid` supports multiple
registries with different characteristics. Users select their registry at DID
creation based on their specific requirements:

| Registry    | Speed   | Cost            | Finality | Best For                      |
| ----------- | ------- | --------------- | -------- | ----------------------------- |
| Hyperswarm  | Seconds | Free            | Eventual | Development, internal systems |
| Bitcoin     | ~60 min | ~$0.001/batch   | Strong   | Enterprise, legal identity    |
| Feathercoin | ~15 min | ~$0.00001/batch | Strong   | Cost-sensitive applications   |

DIDs can also migrate between registries after creation (e.g., from Hyperswarm
to Bitcoin) as requirements evolve, without changing the DID identifier itself.

### DID Lifecycle

```text
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│   CREATE    │───▶│   UPDATE    │───▶│   RESOLVE   │
│  (via CAS)  │    │ (Registry)  │    │ (Any Node)  │
└─────────────┘    └─────────────┘    └─────────────┘
      │                  │                   │
      ▼                  ▼                   ▼
   Instant           Batched to          Reconstruct
   Global           Blockchain           DID Document
   Free             (optional)           from history
```

All `did:cid` identifiers begin life anchored to a Content-Addressable Storage
(CAS) network such as IPFS. The CID itself is derived from the initial DID
Document, making the identifier self-certifying. Updates are registered on a
user-selected registry that provides ordering guarantees.

### How Gatekeeper Builds a did:cid Document

`did:cid` resolution is deterministic replay of an accepted operation chain.
Operations from clients, peer gossip, and registry mediators are validated at
import time — accepted, merged, deferred, replaced, or rejected — into a
per-DID event chain. Resolution then replays the stored chain into a
`didDocument` / `didDocumentMetadata` / `didDocumentData` /
`didResolutionMetadata` result.

![Gatekeeper operation import and DID resolution infographic](https://raw.githubusercontent.com/archetech/archon/main/docs/presentations/gatekeeper-resolution-infographic.png)

A narrative walkthrough of the same pipeline (gates, outcomes, replay options
including `versionTime`, `versionSequence`, `confirm`, `verify`) is in
[`gatekeeper-resolution-infographic.md`](https://github.com/archetech/archon/blob/main/docs/presentations/gatekeeper-resolution-infographic.md).

### Relationship to did:mdip

The `did:cid` method evolved from the MDIP (MultiDimensional Identity Protocol)
implementation. While sharing architectural concepts, `did:cid` represents a
specification refinement focused on:

1. **Clearer naming**: "Content IDentifier" explicitly describes the
   cryptographic foundation
2. **W3C alignment**: Tighter conformance with DID Core specification, W3C JWE
   standard for encryption, and W3C VC Data Model v2 for credentials
3. **Simplified resolution**: Streamlined DID Document format
4. **Production infrastructure**: Public nodes, universal resolver integration,
   production tooling

## Existing Materials

### Specifications

- [DID Scheme Specification](https://archetech.com/protocol.html)
- [Gatekeeper API (OpenAPI)](https://github.com/archetech/archon/blob/main/docs/gatekeeper-api.json)
- [Keymaster API (OpenAPI)](https://github.com/archetech/archon/blob/main/docs/keymaster-api.json)
- [`did:cid` Technical Presentation](https://github.com/archetech/archon/blob/main/docs/presentations/did-cid-technical-presentation.md)
  — slide-level walkthrough of the method: agent vs. asset DIDs, create/update/delete
  operations, the resolution algorithm, temporal proof verification, registry
  trade-offs, and Archon node architecture.

### Reference Implementations

- [Archon Protocol Repository](https://github.com/archetech/archon) (MIT License)
- **TypeScript / Node.js** — original reference implementation. NPM packages:
  `@didcid/gatekeeper`, `@didcid/keymaster`, `@didcid/cipher`.
- **Python Keymaster** — native Python library, service, and CLI. Landed in
  Archon [PR #455](https://github.com/archetech/archon/pull/455); CLI merged
  into the library in [PR #480](https://github.com/archetech/archon/pull/480);
  prepared for PyPI in [PR #483](https://github.com/archetech/archon/pull/483).
  Maintains drop-in parity with the TypeScript Keymaster and exposes
  `http_requests_total` / `http_request_duration_seconds` /
  `service_version_info` for observability.
- **Rust Gatekeeper** — native Rust Gatekeeper service. Landed in Archon
  [PR #404](https://github.com/archetech/archon/pull/404), with hot-path
  performance work in [PR #425](https://github.com/archetech/archon/pull/425)
  (removed full-DB scan from the DID write path).

### Production Infrastructure

- **Gatekeeper API**:
  [Ready check](https://archon.technology/api/v1/ready)
- **Universal Resolver Driver**:
  [resolver.archon.technology](https://resolver.archon.technology)
- **DID Explorer**:
  [explorer.archon.technology](https://explorer.archon.technology)
- **Web Wallet**:
  [wallet.archon.technology](https://wallet.archon.technology)
- **Naming Service**: [archon.social](https://archon.social)
- **Public Demo Node**: [4tress.org](https://4tress.org) (independent
  deployment, "Gondor" node)

### Client Implementations

- Web Wallet (React)
- Chrome Extension
- Firefox Extension
- Android App (Capacitor)
- CLI (`@didcid/archon`)
- TypeScript/JavaScript SDK
- Python SDK

## Meeting the selection criteria

Document here how this DID method meets the
[DID method selection criteria](../selection-criteria/).

| **Criteria** | **Details** |
| ------------ | ----------- |
| **Alignment with DID Core specification** | [Yes](https://archetech.com/protocol.html). Full conformance with W3C DID Core 1.0. Encryption uses W3C JWE standard. Credentials conform to W3C VC Data Model v2. |
| **Security and privacy features** | Yes. Ed25519/secp256k1 keys, W3C JWE encrypted DID documents, selective disclosure via challenge/response. |
| **Scalability and performance** | Yes. CAS-based creation scales infinitely. Multi-registry architecture allows throughput/cost optimization. Benchmarked DID resolution performance. |
| **Ease of implementation and use** | Yes. Docker deployment in minutes. NPM packages for JS/TS. Python SDK. REST APIs for any language. |
| **Community adoption and support** | Growing. ~8,000 DIDs registered. Production deployments at archon.social and 4tress.org. Integration with AI agent ecosystems. |
| **Compliance with relevant regulations and best practices** | Yes. Standard cryptographic libraries, auditable operations, GDPR-compatible (user-controlled data). |
| **Global government-approved crypto** | Yes. Ed25519, secp256k1, AES-256-GCM — all widely approved algorithms. |
| **Privacy-preserving crypto** | Yes. Keys generated locally. Challenge/response enables selective disclosure. No correlation through resolution. |
| **Digitally signed cryptographic log of changes to the DID Document** | Yes. Each update is signed and ordered by registry. Full history reconstructable. Time-travel resolution to any version. |
| **Multi-factor binding to DNS** | Optional via `did:web` alsoKnownAs linking. Not required for base method. (see [archon.technology did:web](https://explorer.archon.technology/search?did=did:web:archon.technology)) |
| **Specification with multiple implementers** | Yes. TypeScript/Node.js reference implementation, plus native **Python Keymaster** ([PR #455](https://github.com/archetech/archon/pull/455), prepared for PyPI in [PR #483](https://github.com/archetech/archon/pull/483)) and native **Rust Gatekeeper** ([PR #404](https://github.com/archetech/archon/pull/404)). Multiple independent node operators (archon.technology, 4tress.org). |
| **Scope/domain of the types of entities/subjects addressed/named by a particular method** | Universal: humans, organizations, AI agents, IoT devices, credentials, assets. |
| **Estimate of the daily transaction volume of each scope/domain** | Current: ~8,000 DIDs registered, growing. Target: millions (AI agent identity market). |
| **DID Methods that do not serve the needs of a particular company or government** | Yes. Open protocol, MIT licensed, no vendor lock-in. Multiple registries prevent single-party control. |
| **Governance: Clear frameworks for updates, dispute resolution, and decision-making** | OSS governance via GitHub. Protocol changes through community RFC process. |
| **Usability: Simple implementation for developers** | Yes. Full node deployment in <5 minutes. SDK available on NPM and PyPI. REST API for all operations. |
| **Sustainability: Energy efficiency and eco-friendly infrastructure** | Yes. Nodes run on Raspberry Pi (8GB RAM). No proof-of-work required for DID creation. |
| **Economic Feasibility: DIDs costs of use must be reasonable** | Yes. DID creation is FREE. Updates optionally batched to blockchain (~$0.001/batch). Built-in Lightning Network integration enables DID-to-DID micropayments for services. |
| **Legal Recognition: Cross-border frameworks for DID acceptance** | Compatible with eIDAS, W3C VC ecosystem. No jurisdiction-specific requirements. |
| **Revocation and Recovery: Decentralized mechanisms for key rotation and DID recovery** | Yes. BIP-39 HD wallet recovery. Per-DID key rotation. Controller-based recovery. Registry migration without identity loss. |
| **Emerging Markets: Offline-friendly, low-bandwidth** | Yes. Local Gatekeeper caches enable offline resolution. Low-power device support. |
| **Long-lived DIDs needed for long-lived VCs** | Yes. Registry-backed DIDs provide permanent audit trail. Time-travel resolution available. Optional Bitcoin anchoring for timestamped immutability. |
| **Low and predictable marginal cost at scale (millions of accounts)** | Yes. Creation is free. Storage costs scale with CAS infrastructure (IPFS pinning ~$0.01/GB/month). |
| **Ability to create and update identifiers rapidly (within seconds)** | Yes. Creation: <1 second. Hyperswarm updates: seconds. Blockchain updates: batched. |
| **Support for key rotation** | Yes. Each DID supports independent key rotation with full history. |
| **Reliable and predictable-latency operation, for updating and resolving** | Yes. Local Gatekeeper DB (SQLite/Redis/MongoDB). Resolution: <100ms typical. |
| **Resolution should not require additional state or context** | Yes. Each Gatekeeper independently maintains and validates DID state. |
| **DIDs are permanent and immutable account identifiers** | Yes. CID-based identifiers are permanent. Document updates don't change the DID. |
| **Consider support for various DID Traits: <https://identity.foundation/did-traits/>** | Supports: Decentralized, Persistent, Cryptographically Verifiable, Resolvable. |
| **Consider categories defined by DID Rubric: <https://www.w3.org/TR/did-rubric/>** | Category: Decentralized (no single point of control or failure). |
| **Who WANTS to standardize the DID method and commits to doing the work?** | Archetech (archetech.com) — Christian Saucier, David Cypher. Committed to spec development and maintenance. |
| **Are there AT LEAST two WG members who support standardization of a DID method?** | Seeking WG member support through this proposal. |
| **Are there no trademark or IP issues?** | Yes. MIT License. "Archon" trademark held by Archetech for protocol branding only. |
| **What type of DID method is this?** | Decentralized |

## Is this DID method already involved in a standardization process? If so, where?

The predecessor protocol (MDIP) has a separate DIF proposal (`did:mdip`). The
`did:cid` method represents an evolution with distinct identifiers and refined
specification. This proposal seeks independent standardization for `did:cid`
while acknowledging shared architectural heritage.

The Universal Resolver driver for `did:cid` has been submitted for inclusion in
the DIF Universal Resolver.

## Supporting use cases

### 1. AI Agent Identity

AI agents need verifiable identity to build trust with other agents and
services. `did:cid` provides:

- Instant identity creation (agents can self-provision)
- Verifiable credentials for capability attestation
- Challenge/response authentication without passwords
- DID-to-DID Lightning micropayments for agent services

### 2. Decentralized Naming (archon.social)

Human-readable `@names` mapped to DIDs with verifiable ownership credentials.

### 3. Enterprise SSO

"Sign in with Archon" — OAuth 2.0 compatible authentication using DID
challenge/response. No password databases, no vendor lock-in.

### 4. Verifiable Credentials

Issue and verify W3C Verifiable Credentials with:

- Credential DIDs for revocation checking
- Schema DIDs for interoperability
- Selective disclosure via challenge/response
- Any URI as credentialSubject.id (W3C VC Data Model v2 compliant)

### 5. Decentralized Messaging (D-Mail)

End-to-end encrypted messaging using DID-based addressing and W3C JWE key
exchange.

### 6. Privacy-Preserving Voting

Anonymous voting with verifiable eligibility using group credentials and spoil
ballots.

## Contact

- **Organization**: Archetech ([archetech.com](https://archetech.com))
- **Primary Contact**: Christian Saucier
- **GitHub**: [github.com/archetech/archon](https://github.com/archetech/archon)
- **Infrastructure**:
  [archon.technology](https://archon.technology)
