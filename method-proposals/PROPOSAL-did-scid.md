# DID method standardization proposal: did:scid

This is a proposal to include `did:scid` in the initial set of DID methods that will be standardized by the DID Methods WG.

## Description

The `did:scid` method is designed to maximize the security, privacy, and portability benefits of self-certifying identifiers (SCIDs) independent of the specific type of SCID. It potentially augments a number of existing DID methods such as `did:webvh`, `did:webs`, and `did:peer` by specifying the location of the verification metatdata in the identifier.

## Existing materials

[DID Method Specification](https://lf-toip.atlassian.net/wiki/spaces/HOME/pages/88572360/DID+SCID+Method+Specification)

## Meeting the selection criteria

| **Criteria** |
| -------- |
| **Alignment with DID Core specification** |
| Fully compliant with core spec. |
| **Security and privacy features** |
| High privacy and security are possible depending on the underlying method represented by the `did:scid`. |
| **Scalability and performance** |
| Can be very scalable and performant depending on the underlying method. |
| **Ease of implementation and use** |
| Variable. It depends on the underlying method. |
| **Community adoption and support** |
| Adoption and support varies, but is generally wide. Examples of underlying methods include `did:webvh`, `did:webs`, `did:peer`, and `did:jlinc`|
| **Compliance with relevant regulations and best practices** |
| Generally highly compliant.|
| **Global government-approved crypto** |
| Yes. |
| **Privacy-preserving crypto** |
| Yes. |
| **Digitally signed cryptographic log of changes to the DID Document** |
| Yes. |
| **Multi-factor binding to DNS** |
| Unkown. |
| **Specification with multiple implementers** |
| Dependent on underlying method. |
| **Scope/domain of the types of entities/subjects addressed/named by a particular method** |
| Wide. |
| **Estimate of the daily transaction volume of each scope/domain** |
| Unkown. |
| **DID Methods that do not serve the needs of a particular company or government** |
| Does not. |
| **Governance: Clear frameworks for updates, dispute resolution, and decision-making** |
| Yes. The current standardization body is Trust-Over-IP (TOIP) |
| **Usability: Simple implementation for developers** |
| Depends on underlying method. |
| **Sustainability: Energy efficiency and eco-friendly infrastructure** |
| Unkown. |
| **Economic Feasibility: DIDs costs of use must be reasonable** |
| Unknown. |
| **Legal Recognition: Cross-border frameworks for DID acceptance** |
| Presumably good. |
| **Revocation and Recovery: Decentralized mechanisms for key rotation and DID recovery** |
| Absolutely. |
| **Emerging Markets: Offline-friendly, low-bandwidth** |
| Yes. |
| **Long-lived DIDs needed for long-lived VCs** |
| Yes. |
| **Low and predictable marginal cost at scale (millions of accounts)** |
| Unkown. |
| **Ability to create and update identifiers rapidly (within seconds)** |
| Yes. |
| **Support for key rotation** |
| Yes. |
| **Reliable and predictable-latency operation, for updating and resolving** |
| Yes. |
| **Resolution should not require additional state or context** |
| Yes. |
| **DIDs are permanent and immutable account identifiers** |
| Unsure |
| **Consider support for various DID Traits: https://identity.foundation/did-traits/** |
| Updateable, Updateable Service Endpoints, Deactivatable, Deletable, Self-Certifying, Rotatable Verification Methods, Pre-rotation of Keys, Multi-Signature Verification Method, Globally Resolvable, Centrally Hosted, United States of America NIST-approved Cryptography |
| **Consider categories defined by DID Rubric: https://www.w3.org/TR/did-rubric/** |
| Not evaluated. |
| **Who WANTS to standardize the DID method and commits to doing the work?** |
| Trust-Over-IP. |
| **Are there AT LEAST two WG members who support standardization of a DID method?** |
| Yes. |
| **Are there no trademark or IP issues?** |
| None. |
| **Diversity of the set of selected DID methods** |
| n/a |
| **At least one ephemeral DID method** |
| Yes. |
| **At least one web-based DID method** |
| Yes. |
| **At least one fully decentralized DID method** |
| Yes. |

## Supporting use cases

Various
