# DID method standardization proposal: did:web

This is a proposal to include `did:web` in the initial set of DID methods that
will be standardized by the DID Methods WG.

## Description

The `did:web` method is a DID Method that leverages DNS and HTTP to provide a
web-based DID Document that supports the entire lifecycle of a Decentralized
Identifier. The DID Method consists of serving a DID Document from a website
domain. It is relatively easy to understand and implement, and is flexible with
respect to key formats and service descriptions. There are a number of
independent implementations of the DID Method, and a variety of security-related
extensions are being created for it.

> NOTE: Standardizing `did:web` alone is not sufficient. It is expected that
> many aspects of `did:webvh` and DNS-based multi-factor security will be added
> to `did:web` to make it a more secure DID Method than it is today.

### Benefits

* Simple to understand
* Simple to implement
* Familiar to website operations teams
* All operations scale linearly with CPU/memory resources
* Supports many different cryptographic key types
* Multiple (6+) implementations

### Drawbacks

* No multi-factor security (website compromise leads to full compromise)
* No history
* No key pre-rotation
* Centrally hosted
* Dependent on DNS
* Domain and website are leased

## Existing materials

* [DID Method Specification](https://w3c-ccg.github.io/did-method-web/)
* [Implementations](https://github.com/search?q=did%3Aweb%20implementation&type=repositories)
* No test suite exists as of Jan 2025

## Meeting the selection criteria

Document here how this DID method meets the [DID method selection criteria](../selection-criteria/).

| **Criteria** | **Details** |
|----------|----------|
| **Alignment with DID Core specification** | Yes, fully compliant with DID specification. |
| **Security and privacy features** | INEFFECTIVE CRITERIA: Every DID Method will probably state: Yes, has security and privacy features. |
| **Scalability and performance** | Good scalability. Limits are tied to CPU and memory speeds (ECDSA generation: ~1,000 keys per second per core) |
| **Ease of implementation and use** | Relatively easy to implement and use. Development effort for a single developer creating an initial implementation is one to three days. A complete production-ready implementation might take two to three weeks. |
| **Community adoption and support** | Implemented by at least six independent software systems. |
| **Compliance with relevant regulations and best practices** | INEFFECTIVE CRITERIA: Every DID Method will probably state: Yes, for the regulations and best practices that apply. |
| **Global government-approved crypto** | Uses latest approved NIST and FIPS cryptography (ECDSA and EdDSA) used by many Western nation-states with ability to support cryptography backed by other Eastern nation-state governments. |
| **Privacy-preserving crypto** | Yes, supports BBS privacy-preserving cryptographic key formats. |
| **Digitally signed cryptographic log of changes to the DID Document** | No. |
| **Multi-factor binding to DNS** | No. |
| **Specification with multiple implementers** | Yes, although the specification needs further work and updating. |
| **Scope/domain of the types of entities/subjects addressed/named by a particular method** | INEFFECTIVE CRITERIA: Debatably. Claiming that specific types of entities require specific types of DIDs seems like a privacy-harming anti-pattern. |
| **Estimate of the daily transaction volume of each scope/domain** | INEFFECTIVE CRITERIA: Debatably. Being able to count transaction volume of DID usage seems like a privacy harming anti-pattern. Estimating without hard data seems fraught as well. It is difficult to get these sorts of counts from decentralized systems. |
| **DID Methods that do not serve the needs of a particular company or government** | INEFFECTIVE CRITERIA: The meaning of "do not serve" is unclear. |
| **Governance: Clear frameworks for updates, dispute resolution, and decision-making** | Framework for updates and dispute resolution is based on the domain hosting the document. Disputes regarding domain names are processed through IANA's [dispute resolution procedures](https://www.icann.org/resources/pages/help/dndr/udrp-en). |
| **Usability: Simple implementation for developers** | Yes, as evidenced by the number of implementations and positive developer feedback. |
| **Sustainability: Energy efficiency and eco-friendly infrastructure** | Yes, keys take milliseconds to create and a few hundred bytes to store. DID Documents are typically a few kilobytes in size and are easily served using standard HTTP server software. |
| **Economic Feasibility: DIDs costs of use must be reasonable** | Yes, costs are a fraction of the smallest denomination of mainstream currencies (less than `USD 0.0000004` for an ECDSA create operation and pennies (multiples of USD 0.01) per year for storage). |
| **Legal Recognition: Cross-border frameworks for DID acceptance** | Yes, supports key types approved by multiple national governments. |
| **Revocation and Recovery: Decentralized mechanisms for key rotation and DID recovery** | Revocation is supported, and recovery is a matter for the administrator of a website domain. |
| **Emerging Markets: Offline-friendly, low-bandwidth** | Not offline-friendly except through caching. Low-bandwidth friendly for simple DID Documents. |
| **Long-lived DIDs needed for long-lived VCs** | Yes, lifetimes of DIDs match the lifetimes of domains, which are counted in decades for long-lived institutions. |
| **Low and predictable marginal cost at scale (millions of accounts)** | Yes. |
| **Ability to create and update identifiers rapidly (within seconds)** | Yes, within hundreds of milliseconds for creation and for serving the file from a website domain. |
| **Support for key rotation** | Yes. |
| **Reliable and predictable-latency operation, for updating and resolving** | Yes. |
| **Resolution should not require additional state or context** | Yes. |
| **DIDs are permanent and immutable account identifiers** | Yes. |
| **Consider support for various DID Traits: https://identity.foundation/did-traits/** | BAD CRITERIA: Traits should be listed directly. |
| **Consider categories defined by DID Rubric: https://www.w3.org/TR/did-rubric/** | BAD CRITERIA: Rubric categories should be listed directly. |
| **Who WANTS to standardize the DID method and commits to doing the work?** | Digital Bazaar will commit to doing the base spec work through the entire standardization process but will rely on other teams, such as `did:webvh` to add additional features. |
| **Are there AT LEAST two WG members who support standardization of a DID method?** | Yes, Digital Bazaar and Province of BC. |
| **Are there no trademark or IP issues?** | None. |
| **What type of DID method is this?** | Web-based.  While it is debatable that this is a fully decentralized DID Method, the reliance on DNS and the centralized hosting on a website probably disqualifies it from what people typically mean by "fully decentralized". |

## Supporting use cases

All [DID Use Cases](https://www.w3.org/TR/did-use-cases/) that do not require
extended offline usage are supported by this DID Method. This DID Method is
specifically beneficial for the following classes of use cases:

* DIDs for governments or other large organizations
