# DID method standardization proposal: did:peer

This is a proposal to include `did:peer` in
the initial set of DID methods that will be standardized by the DID Methods WG.

## Description

The `did:peer` DID Method was developed to enable DIDs that are only shared with
the other parties in a relationship. Core features include:

- **Ledgerless**: Does not use any ledger or hosted asset of any form
- **Multiple Keys**: Allows multiple keys in the DID Document
- **Supports Service Endpoints**: Allows service endpoints to be resolved from the identifier
- **All DID Document Features Supported**: All DID Document features are supported
- **Simple Transformation**: Simple transformation into a DID Document
- **Efficient Mode after Transfer**: After the initial DID is exchanged, a short DID may be used in place of the full DID

The `did:peer` method has developed over time, and contains multiple algorithms. Only the current non-deprecated form (numalgo 4) is part of this standardization proposal.

### Benefits

- Extremely Lightweight
- Free from external costs
- Extremely Private
- Enables communication via service endpoints

### Drawbacks

- Static - DID is not updatable, which disallows key rotations or changes to service endpoints. This has been handled by users by switching to a new DID entirely for the additional privacy benfits of changing the identifier itself.

## Existing materials

- [DID Method Specification](https://identity.foundation/peer-did-method-spec/)
- [Implementations](https://github.com/decentralized-identity/did-peer-4)
- Above implementation contains a test suite.

## Meeting the selection criteria

Document here how this DID method meets the [DID method selection criteria](../selection-criteria/).

| **Criteria** | **Details** |
|----------|----------|
| **Alignment with DID Core specification** | Yes, fully compliant with DID specification, with the one exception being the ability to update. |
| **Security and privacy features** | Yes, the DID Method has security and privacy features. |
| **Scalability and performance** | Infinite scalability as a result of not being publicly recorded. Efficiency of large DID is offset via the use of a short form, linked via `alsoKnownAs`. This short form may be used after initial exchange without loss of functionality. |
| **Ease of implementation and use** | Easy, as the only mechanisms are encoding-related, and the encoding was deliberately designed to be as simple as possible. |
| **Community adoption and support** | Used heavily within the DIDComm community. |
| **Compliance with relevant regulations and best practices** | Yes. |
| **Global government-approved crypto** | Yes. The DID Method itself does not rely on cryptography but rather hashing to link the identifier with the contents of the DID Document. This means that it supports any and all cryptography supported by the DID Core specification. |
| **Privacy-preserving crypto** | Yes, see above. |
| **Digitally signed cryptographic log of changes to the DID Document** | No. This DID Method does not allow changes to the DID Document. |
| **Multi-factor binding to DNS** | No. |
| **Specification with multiple implementers** | Yes. |
| **Scope/domain of the types of entities/subjects addressed/named by a particular method** | Expected to be used to represent individuals where privacy concerns are strong and warranted. May also be used by organizations seeking a temporary or unique DID for specific purposes. |
| **Estimate of the daily transaction volume of each scope/domain** | Given its use by individuals, speed, and low cost, we expect the volume of Peer DIDs to be extremely large. |
| **DID Methods that do not serve the needs of a particular company or government** | N/A |
| **Governance: Clear frameworks for updates, dispute resolution, and decision-making** | Updates happen by new additions, not by changing previously set specifications. |
| **Usability: Simple implementation for developers** | Yes. |
| **Sustainability: Energy efficiency and eco-friendly infrastructure** | Yes. Computation required is low. No recording on any backend is performed. The short form allows efficient use after initial transmission. |
| **Economic Feasibility: DIDs costs of use must be reasonable** | Yes. Only hashing is required. No storage exists. |
| **Legal Recognition: Cross-border frameworks for DID acceptance** | Yes, supports all key types. |
| **Revocation and Recovery: Decentralized mechanisms for key rotation and DID recovery** | No. DIDs are static and cannot be updated, revoked, or recovered. |
| **Emerging Markets: Offline-friendly, low-bandwidth** | Fully offline capable with no online requirements. |
| **Long-lived DIDs needed for long-lived VCs** | While technically possible to use a single DID for a long time, this DID method is not suitable for the identification of VC Issuers. They can be used as subject identifiers. |
| **Low and predictable marginal cost at scale (millions of accounts)** | Yes. |
| **Ability to create and update identifiers rapidly (within seconds)** | Yes. |
| **Support for key rotation** | No. |
| **Reliable and predictable-latency operation, for updating and resolving** | Yes. |
| **Resolution should not require additional state or context** | Yes, except if the Short Form is used with parties already aware of the DID. |
| **DIDs are permanent and immutable account identifiers** | Yes. |
| **Consider support for various DID Traits: https://identity.foundation/did-traits/** | TBD. |
| **Consider categories defined by DID Rubric: https://www.w3.org/TR/did-rubric/** | TBD. |
| **Who WANTS to standardize the DID method and commits to doing the work?** | Indicio and BCGov are willing to continue its work on the base spec and implementations. |
| **Are there AT LEAST two WG members who support standardization of a DID method?** | Yes, Indicio and Province of BC. |
| **Are there no trademark or IP issues?** | None. |
| **What type of DID method is this?** | This method provides features not supported in the other proposed DID Methods. It is an **ephemeral** and **fully decentralized** DID Method. |

## Supporting use cases

This method supports all [DID Use Cases](https://www.w3.org/TR/did-use-cases/) involving individuals.
In these cases, the user's ability to use a unique idenfier until further disclosure is critical to their
privacy in the interaction. The ability to create a new DID at will gives users the power to use as many 
as they want or need for their purposes.