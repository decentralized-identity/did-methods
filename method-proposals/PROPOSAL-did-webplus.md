# DID method standardization proposal: did:webplus

This is a proposal to include `did:webplus` in the initial set of DID methods that will be standardized by the DID Methods WG.

## Description

The `did:webplus` DID method is a natural extension of `did:web`, and its core required extensions were set by Open Credentialing Initiative ([OCI](https://oc-i.org)), a non-profit collaboration of 62 members who are primarily multi-billion dollar healthcare enterprises, in response to US healthcare regulation requirements surrounding privacy, security, and auditability. OCI has set the specifications for a W3C VC ecosystem that today encompasses one in every three packages that move through the supply chain, along with over 10,000 pharmacies. OCI is open to all, with voting membership and a governing board. All decisions are transparent and then upstreamed to the Partnership for [DSCSA](https://www.fda.gov/drugs/drug-supply-chain-integrity/drug-supply-chain-security-act-dscsa) Governance ([PDG](https://dscsagovernance.org/)), a public-private partnership between FDA and industry, for review and publication. Production instances are subject to independent third-party audits recognized by the PDG conformance program, such as by Drummond Group, an internationally recognized software auditing firm.

Specification is found [here](https://ledgerdomain.github.io/did-webplus-spec/).

Documentation and reference implementation is found [here](https://github.com/LedgerDomain/did-webplus).  [Presentation](https://www.youtube.com/watch?v=Ws55MlDuUGI) and corresponding [slide deck](https://docs.google.com/presentation/d/1oZc4WABaG3zhw7gHclSIaQCgnchdWRJvqUDQLq4L-Ig/edit?usp=sharing).

### Some Terminology

- VDR: Verifiable Data Registry (this term is defined generally in the context of decentralized identity) -- a website/web service that hosts DID documents and is the origin (and therefore authority) on their content.  For example, given a DID `did:webplus:example.com/{self-hash}`, its history of DID documents may be retrieved via HTTP GET of URL `https://example.com/{self-hash}/did-documents.jsonl`
- VDG: Verifiable Data Gateway (this is a `did:webplus`-specific term) -- a witnessing and archival service which provides the benefits listed below.
- CDN: Content Delivery Network (this is a standard web technology) -- a large network of proxy servers that service requests on behalf of the primary service, meant to short-cut many requests using cached data.  These servers are placed "near" the service's clients in order to drastically reduce network request latency.  They also provide a layer of defense against security threats such as DDoS attacks.

### Benefits

- Uses standard web technologies.
- Is a "strong" DID method, by which is meant:
  - Has cryptographically verifiable DID create/update operations
  - Provides historical DID resolution (resolve previous versions of DID document)
  - Prevents DID forking and alteration of DID history.
- DID document is self-contained and fully self-verifiable; no auxiliary log files.
- DID create and update are each `O(1)` operations.
- VDG service allows:
  - Provide long-term DID resolution capabilities, even if VDRs go offline.
  - Expansion of the "scope of truth" in which verifiers can agree on which DID updates are valid.
  - Enable "thin" DID resolvers that outsource their DID verification responsibilities to a trusted VDG; DID resolution becomes simply HTTP GET with no verification, which is as simple as `did:web` DID resolution is.  This makes `did:webplus` friendly to browser-based verifiers.
- "Thin" DID resolve is `O(1)` operation.
- "Full" DID resolver keeps its own copy of all previously fetched-and-verified DID documents, and therefore can in many cases operate fully offline (and is therefore fast).
- Its architecture is somewhat configurable, so is tunable to the specific use case.

### Drawbacks

- Resolving a given DID for the first time requires fetching and verifying its entire history, which could be arbitrarily long.  However, realistic uses cases are such that the number of DID updates will be less than several thousand, which verifies in a reasonable amount of time.  The worst case is avoided by the use of VDGs to which DID updates can be pre-emptively pushed.
- VDGs are a point of centralization.  Ideally this should be offset by having VDGs be run by organizations whose interests/business model doesn't conflict with that of DID controllers and DID resolvers.
- As in `did:web`, DID resolution depends on DNS, which is somewhat centralized.  However, verification is independent of DNS.
- As in `did:web`, domains are leased, and a lapsed domain can be co-opted by an attacker.  However, the DIDs anchored to that domain can't be co-opted unless the attacker somehow compromises the DID controllers' private keys.

## Existing Materials

Reference implementations of each component of `did:webplus` are available [on Github](https://github.com/LedgerDomain/did-webplus).  In particular:

- [`did:webplus` Verifiable Data Registry (VDR) service](https://github.com/LedgerDomain/did-webplus/blob/main/did-webplus/vdr/README.md)
- [`did:webplus` Verifiable Data Gateway (VDG) service](https://github.com/LedgerDomain/did-webplus/blob/main/did-webplus/vdg/README.md)
- [`did-webplus` CLI tool](https://github.com/LedgerDomain/did-webplus/blob/main/did-webplus/cli/README.md)

## Is this DID method already involved in a standardization process? If so, where?

The standardization target for `did:webplus` is within Open Credentialing Initiative ([OCI](https://oc-i.org)), a non-profit collaboration of 62 members who are primarily multi-billion dollar healthcare enterprises.

## Meeting the selection criteria

How this DID method meets the [DID method selection criteria](../selection-criteria/):

| **Criteria** | **Details** |
|----------|----------|
| **Alignment with DID Core specification** | Yes, fully compliant. |
| **Security and privacy features** | Security is achieved through cryptographic verification and witnessing capabilities.  Privacy depends on certain governance choices. |
| **Scalability and performance** | Architecture includes elements for hyperscaling, using CDNs to enhance security and performance. |
| **Ease of implementation and use** | Is a balance of standard web technologies and cryptographic strength; most difficult feature is the self-hashing process on DID documents (just as producing SCID in `did:webvh` and `did:webs` is). |
| **Community adoption and support** | `did:webplus` has been cleared under the OCI auditing program and is targeted to be added to the OCI specification in 2026.  Design and reference implementation actively being developed and maintained by LedgerDomain. |
| **Compliance with relevant regulations and best practices** | One of `did:webplus`'s explicit design criteria is servicing historical DID resolution/audit requirements that come from regulation. Implementations of `did:webplus` use standard web technologies aligned with best practices. |
| **Global government-approved crypto** | Specification allows for any cryptographic material within the DID document.  Reference implementation supports various government-approved cryptography, including Secp256k1, P256, P384, P521 (ECDSA) and Ed25519, Ed448 (EdDSA) curves. |
| **Privacy-preserving crypto** | Specification allows for any cryptographic material within the DID document.  Reference implementation will eventually support various privacy-preserving cryptography. |
| **Digitally signed cryptographic log of changes to the DID Document** | Each DID document includes data necessary to cryptographically verify DID operation validity; sequence of DID documents forms a complete and verifiable history of the DID.  This is isomorphic to having a separate log of updates as in `did:webs` and `did:webvh`. |
| **Multi-factor binding to DNS** | Not required by the specification. |
| **Specification with multiple implementers** | [Specification](https://ledgerdomain.github.io/did-webplus-spec/).  [Reference Implementation](https://github.com/LedgerDomain/did-webplus) (the only one so far). |
| **Scope/domain of the types of entities/subjects addressed/named by a particular method** | Intended for omni-directional identity.  DIDs are published on VDRs, which can range from personal website to centralized hosting service.  VDG is meant to broaden the "scope of truth" for strong agreement on valid DID updates. |
| **Estimate of the daily transaction volume of each scope/domain** | Transaction volume depends on the specific ecosystem.  However, regarding max transaction throughput, because VDR and VDG are web services, their throughput capacities have similar characteristics as web services generically (can enhance with vertical/horizontal scaling and CDNs). |
| **DID Methods that do not serve the needs of a particular company or government** | This criteria really only applies at a "survey of DID methods" level, and is not semantically valid for a single DID method. But to comment on this, `did:webplus` provides omni-directional identity, and so would be unsuitable for use cases requiring uni-directional identity. |
| **Governance: Clear frameworks for updates, dispute resolution, and decision-making** | DID creation, update, and fork detection are well-defined, formal data processes.  Other governance aspects are not specified. |
| **Usability: Simple implementation for developers** | For implementers of "thin" DID resolver (i.e. verifiers using a VDG, e.g. verifying signatures, credentials, presentations), implementation is as simple as that of `did:web` -- issue an appropriate HTTP GET and process the DID document as usual (see definition of VDG in "Existing Materials" section). For implementers of VDR, VDG, and "full" DID resolver, `did:webplus` DID document data model, DID document store, and appropriate web endpoints/requests must be implemented. |
| **Sustainability: Energy efficiency and eco-friendly infrastructure** | All operations are effectively ordinary CRUD operations on a web service.  Verification operations are incremental based on the previously-verified history.  The slowest operation would be to fetch and verify the whole history of a DID, but the VDG is intended to obviate that need for the majority of use cases. |
| **Economic Feasibility: DIDs costs of use must be reasonable** | VDR costs are the same as creating, updating, and serving static web content.  VDG costs are fetching, verification, and storage of a large collection of DID documents.  "Thin" DID resolver cost is a single HTTP GET operation per verification.  "Full" DID resolver cost is fetching, verifying, and storage of a collection of DID documents (only the ones actually requested). |
| **Legal Recognition: Cross-border frameworks for DID acceptance** | `did:webplus` was designed in part to service regulatory requirements within the context of the [Open Credentialing Initiative](https://oc-i.org) which currently governs a global network of entities that are subject to the [Drug Supply Chain Security Act](https://www.fda.gov/drugs/drug-supply-chain-integrity/drug-supply-chain-security-act-dscsa).  In particular, this network has achieved interoperability on usage of `did:web` and `did:ethr` as the basis for use of W3C Verifiable Credentials and Presentations. `did:webplus` is part of a plan to enhance and strengthen regulatory compliance capabilities. |
| **Revocation and Recovery: Decentralized mechanisms for key rotation and DID recovery** | Key rotation is supported.  DID recovery can optionally be achieved using the multi-sig capabilities of the "update rules" for a DID, but is not mandated by the specification. |
| **Emerging Markets: Offline-friendly, low-bandwidth** | "Full" DID resolver stores all verified DID documents, and therefore is capable of resolving those DID documents fully offline.  "Full" DID resolution only requires retrieving unseen DID updates, and not necessarily the complete DID history. |
| **Long-lived DIDs needed for long-lived VCs** | Providing historical DID resolution is a primary goal and capability of `did:webplus`. |
| **Low and predictable marginal cost at scale (millions of accounts)** | Yes, costs are proportionate to the number of DIDs and the rate of DID updates; analogous to ordinary CRUD-style web services. |
| **Ability to create and update identifiers rapidly (within seconds)** | Yes.  Actual latencies are similar to ordinary HTTP requests; in the range of hundreds of milliseconds down to tens of milliseconds. |
| **Support for key rotation** | Yes. |
| **Reliable and predictable-latency operation, for updating and resolving** | Yes.  In particular, the "thin" DID resolution operation (which is expected to be by far the most common operation) was designed to have as low latency as possible (especially if a CDN is used with the VDG). |
| **Resolution should not require additional state or context** | Correct. |
| **DIDs are permanent and immutable account identifiers** | Yes. |
| **Consider support for various DID Traits: <https://identity.foundation/did-traits/>** | [PR for did:webplus DID traits template is pending](https://github.com/decentralized-identity/did-traits/pull/66).  |
| **Consider categories defined by DID Rubric: <https://www.w3.org/TR/did-rubric/>** | This criterion is far too broadly-scoped to address in a line item.  Apropos governance, see description at the top of this document. |
| **Who WANTS to standardize the DID method and commits to doing the work?** | LedgerDomain and Open Credentialing Initiative. |
| **Are there AT LEAST two WG members who support standardization of a DID method?** | LedgerDomain and Open Credentialing Initiative. |
| **Are there no trademark or IP issues?** | To the best of our knowledge, `did:webplus` does not infringe upon any existing intellectual property rights, patents, or trademarks.  If any unforeseen intellectual property or trademark concerns arise, LedgerDomain is committed to addressing them transparently and in good faith.  In the event that a legitimate claim is identified, LedgerDomain will assess the matter and, where appropriate, make a voluntary donation or take other reasonable actions to ensure continued open and equitable access. |
| **What type of DID method is this?** | Web-based. `did:webplus` should also be considered as decentralized as the set of VDRs and VDGs in use, which could be structured to have any degree of decentralization.  However, it's not a "purely decentralized" DID method such as one based on a peer-to-peer network. |

## Supporting Use Cases

`did:webplus` is meant to provide everything `did:web` does, and give additional guarantees.  Key use cases include, and are not limited to:

- Omnidirectional, long-term identity for
  - Individuals
  - Devices
  - Servers
  - Companies
  - Entities within regulatory ecosystems
  - etc.
- Use cases having long-term verification/audit requirements, such as
  - Pharmaceutical (and other) supply chain subject to government regulation
  - Academic institutions (digital credentials representing academic degrees)
  - Journalistic entities/institutions (verifiable authorship)
  - Governmental institutions
  - Institutions regarding public record
- Keeping one's own copy of all retrieved DID documents (via "full" DID resolver), so that:
  - DID resolution can happen offline in many cases (and is therefore very fast).
  - One has direct custody of materials needed to conduct audit and historical verification.
  - There is no need to depend on an external service to resolve previously-resolved DIDs.
