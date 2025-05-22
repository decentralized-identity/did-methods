# DID method standardization proposal: did:mdip

This is a proposal to include `did:mdip` to the set of DID methods recognized and recommended by the WIF DID Methods WG.

## Description

The MDIP (MultiDimensional Identity Protocol) DID method specification conforms to the requirements specified in the [DID specification](https://www.w3.org/TR/did-core/) currently published by the W3C Credentials Community Group. The MDIP DID method (`did:mdip`) is designed to support a P2P identity layer with secure decentralized [verifiable credentials](https://www.w3.org/TR/vc-data-model-2.0/). MDIP DIDs are used for agents (e.g., users, issuers, verifiers, and MDIP nodes) and assets (e.g., verifiable credentials, verifiable presentations, schemas, challenges, and responses).

### DID Lifecycle

![did-lifecycle.png](https://github.com/KeychainMDIP/kc/blob/main/doc/mdip/did-lifecycle.png)

All MDIP DIDs begin life anchored to a CAS (Content-Addressable Storage) such as IPFS. Once created they can be used immediately by any application or service connected to an MDIP node. Subsequent updates to the DID (meaning that a document associated with the DID changes) are registered on a registry such as a blockchain (BTC, ETH, etc) or a decentralized database (e.g. hyperswarm). The registry is specified at DID creation so that nodes can determine which single source of truth to check for updates.

The *key concept of this design* is that MDIP DID creation is decentralized through through the CAS, and DID updates are decentralized through the registry specified in the DID creation. The MDIP DID is decentralized for its whole lifecycle, which is a hard requirement of DIDs.

## Overview

**Gatekeeper**: A Keychain MDIP node includes several interoperating microservices. If you follow the dependency arrows on the diagram below, you will end up at the central core service, the [Gatekeeper service](https://github.com/KeychainMDIP/kc/blob/main/services/gatekeeper/server/README.md) responsible for maintaining the integrity of the local DID database. 

**Mediators**: The mediators are responsible for connecting the Gatekeeper to various networks such as [Hyperswarm](https://github.com/KeychainMDIP/kc/blob/main/services/mediators/hyperswarm/README.md). The TBTC (testnet Bitcoin) and TFTC (testnet Feathercoin) mediators are both instances of the [Satoshi mediator](https://github.com/KeychainMDIP/kc/blob/main/services/mediators/satoshi/README.md) since they are derived from Bitcoin core (they differ only in how they are configured). 

**Keymaster**: [Keymaster](https://github.com/KeychainMDIP/kc/blob/main/packages/keymaster/README.md) is the MDIP client responsible for holding the private keys and signing DID operations (create, update, delete) sent to Gatekeeper. 

**Wallets**: The [browser web wallet](https://github.com/KeychainMDIP/kc/blob/main/services/gatekeeper/client/README.md), [browser extension](https://github.com/KeychainMDIP/kc/blob/main/browser/chrome-extension/README.md), and [Keymaster service](https://github.com/KeychainMDIP/kc/blob/main/services/keymaster/server/README.md) all use the [Keymaster library](https://github.com/KeychainMDIP/kc/blob/main/packages/keymaster/README.md). The [server web wallet](https://github.com/KeychainMDIP/kc/blob/main/services/keymaster/client/README.md) is the same as the browser web wallet, except it is configured to talk to the Keymaster service instead of hosting its own wallet. It uses the same [KeymasterClient](https://github.com/KeychainMDIP/kc/blob/main/packages/keymaster/src/keymaster-sdk.ts) as the kc CLI. 

**DID Explorer**: The [explorer](https://github.com/KeychainMDIP/kc/blob/main/services/explorer/README.md) and [search-server](https://github.com/KeychainMDIP/kc/blob/main/services/search-server/README.md) provide DID resolution, search and general interaction with DIDs and DID Documents.

**CLI**: There are two CLI (command line interface) components: [kc](https://github.com/KeychainMDIP/kc/blob/main/scripts/keychain-cli.js) for talking to the Keymaster service, and [admin](https://github.com/KeychainMDIP/kc/blob/main/scripts/admin-cli.js) for talking to the Gatekeeper service. The admin script uses the same [GatekeeperClient](https://github.com/KeychainMDIP/kc/blob/main/packages/gatekeeper/README.md) as the Keymaster service and the mediators.

**Authentication Demo**: A reference MDIP-enabled client application that demonstrates the challenge/response based authentication process. The demo also establishes privileged groups of users categorized as members, moderators, admins, or owner. [MDIP auth-demo repository](https://github.com/KeychainMDIP/auth-demo)

![keychain-node.png](https://github.com/KeychainMDIP/kc/blob/main/keychain-node.png)

## Existing materials

* [Keychain Reference Implementation](https://github.com/KeychainMDIP/kc)
* [MDIP DID Scheme](https://github.com/KeychainMDIP/kc/blob/main/doc/mdip/scheme.md)
* [MDIP Gatekeeper OpenAPI Specs](https://github.com/KeychainMDIP/kc/blob/main/doc/gatekeeper-api.json)
* [MDIP Keymaster OpenAPI Specs](https://github.com/KeychainMDIP/kc/blob/main/doc/keymaster-api.json)
* [MDIP Authentication Process and Demo](https://github.com/KeychainMDIP/auth-demo)

## Meeting the selection criteria

Document here how this DID method meets the [DID method selection criteria](../selection-criteria/).

| **Criteria** | **Details** |
|----------|----------|
| **Alignment with DID Core specification** | Lorem ipsum... |
| **Security and privacy features** | Lorem ipsum... |
| **Scalability and performance** | Lorem ipsum... |
| **Ease of implementation and use** | Lorem ipsum... |
| **Community adoption and support** | Lorem ipsum... |
| **Compliance with relevant regulations and best practices** | Lorem ipsum... |
| **Global government-approved crypto** | Lorem ipsum... |
| **Privacy-preserving crypto** | Lorem ipsum... |
| **Digitally signed cryptographic log of changes to the DID Document** | Lorem ipsum... |
| **Multi-factor binding to DNS** | Lorem ipsum... |
| **Specification with multiple implementers** | Lorem ipsum... |
| **Scope/domain of the types of entities/subjects addressed/named by a particular method** | Lorem ipsum... |
| **Estimate of the daily transaction volume of each scope/domain** | Lorem ipsum... |
| **DID Methods that do not serve the needs of a particular company or government** | Lorem ipsum... |
| **Governance: Clear frameworks for updates, dispute resolution, and decision-making** | Lorem ipsum... |
| **Usability: Simple implementation for developers** | Lorem ipsum... |
| **Sustainability: Energy efficiency and eco-friendly infrastructure** | Lorem ipsum... |
| **Economic Feasibility: DIDs costs of use must be reasonable** | Lorem ipsum... |
| **Legal Recognition: Cross-border frameworks for DID acceptance** | Lorem ipsum... |
| **Revocation and Recovery: Decentralized mechanisms for key rotation and DID recovery** | Lorem ipsum... |
| **Emerging Markets: Offline-friendly, low-bandwidth** | Lorem ipsum... |
| **Long-lived DIDs needed for long-lived VCs** | Lorem ipsum... |
| **Low and predictable marginal cost at scale (millions of accounts)** | Lorem ipsum... |
| **Ability to create and update identifiers rapidly (within seconds)** | Lorem ipsum... |
| **Support for key rotation** | Lorem ipsum... |
| **Reliable and predictable-latency operation, for updating and resolving** | Lorem ipsum... |
| **Resolution should not require additional state or context** | Lorem ipsum... |
| **DIDs are permanent and immutable account identifiers** | Yes. |
| **Consider support for various DID Traits: <https://identity.foundation/did-traits/>** | Lorem ipsum...  |
| **Consider categories defined by DID Rubric: <https://www.w3.org/TR/did-rubric/>** | Lorem ipsum... |
| **Who WANTS to standardize the DID method and commits to doing the work?** | Lorem ipsum... |
| **Are there AT LEAST two WG members who support standardization of a DID method?** | LLorem ipsum... |
| **Are there no trademark or IP issues?** | Lorem ipsum... |
| **What type of DID method is this?** | Ephemeral / Web-based / Decentralized / Other (please choose one/specify) |

## Is this DID method already involved in a standardization process? If so, where?

Some DID Methods have or have had standardization working groups looking at them before. Please provide the relevant background for this method.

## Supporting use cases

Document here how this DID method supports concrete use cases.
