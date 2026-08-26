# DID method standardization proposal: did:hedera

This is a proposal to include `did:hedera` in the initial set of DID methods that will be standardized by the DID Methods WG.

## Description

The `did:hedera` DID Method defines a binding of DID architecture to Hedera ledger and corresponding DID registration / resolution mechanisms.

Hedera is a public ledger that uses the Hashgraph consensus algorithm, providing high throughput, low fees, and asynchronous Byzantine Fault Tolerance (aBFT).
Underlying DLT is open-source and available under [Hiero LFDT project](https://github.com/hiero-ledger).

The `did:hedera` DID Method leverages Hiero Consensus Service (HCS) to store a verifiable log (history) of update operations performed on particual DID Document.
These operations are represented by HCS messages and stored in a unique HCS topic for each DID, providing convenient tracking of full history and high scalability.

### Benefits

- High Performance: Leverages Hedera's high throughput (10,000+ TPS) and low latency (3-5 seconds finality).
- Security: Built on aBFT consensus, the gold standard for security in distributed systems.
- Low and Predictable Fees: Transactions on Hedera have low, fixed fees pegged to USD, making identity operations economically viable at scale.
- Full Document History: HCS-based DIDs maintain a complete, verifiable audit trail of all changes to the DID document.
- Ecosystem Interoperability: Compatible with various SDKs and tools in the Hedera ecosystem, also supported in OpenWallet Foundation projects (ACA-Py, Credo).
- Decentralized Governance: Hedera network is governed by the Hedera Council, a diverse group of leading global organizations.

### Drawbacks

- Dependency on Hedera Network: Requires access to the Hedera network and HBAR for transaction fees.
- Relative complexity of HCS Resolution: Resolving HCS-based DIDs requires processing a sequence of messages (updates history), which may be more complex than simple state lookups, although this is mitigated by mirror nodes and optimizations in SDKs.

## Existing materials

- [Hedera DID Method Specification](https://github.com/hashgraph/did-method)
- [Hiero AnonCreds Method leveraging Hedera DID](https://hiero-ledger.github.io/identity-collaboration-hub/hiero-anoncreds-method/)
- Implementations
  - [Hiero DID SDK JavaScript](https://github.com/hiero-ledger/hiero-did-sdk-js)
  - [Hiero DID SDK Python](https://github.com/hiero-ledger/hiero-did-sdk-python)
  - [Universal Resolver Driver for did:hedera](https://github.com/hiero-ledger/identity-collaboration-hub/tree/main/universal-resolver-driver)
- [Heka Identity Platform supporting Hedera DID](https://github.com/hiero-ledger/heka-identity-platform)
- Plugins for Hedera DID and AnonCreds integration to OpenWallet Foundation projects
  - [Hedera module for OWF Credo](https://github.com/openwallet-foundation/credo-ts/tree/main/packages/hedera)
  - [Hedera plugin for OWF ACA-Py](https://github.com/openwallet-foundation/acapy)
- [Hedera Governance](https://hederacouncil.org)
- [Hiero Identity Collaboration Hub](https://github.com/hiero-ledger/identity-collaboration-hub/)

## Is this DID method already involved in a standardization process? If so, where?

The `did:hedera` method has been developed with Hiero / Hedera community input and is documented in a formal specification on GitHub under Hashgraph org.
It is also listed in the W3C DID Method Registry.

## Meeting the selection criteria

| **Criteria** | **Details** |
|--------------|-------------|
| **Alignment with DID Core specification** | Yes, fully compliant with DID specification. |
| **Security and privacy features** | Uses Hedera's aBFT consensus for high security / reliability and supports various cryptographic key types for privacy. |
| **Scalability and performance** | Hedera ledger provides a high throughput (10,000+ TPS) and fast finality (3-5 seconds) for transactions. Client side performance scalability naturaly depends on CPU and memory constraints. |
| **Ease of implementation and use** | Multiple SDKs (JS, Python), plugins for integration with OWF projects and corresponding documentation available. Supported in the Universal Resolver. |
| **Community adoption and support** | Supported by the Hedera / Hiero ecosystem that includes various enterprise partners. |
| **Compliance with relevant regulations and best practices** | Hedera's governance and technical design are built with enterprise and regulatory requirements in mind. |
| **Global government-approved crypto** | Supports standard Ed25519 and ECDSA (secp256k1) keys, which are widely recognized and used. |
| **Privacy-preserving crypto** | Yes, supports BBS privacy-preserving cryptographic key formats within the DIDDoc. |
| **Digitally signed cryptographic log of changes to the DID Document** | Yes, the method provides such verifiable log in a form of HCS messages that constitute the DID document's update history. |
| **Multi-factor binding to DNS** | No. |
| **Specification with multiple implementers** | The spec is implemented in multiple decentralized identity SDKs hosted under Hiero project and GH org. Initial versions of SDKs were developed by Hashgraph, relevant versions are developed and maintained by DSR Corporation and The Hashgraph Association. |
| **Scope/domain of the types of entities/subjects addressed/named by a particular method** | Expected to be used primarily for organizational entities, but that is not limited by the specification - method can be used for individuals, IoT devices and other entities. |
| **Estimate of the daily transaction volume of each scope/domain** | High potential volume given Hedera's overall network activity, though specific DID transaction metrics vary depending on a use case. |
| **DID Methods that do not serve the needs of a particular company or government** | Hedera is governed by a decentralized council of 30+ diverse global organizations. |
| **Governance: Clear frameworks for updates, dispute resolution, and decision-making** | Governance through the transparent HIP (Hiero Improvement Proposal) process. |
| **Usability: Simple implementation for developers** | Yes, evidenced by available SDKs and integration into existing identity platforms. |
| **Sustainability: Energy efficiency and eco-friendly infrastructure** | Hedera is carbon-negative and highly energy-efficient. |
| **Economic Feasibility: DIDs costs of use must be reasonable** | Yes, fixed fees in USD ($0.0001 for HCS messages) make it very affordable. |
| **Legal Recognition: Cross-border frameworks for DID acceptance** | Used in various international supply chain and identity projects. |
| **Revocation and Recovery: Decentralized mechanisms for key rotation and DID recovery** | No, key rotation does not have decentralized mechanisms. DID recovery is not supported. |
| **Emerging Markets: Offline-friendly, low-bandwidth** | No onffline-friendly feeatures. Low-bandwidth scenarios can be handled by using Hedera / Hiero Mirror Nodes to resolve DIDs efficiently. |
| **Long-lived DIDs needed for long-lived VCs** | Yes, DIDs on Hedera are permanent and their history is immutably stored. |
| **Low and predictable marginal cost at scale (millions of accounts)** | Yes, thanks to fixed USD-pegged fees for HCS transactions. |
| **Ability to create and update identifiers rapidly (within seconds)** | Yes, within 3-5 seconds. |
| **Support for key rotation** | Yes, it's one of core features of the method. |
| **Reliable and predictable-latency operation, for updating and resolving** | Yes, highly predictable performance with additional read operations optimization practices in SDKs. |
| **Resolution should not require additional state or context** | Yes. |
| **DIDs are permanent and immutable account identifiers** | Yes. |
| **Consider support for various DID Traits: <https://identity.foundation/did-traits/>** | Yes, many traits are supported (add link to the table) |
| **Consider categories defined by DID Rubric: <https://www.w3.org/TR/did-rubric/>** | Yes. |
| **Who WANTS to standardize the DID method and commits to doing the work?** | Hiero Identity community and users, potentially supported by Hedera Council Members (to clarify). |
| **Are there AT LEAST two WG members who support standardization of a DID method?** | TBD |
| **Are there no trademark or IP issues?** | Hedera's technology is open-source (Apache 2.0). |
| **What type of DID method is this?** | Decentralized |

## Supporting use cases

All [DID Use Cases](https://www.w3.org/TR/did-use-cases/) that do not require extended offline usage are supported by this DID Method.

This DID Method is specifically beneficial for the following classes of use cases:

- DIDs for governments or other large organizations
- Enterprises, such as verifiable credential issuers, verifiers and participants in verifiable supply chains
- IoT device identity that can leverage efficiency and low latency provided by Hiero / Hedera ledger
