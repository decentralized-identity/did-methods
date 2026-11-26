# DID method recommendation proposal: did:content

This is a proposal to include `did:content` in the set of DID methods recognized and
recommended by the DIF DID Methods WG.

**Status**: Candidate. Specification v0.2 (draft) published 2026-11-11, with a public
registry/resolver in production, two implementations and a Universal Resolver driver.
This document supersedes the v0.1 proposal (which described a Python-only prototype
without a resolver).

## Description

`did:content` identifies a piece of digital content (an image, a video, a sound
recording, a text, a model file, a dataset) rather than a person or an organisation.

The identifier is **self-certifying**: the method-specific id is a multihash of the
canonicalised genesis entry of a **DID Log**, which commits to the content bytes
(hard binding) and to the initial update keys. Every later version is a hash-chained,
signed log entry, so a resolver can verify the complete history of the DID from any
copy of the log without trusting the server that served it. The DID document carries
the content bindings, the parties (creator, rights holder, publisher, …), machine-
readable licence and royalty terms, and links to external provenance (C2PA manifests,
Verifiable Credentials, on-chain registrations).

### Motivation

Content on the Internet is identified by where it is stored (an S3 key, a platform
URL). When storage moves, the identifier breaks; when the platform changes its rules,
the creator's rights go with it. Since 2024 three separate ecosystems have converged
on needing a stable identifier for *the content itself*:

1. **Provenance** — C2PA Content Credentials are now written by cameras and preserved
   by CDNs and platforms; the EU AI Act Article 50 obligations (enforced from
   2 August 2026) make machine-readable provenance a legal requirement.
2. **Identity of the parties** — the CAWG identity assertion (DIF) re-introduced
   creator/publisher identity using X.509 or W3C Verifiable Credentials.
3. **Rights and AI usage terms** — RSL 1.0, Cloudflare Content Signals, W3C TDMRep and
   on-chain IP registries express licensing terms, each in its own silo.

`did:content` provides the missing piece: a decentralised, verifiable,
storage-independent identifier that carries (a) hard and soft bindings to the bytes,
(b) the DIDs of the parties and their roles, (c) licence/royalty terms in the
vocabularies those ecosystems already use, and (d) a verifiable history of all of the
above.

### DID Syntax

```
did-content = "did:content:" scid
scid        = "z" 1*base58char   ; multibase(base58btc, multihash(sha2-256, JCS(genesis entry)))
```

Example (public test vector, resolvable at `https://did.kataru.io`):

```
did:content:zQmbnKX58u9eGUuDCDjKxCaG48Xr375dvf81vdGZqz31ze4
```

### DID Document Structure

```json
{
  "@context": ["https://www.w3.org/ns/did/v1.1", "https://did.kataru.io/did-content/v1"],
  "id": "did:content:zQmbnKX58u9eGUuDCDjKxCaG48Xr375dvf81vdGZqz31ze4",
  "controller": ["did:key:z6MkjchhfUsD6mmvni8mCdXHw216Xrm9bQe2mBH1P5RDjVJG"],
  "verificationMethod": [{
    "id": "did:content:zQmbnKX…#key-1", "type": "Multikey",
    "controller": "did:content:zQmbnKX…", "publicKeyMultibase": "z6MkjchhfUsD6mmvni8mCdXHw216Xrm9bQe2mBH1P5RDjVJG"
  }],
  "assertionMethod": ["did:content:zQmbnKX…#key-1"],
  "capabilityInvocation": ["did:content:zQmbnKX…#key-1"],
  "content": {
    "mediaType": "image/png",
    "byteLength": 165,
    "hardBindings": [{ "digestMultibase": "zQmQoJLz2eqTpNQ7qjqTQ8bJNd24uUaH3YnHXRVmyjn4S7x" }],
    "locations": ["ipfs://bafy…", "https://cdn.example.com/sample.png"]
  },
  "parties": [
    { "id": "did:content:zQmbnKX…#party-1", "role": "creator",      "party": "did:key:z6Mk…" },
    { "id": "did:content:zQmbnKX…#party-2", "role": "rightsHolder", "party": "did:web:label.example.com" }
  ],
  "license": [{
    "id": "did:content:zQmbnKX…#license-1", "type": "RSLLicense",
    "permits":   { "usage": ["search"], "user": ["commercial", "non-commercial"] },
    "prohibits": { "usage": ["ai-train", "ai-input"] },
    "payment":   { "type": "attribution" }
  }],
  "royalty": { "recipients": [
    { "party": "did:content:zQmbnKX…#party-1", "shareBasisPoints": 8000, "payTo": "did:pkh:eip155:1:0x…" }
  ]},
  "service": [{ "id": "did:content:zQmbnKX…#delivery", "type": "ContentDelivery", "serviceEndpoint": "https://cdn.example.com/sample.png" }]
}
```

Documents never contain PII: parties are DIDs, payees are payment URIs.

### DID Log (verifiable history)

The log format is adapted from `did:webvh` 1.0: one JSON Lines entry per version with
`versionId` (`<n>-<entryHash>`), `versionTime`, `parameters` (`method`, `scid`,
`updateKeys`, `nextKeyHashes` for key pre-rotation, optional `witness`/`watchers`,
`deactivated`), the full `state` and a W3C Data Integrity proof
(`eddsa-jcs-2022`). Hard bindings are append-only: a change to the bytes is a new DID
linked by `derivedFrom`.

### Benefits

- **Self-certifying and storage-agnostic**: any registry, IPFS pin or embedded copy of
  the log can be verified offline; registries are untrusted mirrors.
- **Content-bound but updatable**: the content hash is fixed at creation; locations,
  keys, parties, licence and royalty terms evolve through signed versions.
- **Interoperable by construction**: roles follow the CAWG vocabulary, licence tokens
  follow RSL 1.0, soft-binding algorithm ids follow the C2PA registry, identifiers
  such as ISCC/ISRC/EIDR go in `alsoKnownAs`, and the log format follows `did:webvh`.
- **Standard cryptography only**: Multikey, multihash, JCS (RFC 8785), Data Integrity
  cryptosuites. No custom proof formats.
- **Reverse lookup**: registries index hard and soft bindings so a file in hand can be
  mapped back to its DID (the operation CDNs, platforms and crawlers need).

### Drawbacks / Current Limitations

- Specification is a draft (v0.2); the JSON-LD context and vocabulary may still change.
- One public production registry today (operated by Kataru Inc.); the registry
  protocol allows anyone to run one, but no independent operator exists yet.
- Witness proofs are specified but not yet implemented in the reference implementation.
- No formal security audit yet.
- Production volume is low; the method has not been exercised at the scale of
  millions of identifiers.

## Existing Materials

### Specifications

- [did:content v0.2 specification](https://github.com/KataruInc/did-content-spec)
  (ABNF, data model, DID Log, CRUD, resolution, security/privacy considerations,
  migration from v0.1), with [design rationale](https://github.com/KataruInc/did-content-spec/blob/main/docs/design-rationale.md)
  and an [interoperability guide](https://github.com/KataruInc/did-content-spec/blob/main/docs/interoperability.md)
  (C2PA/CAWG, ISCC, RSL/TDMRep, on-chain IP registries, VC 2.0).
- [JSON-LD context](https://github.com/KataruInc/did-content-spec/blob/main/contexts/did-content-v1.jsonld)
  and [JSON Schema](https://github.com/KataruInc/did-content-spec/blob/main/schemas/log-entry.schema.json).
- [W3C DID Extensions (methods) registry entry](https://www.w3.org/TR/did-extensions-methods/).

### Implementations

- **Python reference implementation** (public, standard library + `cryptography`):
  log creation, verification and resolution, CLI, unit tests, deterministic
  [test vectors](https://github.com/KataruInc/did-content-spec/tree/main/examples).
- **Go implementation** (Kataru's registry/resolver and producer library): verifies and
  creates logs; byte-for-byte interoperability with the Python vectors is enforced in
  its test suite. Operated in production at `https://did.kataru.io`.
- **Universal Resolver driver**: [KataruInc/content-did-driver](https://github.com/KataruInc/content-did-driver),
  multi-arch image `kataru/content-did-driver:0.2.0`; registration submitted as
  [decentralized-identity/universal-resolver#604](https://github.com/decentralized-identity/universal-resolver/pull/604).

### Architecture

A **registry** is any server that serves DID Logs; it is untrusted, resolvers verify
everything. The reference registry exposes:

- `GET /1.0/identifiers/{did}` — W3C DID Resolution v0.3 HTTPS binding
  (`versionId`, `versionTime` supported).
- `GET /.well-known/did-content/{scid}/did.jsonl` — the raw log.
- `PUT /.well-known/did-content/{scid}/did.jsonl` — publish; the registry verifies the
  log and refuses history rewrites.
- `GET /1.0/lookup?digestMultibase=…` / `?softBinding=alg:value` — reverse lookup.

Logs can also be pinned on IPFS, embedded in C2PA manifests or advertised from the
content itself (`Link: <did:content:…>; rel="describedby"`).

## Meeting the selection criteria

| **Criteria** | **Details** |
| ------------ | ----------- |
| **Alignment with DID Core specification** | Conforms to DID Core 1.1 (CR), Controlled Identifiers 1.0 (`Multikey`), DID Resolution 0.3 (result format, metadata, errors, HTTPS binding) and VC Data Integrity 1.0 (`eddsa-jcs-2022`). Non-standard v0.1 constructs (`updation`, custom `proof`) were removed. |
| **Security and privacy features** | Self-certifying identifier; hash-chained signed log; key pre-rotation; optional witnesses; append-only hard bindings; registries untrusted. No PII in documents by rule; pseudonymous parties/payees. Detailed considerations in spec §10–§11. No external audit yet. |
| **Scalability and performance** | Logs are small JSON Lines files stored content-addressed (S3/IPFS); resolution is one fetch plus local verification. Registry horizontally scalable (stateless service, object storage). |
| **Ease of implementation and use** | ~600 lines for a full producer/verifier in Python; Go verifier of similar size. Test vectors and JSON Schema published; CLI covers keygen/create/verify/resolve/check. |
| **Community adoption and support** | Registered with W3C; public registry at did.kataru.io; Universal Resolver driver (PR #604). Early: Kataru is the only operator and producer so far. |
| **Compliance with relevant regulations and best practices** | Aligns with EU AI Act Art. 50 provenance expectations via C2PA linkage; licence terms expressible in RSL/TDMRep vocabularies used for AI-training opt-out and licensing. |
| **Global government-approved crypto** | SHA-256 (multihash), Ed25519 (`eddsa-jcs-2022`); ECDSA P-256 (`ecdsa-jcs-2019`) optional. |
| **Privacy-preserving crypto** | Pseudonymous DIDs for parties; per-content `did:key` parties and payment pointers recommended for unlinkability. |
| **Digitally signed cryptographic log of changes to the DID Document** | Yes — the DID Log is the primary artefact: every version signed by the then-authorised update key, chained by entry hash, pre-rotation enforced. |
| **Multi-factor binding to DNS** | Not applicable (identifier is not DNS-based). Registries are discovered via configured URLs, `parameters.registries` or `Link` headers. |
| **Specification with multiple implementers** | Two implementations (Python reference, Go registry/producer) cross-checked on shared vectors; both by Kataru. Independent implementations are sought. |
| **Scope/domain of the types of entities/subjects addressed/named by a particular method** | Digital content items (one file/encoding each): images, audio, video, text, models, datasets. |
| **Estimate of the daily transaction volume of each scope/domain** | Initial deployment: Kataru's catalogue (tens of thousands of works, growing with uploads). Resolution volume expected to dominate creation. |
| **DID Methods that do not serve the needs of a particular company or government** | Open specification; anyone can run a registry; no dependency on Kataru infrastructure for verification. |
| **Governance: Clear frameworks for updates, dispute resolution, and decision-making** | Spec maintained on GitHub (issues/PRs); changelog and versioned contexts. Formal governance to be established with WG input. |
| **Usability: Simple implementation for developers** | Plain JSON (JSON-LD compatible), standard DID Resolution API, reverse lookup, published schema and vectors. |
| **Sustainability: Energy efficiency and eco-friendly infrastructure** | No consensus/proof-of-work; object storage and a stateless resolver. |
| **Economic Feasibility: DIDs costs of use must be reasonable** | Creation and resolution are free on the public registry; self-hosting cost is object storage. |
| **Legal Recognition: Cross-border frameworks for DID acceptance** | Designed to carry rights/licence terms recognised by RSL/TDMRep and C2PA-based provenance; no specific legal framework yet. |
| **Revocation and Recovery: Decentralized mechanisms for key rotation and DID recovery** | Key rotation via `updateKeys`; pre-rotation via `nextKeyHashes`; witnesses for compromise resistance; explicit deactivation. |
| **Emerging Markets: Offline-friendly, low-bandwidth** | Logs are KB-sized and verifiable offline from any copy; IPFS mirroring supported. |
| **Long-lived DIDs needed for long-lived VCs** | Identifier is stable for the lifetime of the content; history preserved even after deactivation. |
| **Low and predictable marginal cost at scale (millions of accounts)** | Per-DID cost is one small object plus index markers; no per-identifier infrastructure. |
| **Ability to create and update identifiers rapidly (within seconds)** | Yes — creation is local signing; publication is one HTTP PUT. |
| **Reliable and predictable-latency operation, for updating and resolving** | Resolution is a single object fetch plus verification (milliseconds). |
| **Resolution should not require additional state or context** | A resolver needs only the log; no shared state. |
| **DIDs are permanent and immutable account identifiers** | Yes; the SCID is fixed by the genesis entry. |
| **Consider support for various DID Traits: <https://identity.foundation/did-traits/>** | Self-certifying: yes. Updateable: yes. Deactivatable: yes. History available: yes (verifiable). Pre-rotation: yes. Enumerable: no. Human-readable: no. Globally resolvable: yes (via registries / Universal Resolver). Formal trait document to be submitted. |
| **Consider categories defined by DID Rubric: <https://www.w3.org/TR/did-rubric/>** | Web/registry-based with verifiable history (same family as `did:webvh`). |
| **Who WANTS to standardize the DID method and commits to doing the work?** | Kataru Inc. (specification, reference implementation, public registry, Universal Resolver driver). |
| **Are there AT LEAST two WG members who support standardization of a DID method?** | Seeking supporters; Kataru will present the method at the WG call. |
| **Are there no trademark or IP issues?** | Specification text under the W3C Document License; code under MIT. No known IP issues. |
| **What type of DID method is this?** | Web/registry-based, self-certifying, with verifiable history; subject domain: digital content. |

## Is this DID method already involved in a standardization process? If so, where?

Registered in the W3C DID Extensions (methods) registry:
<https://www.w3.org/TR/did-extensions-methods/>. Universal Resolver registration
proposed in decentralized-identity/universal-resolver#604.

## Supporting use cases

### 1. Provenance that survives re-hosting
A photo signed by a C2PA-capable camera is published on several CDNs. Its
`did:content` carries the hard binding and a link to the manifest; any copy of the
bytes can be matched to the DID via reverse lookup, and the DID's history shows who
controlled it when.

### 2. Rights and AI-training terms attached to the content itself
A label publishes a track with `license[]` entries: free search indexing with
attribution, AI training only under a paid licence. Crawlers and licensing services
read one declaration (RSL-compatible) regardless of where the file is served.

### 3. Royalty splits for derivative works
A remix is a new DID with `derivedFrom` pointing at the original; `royalty.recipients`
uses DIDs and payment URIs so settlement can be automated without PII.

### 4. Platform-independent catalogue identifiers
Kataru issues a `did:content` for every work it manages; distributors and rights
societies reference the DID instead of platform-specific URLs.

## Seeking Collaboration

- **WG member support** (two members) for the recommendation track.
- **Independent implementations and registry operators** (TypeScript/Rust implementations;
  a second public registry).
- **Trait and rubric review** of the v0.2 specification.
- **Production pilots** with provenance (C2PA/CAWG) and licensing (RSL) partners.

## Contact

- **Organization**: Kataru Inc.
- **Specification**: [github.com/KataruInc/did-content-spec](https://github.com/KataruInc/did-content-spec)
- **Public registry**: <https://did.kataru.io>
- **Issues/Feedback**: [github.com/KataruInc/did-content-spec/issues](https://github.com/KataruInc/did-content-spec/issues)
