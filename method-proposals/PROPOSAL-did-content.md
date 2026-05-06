i# DID method recommendation proposal: did:content

This is a proposal to include `did:content` in the set of DID methods recognized and
recommended by the DIF DID Methods WG.

**Status**: This is an early-stage proposal. The specification is currently in draft
status and seeking community feedback and collaboration.

## Description

The `did:content` method identifies content such as images, video, and music. The goal
is to enable comprehensive decentralized management of content and rights.

### Motivation

Recently, a wide variety of content is uploaded on the Internet. However, content
identifiers depend on storage/platform like S3 or YouTube. As a result, if storage goes down,
access becomes difficult.

While solutions such as Content Delivery Networks (CDN) like Cloudflare or Fastly
exist, they are still managed in a centralized manner.

The `did:content` method addresses these challenges by:

1. **Storage-agnostic identification**: Defining IDs that can resolve various types of
   storage, centered on content rather than location
2. **Improved availability**: Supporting content resolution across multiple storage
   backends
3. **Rights management**: Extending authentication of rights holders to both anonymous
   and non-anonymous types using cryptographic methods

### DID Syntax

```
did:content:<method-specific-id>
```

The method-specific identifier is generated as:

```
content-id: Base58(RIPEMD160(sha3-256(DID Document without id)))
```

Example:

```did
did:content:3qrgME9eV7brjYsx3Ebbp9hubiQna1wcD1FdzuG4P1V6xmZwSdLXzCG
```

### DID Document Structure

```json
{
  "@context": [
    "https://www.w3.org/ns/did/v1",
    "https://did.kataru.io/did/v1",
    "https://w3id.org/security/suites/secp256k1recovery-2020/v2"
  ],
  "id": "did:content:03Z5hdN7vxXyp5YW4WGqMYowMAB3SLG6tN2UjWb2DfAmkTHC1WYDfnjB",
  "controller": [
    "did:content:03Z5hdN7vxXyp5YW4WGqMYowMAB3SLG6tN2UjWb2DfAmkTHC1WYDfnjB#author",
    "did:content:03Z5hdN7vxXyp5YW4WGqMYowMAB3SLG6tN2UjWb2DfAmkTHC1WYDfnjB#rights-holder"
  ],
  "verificationMethod": [
    {
      "id": "did:key:3TL4YbgfwnJmJhyxKKDRpA81vB1QkWvvWRMioKQb6yv9HYwsZCpnVWB#controller",
      "type": "EcdsaSecp256k1RecoveryMethod2020",
      "controller": "did:key:3TL4YbgfwnJmJhyxKKDRpA81vB1QkWvvWRMioKQb6yv9HYwsZCpnVWB"
    },
    {
      "id": "did:key:3qrgME9eV7brjYsx3Ebbp9hubiQna1wcD1FdzuG4P1V6xmZwSdLXzCG#delegate",
      "type": "EcdsaSecp256k1RecoveryMethod2020",
      "controller": "did:key:3qrgME9eV7brjYsx3Ebbp9hubiQna1wcD1FdzuG4P1V6xmZwSdLXzCG"
    }
  ],
  "updation": ["#controller", "#delegate"],
  "authentication": ["#controller", "#delegate"],
  "assertionMethod": ["#controller", "#delegate"],
  "royaltyRecipients": [
    {
      "recipient": "example@getalby.com",
      "ratio": 80
    }
  ],
  "service": [
    {
      "id": "#kataru",
      "type": "kataru",
      "serviceEndpoint": "https://kataru.io/content/example"
    }
  ],
  "proof": {
    "type": "Secp256k1",
    "creator": "did:key:3qrgME9eV7brjYsx3Ebbp9hubiQna1wcD1FdzuG4P1V6xmZwSdLXzCG#key-1",
    "signatureValue": "..."
  }
}
```

### Fragments

- `#author`: Returns authors of content
- `#rights-holder`: Returns rights-holder of content

### Royalty Recipients

The DID Document includes a `royaltyRecipients` property that specifies how royalties
should be distributed, with each recipient having a ratio indicating their share.

### Benefits

- **Content-centric identification**: DIDs tied to content rather than storage location
- **Rights management built-in**: Author and rights-holder fragments, royalty distribution
- **Storage flexibility**: Supports IPFS, S3, and other storage backends
- **Self-certifying**: DID derived from hash of DID Document

### Drawbacks / Current Limitations

- **Early stage**: Specification is in draft status
- **Single implementation**: Only one reference implementation exists (Python)
- **No production deployments**: Not yet deployed in production environments
- **No test suite**: Formal test suite not yet developed
- **Limited tooling**: No SDKs, wallets, or resolver integrations yet
- **Unproven at scale**: Performance and scalability not yet validated

## Existing Materials

### Specifications

- [DID Scheme Specification](https://github.com/KataruInc/did-content-spec) (Draft)
- [W3C DID Methods Registry Entry](https://www.w3.org/TR/did-extensions-methods/)

### Reference Implementation

- [did-content-spec Repository](https://github.com/KataruInc/did-content-spec)
  - Includes key generation code (Python)
  - **Note**: This is currently the only implementation. Additional implementations
    are welcome and needed for standardization.

### Architecture

The DID Resolver serves as the Verifiable Data Registry:

- **GET** `/resolve?did=?` - Resolve a DID to its DID Document
- **POST** `/create?contentType=&contentUrl=&signature=` - Create new DID and Document
- **POST** `/update?did=&contentType=&contentUrl=&signature=` - Update DID Document
- **POST** `/delete?did=` - Deactivate a DID

The DID Resolver creates a DID Document from arguments and generates a DID to be
associated. It maintains a database that associates DIDs with DID Document storage
locations.

### Verifiable Data Registry

DID Documents can be stored in common storage such as:

- IPFS
- S3
- Other highly available storage

## Meeting the selection criteria

| **Criteria** | **Details** |
| ------------ | ----------- |
| **Alignment with DID Core specification** | Designed for conformance with W3C DID Core 1.0. Uses standard contexts including `https://www.w3.org/ns/did/v1`. Formal conformance testing not yet completed. |
| **Security and privacy features** | EcdsaSecp256k1RecoveryMethod2020 for verification. Signature-based operations for all mutations. Security audit not yet conducted. |
| **Scalability and performance** | Designed for scalability via content-addressable approach. Multiple storage backend support (IPFS, S3). Performance benchmarks not yet available. |
| **Ease of implementation and use** | REST API design for CRUD operations. Reference implementation available in Python. Additional language implementations needed. |
| **Community adoption and support** | Early stage. Registered with W3C DID Methods Registry. No known production deployments yet. Seeking community collaboration. |
| **Compliance with relevant regulations and best practices** | Uses standard cryptographic libraries. Specific compliance assessments not yet conducted. |
| **Global government-approved crypto** | secp256k1, SHA3-256, RIPEMD160 — widely used algorithms. |
| **Privacy-preserving crypto** | Controller-based access control. Anonymous and non-anonymous authentication options defined in spec. |
| **Digitally signed cryptographic log of changes to the DID Document** | All updates require cryptographic signatures from authorized controllers. Proof included in DID Document. |
| **Multi-factor binding to DNS** | Not applicable. |
| **Specification with multiple implementers** | **No**. Currently only one reference implementation exists. This is a key area where collaboration is needed. |
| **Scope/domain of the types of entities/subjects addressed/named by a particular method** | Content-focused: images, video, music, and other digital content requiring rights management. |
| **Estimate of the daily transaction volume of each scope/domain** | Unknown. No production deployments yet. |
| **DID Methods that do not serve the needs of a particular company or government** | Open specification under development. |
| **Governance: Clear frameworks for updates, dispute resolution, and decision-making** | OSS governance via GitHub. Governance framework still being established. |
| **Usability: Simple implementation for developers** | REST API design. Developer experience feedback not yet collected at scale. |
| **Sustainability: Energy efficiency and eco-friendly infrastructure** | No proof-of-work required. Lightweight resolution. |
| **Economic Feasibility: DIDs costs of use must be reasonable** | DID creation is free. Storage costs depend on chosen backend. |
| **Legal Recognition: Cross-border frameworks for DID acceptance** | Designed to be compatible with W3C DID ecosystem. No specific legal frameworks established. |
| **Revocation and Recovery: Decentralized mechanisms for key rotation and DID recovery** | Multiple controller support. Delegate keys for recovery defined in spec. |
| **Emerging Markets: Offline-friendly, low-bandwidth** | Partially. Local resolver caching possible but not yet implemented. |
| **Long-lived DIDs needed for long-lived VCs** | Content-addressable design intended for permanent identifiers. Long-term stability not yet proven. |
| **Low and predictable marginal cost at scale (millions of accounts)** | Designed for low cost at scale. Not yet tested at scale. |
| **Ability to create and update identifiers rapidly (within seconds)** | REST API enables fast operations. |
| **Support for key rotation** | Multiple verification methods with delegate support defined in spec. |
| **Reliable and predictable-latency operation, for updating and resolving** | Depends on Verifiable Data Registry choice (IPFS, S3). |
| **Resolution should not require additional state or context** | Each resolver independently maintains DID state. |
| **DIDs are permanent and immutable account identifiers** | Content-addressable identifiers designed to be permanent. |
| **Consider support for various DID Traits: <https://identity.foundation/did-traits/>** | Not yet formally evaluated. Expected traits: Decentralized, Persistent, Cryptographically Verifiable, Resolvable. |
| **Consider categories defined by DID Rubric: <https://www.w3.org/TR/did-rubric/>** | Not yet formally evaluated. Expected category: Decentralized. |
| **Who WANTS to standardize the DID method and commits to doing the work?** | Kataru Inc. Committed to spec development and seeking collaborators. |
| **Are there AT LEAST two WG members who support standardization of a DID method?** | **Not yet**. Seeking WG member support through this proposal. |
| **Are there no trademark or IP issues?** | Open specification. No known IP issues. |
| **What type of DID method is this?** | Content-focused Decentralized (early stage) |

## Is this DID method already involved in a standardization process? If so, where?

The `did:content` method has been registered with the W3C DID Methods Registry:
<https://www.w3.org/TR/did-extensions-methods/>

## Supporting use cases

The following use cases are envisioned but not yet validated in production:

### 1. Digital Content Rights Management

Content creators could use `did:content` to:

- Establish verifiable ownership of digital content
- Define royalty distribution among multiple rights holders
- Manage content across multiple platforms with a single identifier

### 2. Music and Video Distribution

- Artists could mint DIDs for their work
- Royalty recipients defined in the DID Document
- Multiple service endpoints for multi-platform distribution

### 3. Content Authentication

- Verify the authenticity of content regardless of where it's hosted
- Prevent unauthorized claims of ownership
- Enable transparent rights holder discovery via fragments

### 4. Cross-platform Content Resolution

- Content resolved from multiple storage backends
- Platform independence through storage-agnostic identification

## Seeking Collaboration

This proposal is at an early stage and we are actively seeking:

- **Additional implementers**: Implementations in other languages (TypeScript, Go, Rust)
- **WG member support**: At least two WG members needed for standardization
- **Production pilots**: Organizations interested in piloting `did:content`
- **Specification review**: Feedback on the draft specification
- **Test suite development**: Contributors for conformance test suite

## Contact

- **Organization**: Kataru Inc.
- **Specification**: [github.com/KataruInc/did-content-spec](https://github.com/KataruInc/did-content-spec)
- **Issues/Feedback**: [github.com/KataruInc/did-content-spec/issues](https://github.com/KataruInc/did-content-spec/issues)
