# DID method standardization proposal: did:webvh

This is a proposal to include `did:webvh` (`did:web` + Verifiable History)
[v1.0](https://identity.foundation/didwebvh/v1.0/) in the initial set of DID
methods that will be standardized by the DID Methods WG.

## Description

The `did:webvh` DID Method (`did:web` + Verifiable History) was developed to
provide stronger trust guarantees than `did:web` without sacrificing its
simplicity or web-native deployment model. While `did:webvh` uses DNS for
initial discovery, all critical state—identity, updates, and control—is anchored
in a cryptographically verifiable log that is independent of DNS and resistant
to tampering.

Core features of the `did:webvh` method include:

- **DID-to-HTTPS transformation** that is the same as `did:web`.
- **A Verifiable History**: The ability to resolve the full history of the DID using a verifiable chain of
  updates to the DIDDoc from genesis to deactivation.
- **A Self-Certifying Identifier (SCID)**: The SCID, globally unique and
  embedded in the DID, is derived from the initial DID log entry. It ensures the integrity
  of the DID's history mitigating the risk of attackers creating a new object with
  the same identifier.
- **Authorized Keys**: DIDDoc updates include a proof signed by the DID Controllers *authorized* to
  update the DID.
- **Cryptographic Agility** enabled through versioned specification upgrades,
  algorithm-identifying formats (e.g.,
  [multihash](https://identity.foundation/didwebvh/v1.0/#term:multihash) and
  [Data
  Integrity](https://identity.foundation/didwebvh/v1.0/#term:data-integrity)
  proofs), and per-entry method parameters in the DID log that enable DIDs to
  evolve cryptographically over time. No constraints on the keys published in the DIDDoc.
- **Pre-rotation Keys** (optional): The mechanism for publishing pre-rotation keys prevents the loss of
  control of a DID in cases where an active private key is compromised.
- **Witnesses** (optional): The mechanism for having witnesses enables the collaborative
  approval of updates to the DID by a DID Controller before publication.
- **Watchers** An optional mechanism for publishing the location of `did:webvh`
  watchers in the DID log that resolvers can use as another source DID data for
  long term resolution and detection of malicious DID Controllers.
- **DID Portability** (optional): The mechanism for enabling portability allows
  the DID's web location to be moved and the DID string to be updated, both while retaining
  a connection to the predecessor DID(s) and preserving the DID's verifiable history.
- **DID URL path handling** that defaults (but can be overridden) to
  automatically resolving `<did>/path/to/file` by using the same DID-to-HTTPS
  transformation as the DID.
- **Simple, small implementations with minimum dependencies**: Six
  implementations have been created so far, all relatively small (under 3k LOC).
  Few dependencies are required, and each is in common use.

`did:webvh` was previously called "The Trusted DID Web (`did:tdw`) DID Method".

### Benefits

- Straight forward to understand -- with clear cryptographic processes for verifiability.
- The cryptographically-verifiable history eliminates the reliance on the DNS system for other than DID Log discovery.
- Formalized DID Method specification versioning and (optional) identifier portability enables long (decades) lasting, secure identifiers.
- Can be used in conjunction with existing `did:web` implementations to provide a smooth security upgrade.
- Optional features (pre-rotation, witnesses, watchers) allow the DID Controller to increase security at the cost of more complex key management on their part -- with little increase in the complexity of resolvers.
- Simple to implement, with few dependencies required for managing (registering, resolving) the DID.
- Supports all cryptographic key types in the DIDDoc, as permitted by the DID Core specification, and as required by the DID Controller.
- Familiar web server publishing of data, understood by website operations teams.
- All operations scale linearly with CPU/memory resources.
- Multiple (5+) implementations.

### Drawbacks

- Centrally hosted -- although the verifiability of the DID and DIDDoc content is independent of the DNS location of the DID Log file.
- Dependent on DNS for DID discovery, but not for the security and verifiability of the DID and its history.
- Domain and website are leased, although there is an (optional) portability capability that allows the history of the DID to move if Domain and website are lost.

## Existing materials

- [DID Method Specification](https://identity.foundation/didwebvh/)
- [Implementations](https://didwebvh.info/latest/implementations/)
- [Test Suite](https://github.com/decentralized-identity/didwebvh-test-suite)

## Is this DID method already involved in a standardization process? If so, where?

The incubation of the `did:webvh` DID Method Specification is happening at the [Decentralized Identity Foundation](https://identity.foundation).

The DID has achieved a v1.0 status, following the DIF Guidelines and approved by the DIF Steering Committee.

## Meeting the selection criteria

Document here how this DID method meets the [DID method selection criteria](../selection-criteria/).

| **Criteria** | **Details** |
|----------|----------|
| **Alignment with DID Core specification** | Yes, fully compliant with DID specification. |
| **Security and privacy features** | Yes, see the verifiability and security features listed above. `did:webvh` inherits the privacy features of [DID Core](https://w3c.github.io/did/) |
| **Scalability and performance** | Web scalability for resolvers. Per DID update limits are tied to CPU and memory speeds (ECDSA generation: ~1,000 keys per second per core) |
| **Ease of implementation and use** | Relatively easy to implement and use. Registrar and resolver implementations are about ~3k lines of code, and a test suite is available. Web server development effort for a single developer creating an initial implementation is one to three weeks. A complete production-ready web server implementation might take one to two months from scratch, driven by the desired governance around the publication of DIDs and related resources. Full stack reference implementations exist, along with the did:webvh Information [https://didwebvh.info](https://didwebvh.info) for collaborating.  |
| **Community adoption and support** | Implemented by at least four independent software systems. |
| **Compliance with relevant regulations and best practices** | Yes. |
| **Global government-approved crypto** | The DID Method itself uses approved NIST and FIPS cryptography (ECDSA and EdDSA) permitted by many Western nation-states, with ability to support cryptography backed by other Eastern nation-state governments. The DID Method is defined to support evolving the cryptography used by the DID Method for handling the verifiable history log through the versioning of the specification and DIDs using the specification. DIDs created by DID Controllers can use whatever cryptography they want -- the specification does not constrain what is put into the DIDDoc. |
| **Privacy-preserving crypto** | Yes, supports BBS privacy-preserving cryptographic key formats within the DIDDoc. Any DID-Core compatible key formats can be defined in the published DIDDocs. |
| **Digitally signed cryptographic log of changes to the DID Document** | Yes. |
| **Multi-factor binding to DNS** | No. |
| **Specification with multiple implementers** | Yes |
| **Scope/domain of the types of entities/subjects addressed/named by a particular method** | Expected to be used primarily for organizational entities, but that is not limited by the specification. Self-hosting is possible, and one could imagine DID-hosting services could be created using `did:webvh` in a way similar to [BlueSky](https://bsky.social/)'s use of `did:plc`. |
| **Estimate of the daily transaction volume of each scope/domain** | A difficult metric, but "web-scale" seems the appropriate response. The publication and resolution process is comparable to writing/retrieving a file from a web server. |
| **DID Methods that do not serve the needs of a particular company or government** | The DID Method and publication/retrieval methods are independent of any particular entity. Requires only the ability to publish and update a web file secured with SSL. |
| **Governance: Clear frameworks for updates, dispute resolution, and decision-making** | Framework for updates and dispute resolution is based on the domain or platform hosting the document. Disputes regarding domain names are processed through IANA's [dispute resolution procedures](https://www.icann.org/resources/pages/help/dndr/udrp-en). `did:webvh` DID Logs published to a platform (such as GitHub, or a DID publishing service) would be subject to the dispute resolution governance of the selected platform or service. |
| **Usability: Simple implementation for developers** | Yes, as evidenced by the number of early implementations and positive developer feedback. |
| **Sustainability: Energy efficiency and eco-friendly infrastructure** | Yes, keys take milliseconds to create and minimal overhead to store. `did:webvh` DID Logs are typically a few kilobytes in size and are easily served using standard HTTP server software. Frequently updated, very long lasting `did:webvh` DIDs might have a DID Log in the low megabyte size. The majority  of the DID Log is the content of the DIDDoc. |
| **Economic Feasibility: DIDs costs of use must be reasonable** | Yes, costs are a fraction of the smallest denomination of mainstream currencies (less than `USD 0.0000004` for an ECDSA create operation and pennies (multiples of USD 0.01) per year for storage). |
| **Legal Recognition: Cross-border frameworks for DID acceptance** | Yes, supports key types approved by multiple national governments. |
| **Revocation and Recovery: Decentralized mechanisms for key rotation and DID recovery** | Key rotation is inherent in the DID Method and is secure and verifiable, independent of DNS. Revocation is supported per the DID-Core specification. Recovery is both a matter for the administrator of a website domain, and how the DID Controller manages the `did:webvh` update authorization keys. For example, a `did:webvh` could retain an offline key that is used for DID recovery, should that be needed. Watchers are supported to enable alternate locations for resolution that can be used long after the deletion of the DID from its original location.|
| **Emerging Markets: Offline-friendly, low-bandwidth** | Not offline-friendly except through caching. Low-bandwidth friendly for simple DID Documents. The `did:webvh` log format use of [JSON Lines](https://jsonlines.org) enables retrieval of only added versions (log entries) using standard HTTP headers.  |
| **Long-lived DIDs needed for long-lived VCs** | Yes, lifetimes of DIDs match the lifetimes of domains, which are counted in decades for long-lived institutions. The formal use of DID Method specification versions enables evolving the characteristics of the DID Method (e.g., permitted hashing and signature algorithms) over the lifetime of the DID. The DID Controller has full control over the contents of the DIDDoc versions, allowing updates to the DID as the DID Core specification evolves, and as cryptographic requirements change. The optional portability mechanism allows for DIDs to be moved to a new location (ideally with an HTTPS "redirect"), while retaining its self-certifying identifier and verifiable history. The inclusion of the globally unique self-certifying identifier in the DID and support for Watchers allows services such as trust registries, DID stores, or independent Watchers to retain verifiable copies of the DID and monitor its evolution over time—extending the DID’s lifetime even if the original domain becomes unavailable. Watchers may also cache and serve DID resources—such as schemas, credential metadata, or revocation status—ensuring (for example) the continuity of verifiable credential issuance, verification, and revocation workflows. |
| **Low and predictable marginal cost at scale (millions of accounts)** | Yes -- "web-scale". |
| **Ability to create and update identifiers rapidly (within seconds)** | Yes, within hundreds of milliseconds for creation and for serving the DID Log file from a website domain. |
| **Support for key rotation** | Yes, with a verifiable history of the versions of the DID, past keys and rotations. |
| **Reliable and predictable-latency operation, for updating and resolving** | Yes. |
| **Resolution should not require additional state or context** | Yes. |
| **DIDs are permanent and immutable account identifiers** | Yes. Optionally, a DID **MAY** enable portability, where the location of the DID can change (ideally with an HTTPS redirection), while retaining the same immutable self-certifying ID (SCID) and the same verifiable history -- including the verifiable change of the DID's web location. Further, support for Watchers, queried by only the SCID (and thus, independent of the location element of the DID), enable the survivability of the DID long past when the DID is removed from its original location on the web. |
| **Consider support for various DID Traits: <https://identity.foundation/did-traits/>** | `did:webvh` is included in the [Comparison of DID Methods](https://identity.foundation/did-traits/#comparison-of-did-methods) in the DID Traits document. While the majority of the Traits are `true` for `did:webvh, the following ones are `false`: Transactional Fees, Multi-Sig Verification Method, Human-readable, Enumerable, Locally Resolvable, Decentrally Hosted.  |
| **Consider categories defined by DID Rubric: <https://www.w3.org/TR/did-rubric/>** | A `[did:webvh` DID Rubric Evaluation](https://didwebvh.info/latest/did-rubric-evaluation/) by the `did:webvh` specification editors can be found on the `did:webvh` Information Site ([https://didwebvh.info/](https://didwebvh.info)) |
| **Who WANTS to standardize the DID method and commits to doing the work?** | BC Gov and its collaborators are willing to continue its work on the base specification and implementations. |
| **Are there AT LEAST two WG members who support standardization of a DID method?** | Yes, Digital Bazaar and the Province of British Columbia, Canada. |
| **Are there no trademark or IP issues?** | None. |
| **What type of DID method is this?** | Web-based, Decentralized. This is arguably a fully decentralized DID Method. While it relies on DNS to locate the DID Log, the DID itself is self-certifying and its history is chained and fully verifiable. Optionally, updates can be witnessed by independent parties, and Watchers can cache and serve verified copies of the DID over time. Even if the original hosting domain becomes unavailable, the DID can be verified and resolved through external sources such as Trust Registries, DID archives, or Watchers. |

## Supporting use cases

All [DID Use Cases](https://www.w3.org/TR/did-use-cases/) that do not require
extended offline usage are supported by this DID Method. This DID Method is
specifically beneficial for the following classes of use cases:

- DIDs for governments or other large organizations
- Enterprises, such as verifiable credential issuers, verifiers and participants in verifiable supply chains.
- To Be Explored: Platforms might provide `did:webvh` DIDs as a service for individuals, where the individuals hold the private keys, and the service publishes the public information for the individuals, enabling the individual to control their participation in verifiable transactions.
