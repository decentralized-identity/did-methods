# DID method standardization proposal: did:mdip

This is a proposal to include `did:mdip` to the set of DID methods recognized and recommended by the WIF DID Methods WG.

## Description

The MDIP (MultiDimensional Identity Protocol) DID method specification conforms to the requirements specified in the [DID specification](https://www.w3.org/TR/did-core/) currently published by the W3C Credentials Community Group. The MDIP DID method (`did:mdip`) is designed to support a P2P identity layer with secure decentralized [verifiable credentials](https://www.w3.org/TR/vc-data-model-2.0/). MDIP DIDs are used for agents (e.g., users, issuers, verifiers, and MDIP nodes) and assets (e.g., verifiable credentials, verifiable presentations, schemas, challenges, and responses).

### DID Lifecycle

![did-lifecycle.png](https://github.com/KeychainMDIP/kc/blob/main/doc/mdip/did-lifecycle.png)

All MDIP DIDs begin life anchored to a CAS (Content-Addressable Storage) such as IPFS. Once created they can be used immediately by any application or service connected to an MDIP node. Subsequent updates to the DID (meaning that a document associated with the DID changes) are registered on a registry such as a blockchain (BTC, ETH, etc) or a decentralized database (e.g. hyperswarm). The registry is specified at DID creation so that nodes can determine which single source of truth to check for updates.

The *key concept of this design* is that MDIP DID creation is decentralized through through the CAS, and DID updates are decentralized through the registry specified in the DID creation. The MDIP DID is decentralized for its whole lifecycle, which is a hard requirement of DIDs.

## Overview
The diagram below illustrates the components that form a full Keychain MDIP Node. Additional details and quick start instructions are available in the repository. 

![keychain-node.png](https://github.com/KeychainMDIP/kc/blob/main/keychain-node.png)

### Gatekeeper: 
A Keychain MDIP node includes several interoperating microservices. If you follow the dependency arrows on the diagram above, you will end up at the central core service, the [Gatekeeper service](https://github.com/KeychainMDIP/kc/blob/main/services/gatekeeper/server/README.md) responsible for maintaining the integrity of the local DID database. 

### Mediators: 
The mediators are responsible for connecting the Gatekeeper to various networks such as [Hyperswarm](https://github.com/KeychainMDIP/kc/blob/main/services/mediators/hyperswarm/README.md). The TBTC (testnet Bitcoin) and TFTC (testnet Feathercoin) mediators are both instances of the [Satoshi mediator](https://github.com/KeychainMDIP/kc/blob/main/services/mediators/satoshi/README.md) since they are derived from Bitcoin core (they differ only in how they are configured). 

### Keymaster: 
[Keymaster](https://github.com/KeychainMDIP/kc/blob/main/packages/keymaster/README.md) is the MDIP client responsible for holding the private keys and signing DID operations (create, update, delete) sent to Gatekeeper. 

### Wallets: 
The [browser web wallet](https://github.com/KeychainMDIP/kc/blob/main/services/gatekeeper/client/README.md), [browser extension](https://github.com/KeychainMDIP/kc/blob/main/browser/chrome-extension/README.md), and [Keymaster service](https://github.com/KeychainMDIP/kc/blob/main/services/keymaster/server/README.md) all use the [Keymaster library](https://github.com/KeychainMDIP/kc/blob/main/packages/keymaster/README.md). The [server web wallet](https://github.com/KeychainMDIP/kc/blob/main/services/keymaster/client/README.md) is the same as the browser web wallet, except it is configured to talk to the Keymaster service instead of hosting its own wallet. It uses the same [KeymasterClient](https://github.com/KeychainMDIP/kc/blob/main/packages/keymaster/src/keymaster-sdk.ts) as the kc CLI. 

### DID Explorer: 
The [explorer](https://github.com/KeychainMDIP/kc/blob/main/services/explorer/README.md) and [search-server](https://github.com/KeychainMDIP/kc/blob/main/services/search-server/README.md) provide DID resolution, search and general interaction with DIDs and DID Documents.

### CLI: 
There are two CLI (command line interface) components: [kc](https://github.com/KeychainMDIP/kc/blob/main/scripts/keychain-cli.js) for talking to the Keymaster service, and [admin](https://github.com/KeychainMDIP/kc/blob/main/scripts/admin-cli.js) for talking to the Gatekeeper service. The admin script uses the same [GatekeeperClient](https://github.com/KeychainMDIP/kc/blob/main/packages/gatekeeper/README.md) as the Keymaster service and the mediators.

### Authentication Demo: 
A reference MDIP-enabled client application that demonstrates the challenge/response based authentication process. The demo also establishes privileged groups of users categorized as members, moderators, admins, or owner. [MDIP auth-demo repository](https://github.com/KeychainMDIP/auth-demo)

## Existing materials

* [Keychain Reference Implementation Repository](https://github.com/KeychainMDIP/kc)
* [MDIP DID Scheme](https://github.com/KeychainMDIP/kc/blob/main/doc/mdip/scheme.md)
* [MDIP Gatekeeper OpenAPI Specs](https://github.com/KeychainMDIP/kc/blob/main/doc/gatekeeper-api.json)
* [MDIP Keymaster OpenAPI Specs](https://github.com/KeychainMDIP/kc/blob/main/doc/keymaster-api.json)
* [MDIP Authentication Process and Demo](https://github.com/KeychainMDIP/auth-demo)
* [keychain.org Website](https://keychain.org)

### Online demo sites
The links below point to development systems to be used for demonstration and DIF evaluation purposes only. All the systems demonstrated in the links below can be found in the kc and auth-demo repositories.

* [Demo MDIP Explorer](https://explorer.mdip.yourself.dev)
* [Demo MDIP Web Wallet](https://wallet.mdip.yourself.dev)
* [Demo MDIP Authentication](https://auth.mdip.yourself.dev)

## Meeting the selection criteria

Document here how this DID method meets the [DID method selection criteria](../selection-criteria/).

| **Criteria** | **Details** |
|----------|----------|
| **Alignment with DID Core specification** | [Yes](https://github.com/KeychainMDIP/kc/blob/main/doc/mdip/scheme.md) |
| **Security and privacy features** | [Yes](https://github.com/KeychainMDIP/kc/tree/main/packages/cipher) |
| **Scalability and performance** | Yes. MDIP has a [modular architecture](https://github.com/KeychainMDIP/kc/blob/main/keychain-node.png) that enables scalable deployments. |
| **Ease of implementation and use** | Yes. See our [quick start](https://github.com/KeychainMDIP/kc/blob/main/README.md) instructions for easy Docker deployment. |
| **Community adoption and support** | Early Stages. This is one of our objectives in engaging with the DIF. |
| **Compliance with relevant regulations and best practices** | Yes. Another good reason for MDIP to register with the DIF. |
| **Global government-approved crypto** | No. MDIP is 100% P2P and agnostic to "crypto" networks. |
| **Privacy-preserving crypto** | Yes. Users generate their key-pairs on local devices. |
| **Digitally signed cryptographic log of changes to the DID Document** | Yes. Each Gatekeeper re-validates each DIDs by [applying DID Document changes one-by-one](https://github.com/KeychainMDIP/kc/blob/main/doc/mdip/did-lifecycle.png) in their proper order of registration. |
| **Multi-factor binding to DNS** | No. This could be a desirable feature to add to the protocol. |
| **Specification with multiple implementers** | No. We are looking forward to multiple implementations and SDKs in other languages. |
| **Scope/domain of the types of entities/subjects addressed/named by a particular method** | In its default configuration, MDIP publishes all DIDs to a public Hyperswarm channel. |
| **Estimate of the daily transaction volume of each scope/domain** | The MDIP network currently resolves ~15K DIDs. The network is mainly used by SelfID.com developers. |
| **DID Methods that do not serve the needs of a particular company or government** | Development of MDIP is financed by SelfID.com |
| **Governance: Clear frameworks for updates, dispute resolution, and decision-making** | An OSS-friendly governance model is being prepared but has not been launched yet. |
| **Usability: Simple implementation for developers** | A full MDIP node can be installed and launched within minutes using the [quick-start](https://github.com/KeychainMDIP/kc/blob/main/README.md) Docker deployment. |
| **Sustainability: Energy efficiency and eco-friendly infrastructure** | A full MDIP node can be operated on a simple RaspberryPi with 8Gb of RAM. |
| **Economic Feasibility: DIDs costs of use must be reasonable** | MDIP batches DID registration; node operators can configure batch frequency, etc.  |
| **Legal Recognition: Cross-border frameworks for DID acceptance** | N/A |
| **Revocation and Recovery: Decentralized mechanisms for key rotation and DID recovery** | The MDIP Keymaster wallet uses Bip-39 HD Keys. Each Agent DID in the wallet receives its own keypair that can be rotated. |
| **Emerging Markets: Offline-friendly, low-bandwidth** | Yes. MDIP can operate on low-power devices. Gatekeeper DID resolution functionality remains available to local users when disconnected from the global networks. |
| **Long-lived DIDs needed for long-lived VCs** | Yes. MDIP can evidence DIDs and VCs on a plurality of registries. |
| **Low and predictable marginal cost at scale (millions of accounts)** | TBD |
| **Ability to create and update identifiers rapidly (within seconds)** | Yes. MDIP operations are distributed to a public Hyperswarm channel within seconds, fast enough for user authentication scenarios. |
| **Support for key rotation** | Yes. MDIP provides key rotation functionality for each individual DID.  |
| **Reliable and predictable-latency operation, for updating and resolving** | The MDIP Gatekeeper operates its own indexed DB; supported DBs include: mysql, redis, and json file.  |
| **Resolution should not require additional state or context** | Each MDIP Gatekeeper operates independently and manages its current view of the network in a local database. |
| **DIDs are permanent and immutable account identifiers** | Yes. |
| **Consider support for various DID Traits: <https://identity.foundation/did-traits/>** | There are many desireable DID Traits that are not currently supported by MDIP. Likewize, MDIP implements new capabilities (like the Agent DID Manifest) that could be considered for standardization   |
| **Consider categories defined by DID Rubric: <https://www.w3.org/TR/did-rubric/>** | TBD |
| **Who WANTS to standardize the DID method and commits to doing the work?** | Keychain MDIP development is managed and financed by [Selfid.com](https://selfid.com), a brainchild and business lead and operated by [Craig Sellars](https://www.linkedin.com/in/craigcsellars/) |
| **Are there AT LEAST two WG members who support standardization of a DID method?** | We are looking to build interoperability and data formats standardization between MDIP and other available DID Methods |
| **Are there no trademark or IP issues?** | MDIP and the systems referenced in this document are published under an MIT License by SelfID.  |
| **What type of DID method is this?** | Decentralized |

## Is this DID method already involved in a standardization process? If so, where?

The DIF is our first attempt at interoperating and standardizing MDIP with other DID methods. 

## Supporting use cases

Keychain MDIP can be applied to a vast variety of use cases. MDIP includes numerous user-centric features designed to facilitate development of P2P identity solutions. Use-case centric functionality includes: 
* Full-featured W3C DID and VC platform
* Challenge/Response VC presentation process
* Encrypted documents assets identification and storage 
* Universal credential schema support
* P2P polling and voting functionality

See CLI references below for a more complete list of supported features.

### Keychain MDIP CLI 
```
Usage: keychain-cli [options] [command]

Keychain CLI tool

Options:
  -V, --version                            output the version number
  -h, --help                               display help for command

Commands:
  accept-credential [options] <did>        Save verifiable credential for current ID
  add-group-member <group> <member>        Add a member to a group
  add-group-vault-item <id> <file>         Add an item (file) to a group vault
  add-group-vault-member <id> <member>     Add a member to a group vault
  add-name <name> <did>                    Add a name for a DID
  backup-id                                Backup the current ID to its registry
  backup-wallet-did                        Backup wallet to encrypted DID and seed bank
  backup-wallet-file <file>                Backup wallet to file
  bind-credential <schema> <subject>       Create bound credential for a user
  check-wallet                             Validate DIDs in wallet
  clone-asset [options] <id>               Clone an asset
  create-asset [options]                   Create an empty asset
  create-asset-document [options] <file>   Create an asset from a document file
  create-asset-image [options] <file>      Create an asset from an image file
  create-asset-json [options] <file>       Create an asset from a JSON file
  create-challenge [options] [file]        Create a challenge (optionally from a file)
  create-challenge-cc [options] <did>      Create a challenge from a credential DID
  create-group [options] <groupName>       Create a new group
  create-group-vault [options]             Create a group vault
  create-id [options] <name>               Create a new decentralized ID
  create-poll [options] <file>             Create a poll
  create-poll-template                     Create a poll template
  create-response <challenge>              Create a response to a challenge
  create-schema [options] <file>           Create a schema from a file
  create-schema-template <schema>          Create a template from a schema
  create-wallet                            Create a new wallet (or show existing wallet)
  decrypt-did <did>                        Decrypt an encrypted message DID
  decrypt-json <did>                       Decrypt an encrypted JSON DID
  encrypt-file <file> <did>                Encrypt a file for a DID
  encrypt-message <message> <did>          Encrypt a message for a DID
  encrypt-wallet                           Encrypt wallet
  fix-wallet                               Remove invalid DIDs from the wallet
  get-asset <id>                           Get asset by name or DID
  get-credential <did>                     Get credential by DID
  get-group <did>                          Get group by DID
  get-group-vault-item <id> <item> <file>  Save an item from a group vault to a file
  get-name <name>                          Get DID assigned to name
  get-schema <did>                         Get schema by DID
  help [command]                           display help for command
  import-wallet <recovery-phrase>          Create new wallet from a recovery phrase
  issue-credential [options] <file>        Sign and encrypt a bound credential file
  list-assets                              List assets owned by current ID
  list-credentials                         List credentials by current ID
  list-group-vault-items <id>              List items in the group vault
  list-group-vault-members <id>            List members of a group vault
  list-groups                              List groups owned by current ID
  list-ids                                 List IDs and show current ID
  list-issued                              List issued credentials
  list-names                               List DID names (aliases)
  list-schemas                             List schemas owned by current ID
  perf-test [N]                            Performance test to create N credentials
  publish-credential <did>                 Publish the existence of a credential to the current user manifest
  publish-poll <poll>                      Publish results to poll, hiding ballots
  recover-id <did>                         Recovers the ID from the DID
  recover-wallet-did [did]                 Recover wallet from seed bank or encrypted DID
  remove-group-member <group> <member>     Remove a member from a group
  remove-group-vault-item <id> <item>      Remove an item from a group vault
  remove-group-vault-member <id> <member>  Remove a member from a group vault
  remove-id <name>                         Deletes named ID
  remove-name <name>                       Removes a name for a DID
  rename-id <oldName> <newName>            Renames the ID
  resolve-did <did> [confirm]              Return document associated with DID
  resolve-did-version <did> <version>      Return specified version of document associated with DID
  resolve-id                               Resolves the current ID
  restore-wallet-file <file>               Restore wallet from backup file
  reveal-credential <did>                  Reveal a credential to the current user manifest
  reveal-poll <poll>                       Publish results to poll, revealing ballots
  revoke-credential <did>                  Revokes a verifiable credential
  revoke-did <did>                         Permanently revoke a DID
  rotate-keys                              Generates new set of keys for current ID
  set-property <id> <key> [value]          Assign a key-value pair to an asset
  show-mnemonic                            Show recovery phrase for wallet
  show-wallet                              Show wallet
  sign-file <file>                         Sign a JSON file
  test-group <group> [member]              Determine if a member is in a group
  transfer-asset <id> <controller>         Transfer asset to a new controller
  unpublish-credential <did>               Remove a credential from the current user manifest
  unpublish-poll <poll>                    Remove results from poll
  update-asset-document <id> <file>        Update an asset from a document file
  update-asset-image <id> <file>           Update an asset from an image file
  update-asset-json <id> <file>            Update an asset from a JSON file
  update-poll <ballot>                     Add a ballot to the poll
  use-id <name>                            Set the current ID
  verify-file <file>                       Verify the signature in a JSON file
  verify-response <response>               Decrypt and validate a response to a challenge
  view-poll <poll>                         View poll details
  vote-poll <poll> <vote> [spoil]          Vote in a poll
```

### MDIP Admin CLI
```
Usage: admin-cli [options] [command]

Admin CLI tool

Options:
  -V, --version                                                output the version number
  -h, --help                                                   display help for command

Commands:
  cas-add-file <file>                                          Add a file to the CAS
  cas-add-json <file>                                          Add JSON file to the CAS
  cas-add-text <text>                                          Add text to the CAS
  cas-get-file <cid> <file>                                    Get a file from the CAS
  cas-get-json <cid>                                           Get JSON from the CAS
  cas-get-text <cid>                                           Get text from the CAS
  export-batch                                                 Export all events in a batch
  export-did <did>                                             Export DID to file
  export-dids                                                  Export all DIDs
  get-block <registry> [blockHeightOrHash]                     Get block info for registry
  get-dids [updatedAfter] [updatedBefore] [confirm] [resolve]  Fetch all DIDs
  get-status                                                   Report gatekeeper status
  hash-dids <file>                                             Compute hash of batch
  help [command]                                               display help for command
  import-batch-file <file> [registry]                          Import batch of events
  import-did <file>                                            Import DID from file
  import-dids <file>                                           Import DIDs from file
  list-registries                                              List supported registries
  perf-test [full]                                             DID resolution performance test
  process-events                                               Process events queue
  reset-db                                                     Reset the database to empty
  resolve-did <did> [confirm]                                  Return document associated with DID
  show-queue <registry>                                        Show queue for a registry
  verify-db                                                    Verify all the DIDs in the db
  verify-did <did>                                             Return verified document associated with DID
```

### Experimental Use Case: MDIP Authentication to online music album

This simple experimental use case is a customization of the generic auth-demo repository. 

[https://music.mdip.yourself.dev](https://music.mdip.yourself.dev)

### Use Case Proposal: Simple P2P Password Database

This use case has not been implemented. We hope to propose this project to the DIF Labs in a separate document.

Summary: We propose using MDIP's Group Vault functionality to create a collection of encrypted documents that can be shared with authorized Member users. Using the member-management functionality already provided by the MDIP auth-demo, a system owner/operator could delegate database Items and Members administration privileges to selected users. 
