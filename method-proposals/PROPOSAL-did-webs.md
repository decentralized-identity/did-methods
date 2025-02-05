# DID Method Standardization Proposal: did:webs

This is a proposal to include `did:webs` in the initial set of DID methods to be standardized by the DID Methods WG.

## Description

Like its cousin, `did:web`, the `did:webs` method uses traditional web infrastructure to publish DIDs and make them discoverable. However, unlike `did:web`, this method’s trust is not rooted in DNS, webmasters, X.509 certificates, or certificate authorities. Instead, it utilizes [KERI](https://trustoverip.github.io/tswg-keri-specification/) to provide a secure chain of cryptographic key events managed by those who control the identifier.

## Existing Materials

* [DID Method Specification](https://trustoverip.github.io/tswg-did-method-webs-specification/)
* A somewhat outdated but still helpful reference [implementation](https://github.com/hyperledger-labs/did-webs-resolver)

## Meeting the Selection Criteria

Documenting how this DID method meets the [DID method selection criteria](../selection-criteria/).

| **Criteria** | **Details** |
|--------------|-------------|
| **Alignment with DID Core specification** | Fully compliant with core specification. |
| **Security and privacy features** | Security is robust due to KERI. However, publication and discoverability depend on the Web, which diminishes decentralization and privacy. |
| **Scalability and performance** | With the proper infrastructure, `did:webs` will scale and perform well. |
| **Ease of implementation and use** | The implementation learning curve is moderate to high due to KERI. Users must demonstrate greater accountability, thoughtfulness, and autonomy compared to other methods. |
| **Community adoption and support** | There is a [KERI working group](https://www.trustoverip.org/our-work/working-groups/) at Trust-Over-IP (TOIP) and an active [developer group](https://github.com/WebOfTrust/keri). Adoption is minimal currently, but organizations like the [Global Legal Identifier Foundation (GLEIF)](https://www.gleif.org/en) are active champions. |
| **Compliance with relevant regulations and best practices** | Highly compliant. |
| **Global government-approved crypto** | All cryptography is based on current government-approved standards. |
| **Privacy-preserving crypto** | The cryptography is highly privacy-preserving. |
| **Digitally signed cryptographic log of changes to the DID Document** | Yes. |
| **Multi-factor binding to DNS** | Unknown. |
| **Specification with multiple implementers** | Partial. There are multiple implementations of KERI but not necessarily of `did:webs` itself. |
| **Scope/domain of the types of entities/subjects addressed/named by a particular method** | Wide. |
| **Estimate of the daily transaction volume of each scope/domain** | Unknown. |
| **DID Methods that do not serve the needs of a particular company or government** | Does not. |
| **Governance: Clear frameworks for updates, dispute resolution, and decision-making** | Yes. The current standardization body is Trust-over-IP (ToIP). |
| **Usability: Simple implementation for developers** | Most aspects of the reference implementation are complete, with active development of missing capabilities underway. |
| **Sustainability: Energy efficiency and eco-friendly infrastructure** | Highly energy-efficient, as identifier creation is inexpensive and infrastructure can be tailored to scale. |
| **Economic Feasibility: Reasonable costs** | The cost of creating each `did:webs` identifier is trivial, and maintaining the infrastructure is low-cost. |
| **Legal Recognition: Cross-border frameworks for DID acceptance** | The `did:webs` method leverages KERI, and the growing legal recognition of the vLEI ecosystem supports its prospects. |
| **Revocation and Recovery: Decentralized mechanisms** | Yes, fully supported. |
| **Emerging Markets: Offline-friendly, low-bandwidth** | Yes. |
| **Long-lived DIDs for long-lived VCs** | Yes. |
| **Low and predictable marginal cost at scale** | Yes. Infrastructure providers are emerging to commoditize key services (e.g., healthKERI, KERIon, GLEIF). |
| **Ability to create and update identifiers rapidly (within seconds)** | Yes. |
| **Support for key rotation** | Yes. |
| **Reliable and predictable-latency operation for updates and resolutions** | Yes. |
| **Resolution does not require additional state or context** | Resolution requires only the Key Event Log (KEL) stream and Transaction Event Log (TEL) data supplied as a CESR stream from the host. |
| **DIDs as permanent and immutable identifiers** | Yes, the KERI identifier remains stable and long-term, while key states can change. |
| **Support for various DID Traits** | Updateable, Updateable Service Endpoints, Deactivatable, Deletable, Self-Certifying, Rotatable Verification Methods, Pre-rotation of Keys, Multi-Signature Verification Method, Globally Resolvable, Centrally Hosted, NIST-approved Cryptography. |
| **Consider categories defined by DID Rubric** | Not evaluated. |
| **Support for standardization by interested parties** | ToIP, GLEIF, and other private entities are committed to standardization. Financial subsidies are likely. |
| **Support from at least two WG members** | Yes. |
| **No trademark or IP issues** | None. |
| **What type of DID method is this?** | Ephemeral, Web-based |

## Supporting Use Cases

The `did:webs` method supports all use cases of other web-based identifiers (like `did:web`). It combines high discoverability with robust security.