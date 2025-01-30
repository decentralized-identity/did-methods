# DID method standardization proposal: did:key

This is a proposal to include `did:key` in the initial set of DID methods that
will be standardized by the DID Methods WG.

## Description

The `did:key` method is a minimal, static DID Method that is used to express a
single public cryptographic key. The DID Document supports many different types
of cryptographic keys with the ability to add future cryptographic key types in
a way that is backwards compatible with the key format. The method does not
support key revocation or key rotation. As of January 2025, it is implemented by
[over 23 implementations](https://canivc.com/implementations/).

### Benefits

* Simple to understand
* Simple to implement
* All operations scale linearly with CPU/memory resources
* Supports many different cryptographic key types
* Broadly implemented and deployed (23+ implementations)

### Drawbacks

* No key rotation
* No deactivation
* No multi-factor security (private key compromise leads to full compromise)

## Existing materials

* [DID Method Specification](https://w3c-ccg.github.io/did-method-key/)
* [Implementations](https://canivc.com/implementations/) (all test suite implementations use `did:key` for public keys)
* [Preliminary Test Suite](https://w3c-ccg.github.io/did-key-test-suite/)

## Meeting the selection criteria

Document here how this DID method meets the [DID method selection criteria](../selection-criteria/).

| **Criteria** |
| -------- |
| **Alignment with DID Core specification** |
| Yes, fully compliant with DID specification. |
| **Security and privacy features** |
| INEFFECTIVE CRITERIA: Every DID Method will probably state: Yes, has security and privacy features. |
| **Scalability and performance** |
| Good scalability performance. Limits are based on CPU and memory performance (ECDSA generation: ~1,000 keys per second per core) |
| **Ease of implementation and use** |
| Relatively easy to implement and use. Development effort for a single developer creating an initial implementation is between 1-3 days. A complete production-ready implementation might take 2-3 weeks. |
| **Community adoption and support** |
| Implemented by at least 23 independent software systems. |
| **Compliance with relevant regulations and best practices** |
| INEFFECTIVE CRITERIA: Every DID Method will probably state: Yes, for the regulations and best practices that apply. |
| **Global government-approved crypto** |
| Uses latest approved NIST and FIPS cryptography (ECDSA and EdDSA) used by many Western nation states with ability to support other Eastern nation-state backed government cryptography. |
| **Privacy-preserving crypto** |
| Yes, supports BBS privacy-preserving cryptographic key formats. |
| **Digitally signed cryptographic log of changes to the DID Document** |
| No. |
| **Multi-factor binding to DNS** |
| No. |
| **Specification with multiple implementers** |
| Yes, although the specification needs further work and updating. |
| **Scope/domain of the types of entities/subjects addressed/named by a particular method** |
| INEFFECTIVE CRITERIA: Debatably, this seems like a privacy-harming anti-pattern to claim that specific types of entities require specific types of DIDs. |
| **Estimate of the daily transaction volume of each scope/domain** |
| INEFFECTIVE CRITERIA: Debatably, this seems like a privacy harming anti-pattern to be able to count transaction volume of DID usage. Estimating seems fraught as well without hard data. Getting these sorts of counts in decentralized systems is difficult. |
| **DID Methods that do not serve the needs of a particular company or government** |
| INEFFECTIVE CRITERIA: What "do not serve" means is unclear. |
| **Governance: Clear frameworks for updates, dispute resolution, and decision-making** |
| No framework is needed since updates are not supported, disputes could only be about private key possession (and a court with jurisdiction would adjudicate any dispute, and any other decision making does not apply. |
| **Usability: Simple implementation for developers** |
| Yes, as evidenced by the number of implementations and positive developer feedback. |
| **Sustainability: Energy efficiency and eco-friendly infrastructure** |
| Yes, keys take milliseconds to create and a few hundred bytes to store. |
| **Economic Feasibility: DIDs costs of use must be reasonable** |
| Yes, costs are a fraction of the smallest denomination of mainstream currencies (less than $0.0000004 USD for an ECDSA create operation). |
| **Legal Recognition: Cross-border frameworks for DID acceptance** |
| Yes, supports key types approved by multiple national governments. |
| **Revocation and Recovery: Decentralized mechanisms for key rotation and DID recovery** |
| None. |
| **Emerging Markets: Offline-friendly, low-bandwidth** |
| Yes, offline-friendly due to no need for a network look up. |
| **Long-lived DIDs needed for long-lived VCs** |
| Yes, but only if paired with hardware security modules. |
| **Low and predictable marginal cost at scale (millions of accounts)** |
| Yes. |
| **Ability to create and update identifiers rapidly (within seconds)** |
| Yes, within milliseconds for creation. Update is not supported. |
| **Support for key rotation** |
| No. |
| **Reliable and predictable-latency operation, for updating and resolving** |
| Yes. |
| **Resolution should not require additional state or context** |
| Yes. |
| **DIDs are permanent and immutable account identifiers** |
| Yes. |
| **Consider support for various DID Traits: https://identity.foundation/did-traits/** |
| BAD CRITERIA: Traits should be listed directly. |
| **Consider categories defined by DID Rubric: https://www.w3.org/TR/did-rubric/** |
| BAD CRITERIA: Rubric categories should be listed directly. |
| **Who WANTS to standardize the DID method and commits to doing the work?** |
| Digital Bazaar will commit to doing the work through the entire standardization process. |
| **Are there AT LEAST two WG members who support standardization of a DID method?** |
| TBD. |
| **Are there no trademark or IP issues?** |
| None. |
| **Diversity of the set of selected DID methods** |
| BAD CRITERIA: Should be removed as this is a meta-question about the set of selected methods. |
| **At least one ephemeral DID method** |
| This could be considered one of the ephemeral DID Methods. |
| **At least one web-based DID method** |
| This is not a web-based DID Method. |
| **At least one fully decentralized DID method** |
| While it is debatable that this is a fully decentralized DID Method, the lack of update and deactivate features probably disqualify it from what people typically mean by "fully decentralized". |

## Supporting use cases

All [DID Use Cases](https://www.w3.org/TR/did-use-cases/) that do not require
updating or deactivation are supported by this DID Method. This DID Method is
specifically beneficial for the following classes of use cases:

* Strong temporary authentication (account log in via digital signatures)
* Strong temporary authorization (HTTP API service access via digital signatures)
* Strong temporary delegated authorization (cryptographically delegated HTTP API service access)
* Medium-term identification (up to 5 years) if paired with a hardware security module (HSM)
* Document-based identification where proof of possession is bound to a cryptographic key
