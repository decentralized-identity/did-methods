# DID Method Standardization Proposal: did:webs

This is a proposal to include `did:webs` in the initial set of DID methods to be standardized by the DID Methods WG.

## Description

Like its cousin, `did:web`, the `did:webs` method uses traditional web infrastructure to publish DIDs and make them discoverable. However, unlike `did:web`, this method’s trust is not rooted in DNS, webmasters, X.509 certificates, or certificate authorities. Instead, it utilizes [KERI](https://trustoverip.github.io/tswg-keri-specification/) to provide a secure chain of cryptographic key events managed by those who control the identifier.

## Existing Materials

* [DID Method Specification](https://trustoverip.github.io/tswg-did-method-webs-specification/)
* [Reference implementation](https://github.com/GLEIF-IT/did-webs-resolver)

## Is this DID method already involved in a standardization process? If so, where?

Part of the [KERI Suite Working Group](https://lf-toip.atlassian.net/wiki/spaces/HOME/pages/22992904/DID+WebS+Method+Task+Force) at the Trust Over IP Foundation.

## Meeting the Selection Criteria

Documenting how this DID method meets the [DID method selection criteria](../selection-criteria/).

| **Criteria** | **Details** |
|--------------|-------------|
| **Alignment with DID Core specification** | Fully compliant with core specification. |
| **Security and privacy features** | Security is robust due to KERI. However, publication and discoverability depend on the Web, which diminishes decentralization and privacy. |
| **Scalability and performance** | With the proper infrastructure, `did:webs` will scale and perform well. |
| **Ease of implementation and use** | There is a significant learning curve due to the use of KERI/ACDC/CESR, though the usage is potentially simplified with the availability of the reference implementation. |
| **Community adoption and support** | There is a [KERI Suite Working Group](https://lf-toip.atlassian.net/wiki/spaces/HOME/pages/56819755/KERI+Suite+Working+Group) at Trust-Over-IP (TOIP) and an active [developer group](https://github.com/WebOfTrust/keri). Adoption is minimal currently, but organizations like the [Global Legal Identifier Foundation (GLEIF)](https://www.gleif.org/en) are active champions. |
| **Compliance with relevant regulations and best practices** | Highly compliant. Uses only well-known, accepted cryptography and derives best-in-class security and privacy practices from KERI. |
| **Global government-approved crypto** | All cryptography is based on current government-approved standards. |
| **Privacy-preserving crypto** | The cryptography is highly privacy-preserving. |
| **Digitally signed cryptographic log of changes to the DID Document** | The log tracks key state. Any version of the DID document can be regenerated from log information. |
| **Multi-factor binding to DNS** | No. |
| **Specification with multiple implementers** | There is a single, reference implementation of `did:webs` but multiple implementations of KERI. |
| **Scope/domain of the types of entities/subjects addressed/named by a particular method** | Wide. |
| **Estimate of the daily transaction volume of each scope/domain** | Unknown. GLEIF has performed some testing. |
| **DID Methods that do not serve the needs of a particular company or government** | Does not. |
| **Governance: Clear frameworks for updates, dispute resolution, and decision-making** | Yes. The KERI Suite Working Group at Trust over IP Foundation. |
| **Usability: Simple implementation for developers** | There is a simple reference implementation available for developers. |
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
| **Resolution does not require additional state or context** | Resolution requires only the Key Event Log (KEL) stream and Transaction Event Log (TEL) and Designated Alias ACDC data supplied as a CESR stream from the host. |
| **DIDs as permanent and immutable identifiers** | Yes, the KERI identifier remains stable and long-term, while key states can change. |
| **Support for various DID Traits** | Updateable, Updateable Service Endpoints, Deactivatable, Deletable, Self-Certifying, Rotatable Verification Methods, Pre-rotation of Keys, Multi-Signature Verification Method, Globally Resolvable, Centrally Hosted, NIST-approved Cryptography. |
| **Consider categories defined by DID Rubric** | Not evaluated. |
| **Support for standardization by interested parties** | ToIP, GLEIF, and other public and private entities are committed to standardization. Financial subsidies are likely. |
| **Support from at least two WG members** | Yes. |
| **No trademark or IP issues** | None. |
| **What type of DID method is this?** | Ephemeral, Web-based |

## Supporting Use Cases

The `did:webs` method supports all use cases of other web-based identifiers (like `did:web`). It combines high discoverability with robust security.
