# DID method standardization proposal: did:cheqd

This is a proposal to include `did:cheqd` in the initial set of DID methods that will be standardized by the DID Methods WG.

## Description

`did:cheqd` is a blockchain-based DID Method that runs atop the cheqd Network.

- Summary of [DID Method Traits](https://identity.foundation/did-traits/#comparison-of-did-methods)

### Benefits

- Immutable, cryptographically verifiable history of DID Documents and DID Document updates
- Key rotation supported with fully indexed, chronologically ordered and searchable history of DID Documents and associated updates
- Multi-sig supported, with multiple DID Controllers able to be added, or multiple keys listed for `authentication`
- Hosted in a decentralized way, eliminating reliance on DNS, web servers or other centralized storage
- Blockchain-based validation of cryptographic keys referenced or embedded within the `authentication` section of DID Documents, ensuring that only the controller of those keys has the ability to update or deactivate the DID Document
- Deactivation of DIDs supported
- Full support for verification method relationships, whereby different key types can be specified for defined purposes within the DID Document, including `assertionMethod`, `keyAgreement` `capabilityInvocation` and `capabilityDelegation`, including both **referenced** and **embedded** keys as defined in [DID Core](https://www.w3.org/TR/did-1.0/)
- `alsoKnownAs` allows synonymous DIDs to be published in alternative locations, such as on a web server using `did:web` or `did:webvh`
- [DID-Linked Resources](https://w3c-ccg.github.io/DID-Linked-Resources/) supported, with optional inclusion in the DID Document Metadata, to create searchable directories of DIDs and associated collections of resources
- Support for multiple namespaces, including `did:cheqd:testnet` for testing, as well as for `did:cheqd:mainnet` mainnet for full, consensus-backed security
- Transactions for writing `did:cheqd` DIDs in MiCA Regulated Electronic Money Tokens (EMTs), including USDC and EURe
- Clear and [consistent pricing](https://docs.cheqd.io/product/network/cheqd/identity-write-pricing) for DIDs and DID-Linked Resources
- [Decentralized governance framework](https://learn.cheqd.io/governance/start) for updates to software updates or pricing changes for DID Method on cheqd Network, voted through by the validator nodes and delegators who stake the $CHEQ token
- Innovative trust registry / trust infrastructure model natively supported, with hierarchical DID and VC relationships able to be expressed to mirror traditional PKI models that would usually adopt X.509 certificates
- Support in 5+ Open Source SDKs and libraries
- Support for all major credential flavors via these SDKs and libraries, including VCDM (JWT, JSON-LD, SD-JWT) as well as AnonCreds
- Support in both Universal Resolver and Universal Registrar

### Drawbacks

- Token used for underlying transactions ($CHEQ), which may limit adoption owing to lack of regulatory clarity in certain jurisdictions. Although this drawback is mitigated through the support for MiCA regulated stablecoins natively on the network.
- Volatile transaction pricing for DIDs, based on fluctuations in value of $CHEQ.
- Immutability of DIDs, which may be problematic if sensistive data such as Personally Identifiable Information (PII) is pointed to within the `serviceEndpoint` or as a DID-Linked Resource.

## Existing materials

- [DID Method Specification](https://docs.cheqd.io/product/architecture/adr-list/adr-001-cheqd-did-method)
- Implementations
  - [Veramo SDK plugin](https://docs.cheqd.io/product/sdk/veramo-plugin)
  - [Credo](https://credo.js.org/guides/getting-started/set-up/cheqd)
  - [Aries Cloud Agent Python (ACA-Py)](https://docs.cheqd.io/product/sdk/aca-py)
  - [Dock SDK](https://github.com/docknetwork/sdk)
  - [Walt.id Community Stack](https://walt.id/blog/p/community-stack)
  - [cheqd Studio](https://cheqd.io/solutions/cheqd-studio/)
  - [Universal Registrar Driver](https://github.com/decentralized-identity/universal-registrar)
  - [Universal Resolver Driver](https://github.com/decentralized-identity/universal-resolver)
  - [Vidos Universal Resolver](https://vidos.id/docs/services/resolver)
- Block Explorer (including ability to filter by DID transaction types)
  - [Mainnet transactions](https://explorer.cheqd.io/transactions)
  - [Testnet transactions](https://testnet-explorer.cheqd.io/transactions)
- [cheqd Governance Framework](https://learn.cheqd.io/governance/start)
- [Documentation and tutorials for use of SDKs or APIs](https://docs.cheqd.io/product)
- No test suite exists as of Jan 2025

## Meeting the selection criteria

| **Criteria** | **Details** |
|----------|----------|
| **Alignment with DID Core specification** | Yes, fully compliant with DID specification. |
| **Security and privacy features** | Yes, the DID Method has security and privacy features primarily established via the resilience and security of the underlying cheqd network blockchain. |
| **Scalability and performance** | Support for between 5000 and 10,000 transactions per second, with multiple transactions allowed and batched per block |
| **Ease of implementation and use** | Multiple implementation routes, via SDKs and APIs as well as full support in the Universal Registrar and Resolver. Support for `did:cheqd:testnet` and `did:cheqd:mainnet` for different purposes. Clear documentation and tutorials written for each seperate integration pathway  |
| **Community adoption and support** | Over 300,000 DIDs on testnet and support in five of the largest industry SDKs, as well as over ten identity applications |
| **Compliance with relevant regulations and best practices** | Yes, and actively working with EU on establishing best practices for using DLT as trust infrastructure for the EU Digital Identity market. |
| **Global government-approved crypto** | The DID Method itself uses the latest approved NIST and FIPS cryptography (ECDSA and EdDSA) used by many Western nation-states with ability to support cryptography backed by other Eastern nation-state governments. The DID Method is defined to support evolving the cryptography used by the DID Method through the versioning of the specification and DIDs using the specification.  |
| **Privacy-preserving crypto** | Yes, supports BBS privacy-preserving cryptographic key formats embedded within the DIDDoc. Any DID-Core compatible key formats can be defined in verification method relationships within the DID Documents, even if they are not natively validated against by the underlying cheqd network. AnonCreds are also supported as a credential format on top of cheqd, with Camenisch-Lysyanskaya (CL) signatures. |
| **Digitally signed cryptographic log of changes to the DID Document** | Yes. |
| **Multi-factor binding to DNS** | No. |
| **Specification with multiple implementers** | Yes, multiple independent SDKs in different programming languages exist for interacting with the DID method. |
| **Scope/domain of the types of entities/subjects addressed/named by a particular method** | Expected to be used primarily for organizational entities, but that is not limited by the specification. |
| **Estimate of the daily transaction volume of each scope/domain** | Yes, daily metrics are actively recorded and provided via services such as [GoDiddy Stats](https://stats.godiddy.com/cheqd). |
| **DID Methods that do not serve the needs of a particular company or government** | The cheqd Network and associated DID Method is separate from cheqd as a profit making entity and is controlled by its decentralized governance framework. As such, it is a public resource which may be used via open source libraries without a tie to any company or government. |
| **Governance: Clear frameworks for updates, dispute resolution, and decision-making** | Established decentralized governance framework, with clear documentation, discussion forum and simple voting process. There have been 60 proposals on mainnet as of January 2025. |
| **Usability: Simple implementation for developers** | Yes, as evidenced by developers building across SDKs, APIs and Registrar implementations |
| **Sustainability: Energy efficiency and eco-friendly infrastructure** | While there is energy used in the running of a blockchain network, the maintainers have sought to offset carbon generated by validators running on network via [Regen Network](https://www.registry.regen.network/) |
| **Economic Feasibility: DIDs costs of use must be reasonable** | Yes, costs are set via the decentralized governance framework. Testnet is free to write to; and, mainnet is approximately $2 USD per DID create. |
| **Legal Recognition: Cross-border frameworks for DID acceptance** | Yes, supports key types approved by multiple national governments, as well as compliance in terms of the underlying asset to write to the network (e.g. MiCA compliant Electronic Money Tokens such as USDC). |
| **Revocation and Recovery: Decentralized mechanisms for key rotation and DID recovery** | Key rotation is inherent in the DID Method and is secure and verifiable, independent of DNS. Revocation is supported per the DID-Core specification. |
| **Emerging Markets: Offline-friendly, low-bandwidth** | Not specifically tested. For certain operations, a concept of "light clients" exists which allow interacting with the underlying network without running a full node. |
| **Long-lived DIDs needed for long-lived VCs** | Yes, DIDs and associated DID Documents, as well as past, present and future versions of these are immutably stored for use in long-lived VCs |
| **Low and predictable marginal cost at scale (millions of accounts)** | Yes, and price can be adjusted as scale increases accordingly. |
| **Ability to create and update identifiers rapidly (within seconds)** | Yes, support for 5000 to 10,000 transactions per second |
| **Support for key rotation** | Yes, with a verifiable history of the versions of the DID, past keys and rotations. |
| **Reliable and predictable-latency operation, for updating and resolving** | Yes. |
| **Resolution should not require additional state or context** | Yes. |
| **DIDs are permanent and immutable account identifiers** | Yes.   |
| **Consider support for various DID Traits: https://identity.foundation/did-traits/** | Yes, full suite of [DID traits are identified and referenced here](https://github.com/decentralized-identity/did-traits/blob/main/methods/cheqd.json). |
| **Consider categories defined by DID Rubric: https://www.w3.org/TR/did-rubric/** | Yes. |
| **Who WANTS to standardize the DID method and commits to doing the work?** | Cheqd Foundation Limited is able to fund the standardization of the method via its community pool, and the work will likely be carried out by the maintainers of the method |
| **Are there AT LEAST two WG members who support standardization of a DID method?** | Yes, cheqd and Danube Tech |
| **Are there no trademark or IP issues?** | To the best of our knowledge, `did:cheqd` does not infringe upon any existing intellectual property rights, patents, or trademarks. If any unforeseen intellectual property or trademark concerns arise, Cheqd Foundation is committed to addressing them transparently and in good faith. In the event that a legitimate claim is identified, Cheqd Foundation will assess the matter and, where appropriate, make a voluntary donation or take other reasonable actions to ensure continued open and equitable access. |
| **What type of DID method is this?** | Decentralized |

## Supporting use cases

- DIDs for non-natural persons, including legal entities, objects, processes.
- DIDs for verifiable credential issuers.
- DID-based trust registries, using merkle trees of trusted relationships between legal entities.
- DIDs for digital product passports, supply chain traceability and associated metadata stored as linked resources.
- DIDs for establishing directories of immutable information, such as for land registries, content integrity, databases.
- Commercial models for verifiable credentials, including support for encryption and decryption of DID-Linked resources including schemas, status lists or trust registries.
