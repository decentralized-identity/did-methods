# DID method standardization proposal:  did:hsm

This is a proposal to include `did:hsm` (HSM = Hardware Security Module) in the initial set of DID methods that will be standardized by the DID Methods WG.

## Description

Asymmetric cryptographic key pairs form the basis of digital identities. In order to do justice to the nature of an identity, it must be ensured that the digital identity is only controlled by a single natural or legal person. It is therefore essential to prevent any copying of the private key material used by the identity. Any information handled by computers, including servers, desktops, notebooks, smartphones, tablets etc. can be copied. It is therefore generally known that digital key material can only be securely stored on secure elements (chip cards, embedded secure elements, etc.) using hardware encryption. None of the DID methods that have been propagated up to now have mapped the hardware binding in the interaction between ID wallet and Hardware Security Module (HSM). For this reason, a specific method was developed and implemented with `did:hsm`. `did:hsm` is a DID method that enables the creation and anchoring of a DID in an HSM. The security concept of the DID method is based on did:keri and includes 

- Generation of the asymmetric key material exclusively in a secure element certified to ISO/IEC 15408-3 at EAL6 level. The import and export of private key material is prevented.
- A self-certifying identifier (SCID): The SCID, which is globally unique and embedded in the DID, is derived from the original DID protocol entry. It ensures the integrity of the DID history and reduces the risk of attackers creating a new object with the same identifier.
- Pre-rotation of the key pair and documentation in a signed data record: The mechanism for publishing the hashes of pre-rotation keys prevents the loss of control over a DID if an active private key is compromised. At the same time, the hash prevents the pre-rotated key from being calculated from the publication. The pre-rotated key pair remains in the secure element. The public key is only disclosed with a further key rotation.
- Key event log: The ability to resolve the entire key history of the DID using a verifiable chain of updates to the DID document from creation to deactivation. The chain of events is stored in a double-linked cryptographically signed chain of records and passed on to interaction partners, with each data record containing the hash of the next pre-rotated key (forward link) and the hash of the last entry in the chain (backward link).

`did:hsm` simplifies the generation and thus also the verification of a namespace-specific identifier. In addition, not only are the keys generated in an HSM, but also the DID that identifies this key set. By maintaining a key event log, the key status can be converted into a DID document. This DID document can be presented offline or stored under a URL. This means that `did:hsm` can also be supplemented by `did:web(s)`.

## Benefits

- With hardware encryption, all cryptographic keys are generated in a special security hardware (e.g. chip according to ISO 7816) and the cryptographic functions are calculated in hardware. If the security hardware does not provide an interface via which the keys can be exported or imported, the keys can never be stored useably in the working memory of the connected device. This prevents digital attackers from gaining access to the key material - the isolated memory areas ensure complete protection of cryptographic keys and data.
- Should an attacker guess the key material or succeed in recalculating the private key from the public key, pre-rotated key material stored in the HSM can be used to prevent misuse. This means that DIDs can be used over very long periods of time.
- The cryptographically verifiable key history enables direct interaction between two actors without the need to involve a third party. This protects the privacy of the actors and the interaction can also take place without an internet connection if necessary.
- Interoperability with other DID methods, e.g. `did:key`, `did:web`, `did:webvh`, `did:keri` etc., is possible. 
- The highest possible level of security forms a good basis for process automation and court-proof evidence.

## Drawbacks

- In contrast to `did:keri`, where the lack of hardware binding is compensated for on the software side by the concept of witnesses, `did:hsm` consistently supports hardware binding. This means that `did:hsm` always requires an HSM. In order to support large transaction volumes, such as those expected when used in organizations, it may be necessary to operate a number of HSMs in a cluster. 
- There are intentionally no backups of the keys. A defect in the HSM nominally terminates the use of the DID. It is therefore necessary to organize the inheritance of credentials via additional protocols and infrastructures.

## Existing materials

### Specifications

- Description in progress

### Implementations

- Applet for SSI-capable Hardware Security Modules 
- Applet-API library in Kotlin-Multi-Plattform, tested on Android, iOS and Debian Linux servers

### Deployments

- Documentation of the piloting by German municipal administration is in progress 

### Test suites

- HSM test kit with implemented `did:hsm` will be available on request

## Meeting the selection criteria

How `did:hsm` meets the DID method selection criteria:

|   **Criteria**   |   **Details**   |
| --- | --- |
|   **Alignment with DID Core specification**   |   Yes, fully compliant with DID specification   |
|   **Security and privacy features**   |   Yes, the DID Method has highest possible security and privacy features by supporting hardware security   |
|   **Scalability and performance**   |   Scalability is given by the number of secure elements. Organisations need to operate a number of secure elements in parallel. The number is determined by the number of parallel transactions to be supported. DID initialization requires approximately 2 seconds.    |
|   **Ease of implementation and use**   |   Implementation of Applet requires knowledge about smart card programming. Installation in organizational environment may require operation of an HSM cluster.  HSM are connectable to servers, PCs, mobiles and IoT devices either by being integrated (embedded), by being connected via NFC or USB, ISO7816 or Bluetooth.   |
|   **Community adoption and support**   |   Pilot customers in municipal administration environment. Supported by Trustnet community.   |
|   **Compliance with relevant regulations and best practices**   |   Yes. Participation in German SPRIN-D “Funke EUDI wallet prototypes” competition.   |
|   **Global government-approved crypto**   |   The DID method is cryptographically agnostic.  Current implementation uses the latest approved NIST and FIPS cryptography (ECDSA and EdDSA).   |
|   **Privacy-preserving crypto**   |   Privacy preservation is achieved by direct bi-lateral communication.   |
|   **Digitally signed cryptographic log of changes to the DID Document**   |   Yes. The Key Event Log (KEL) is the DID Document. The KEL is stored in the wallet.   |
|   **Multi-factor binding to DNS**   |   Not necessary.   |
|   **Specification with multiple implementers**   |   Not yet.   |
|   **Scope/domain of the types of entities/subjects addressed/named by a particular method**   |   It addresses areas of application in which legally compliant interaction is required and can be proven in court. The method can be used by individuals as well as organizations and IoT devices.   |
|   **Estimate of the daily transaction volume of each scope/domain**   |   Difficult to estimate as it is not a question of the DID method. The number of contracts concluded, documents issued and official notifications between natural persons and/or legal entities on a daily basis could serve as a guide.   |
|   **DID Methods that do not serve the needs of a particular company or government**   |   The DID method and publication/retrieval methods are independent of any particular entity and their specific needs.   |
|   **Governance: Clear frameworks for updates, dispute resolution, and decision-making**   |   tbd   |
|   **Usability: Simple implementation for developers**   |   Yes.   |
|   **Sustainability: Energy efficiency and eco-friendly infrastructure**   |   Yes, no public blockchain infrastructure involved.   |
|   **Economic Feasibility: DIDs costs of use must be reasonable**   |   Security has its prize. Compared to the costs that are usually spent on IT security and the damage caused annually by identity theft and the resulting misuse, the costs of operating a DID are very low. In large quantities, a single HSM costs less than EUR 1 and can be used for several years.   |
|   **Legal Recognition: Cross-border frameworks for DID acceptance**   |   Being piloted by German municipal administration. Exchange with Dutch partner municipality in planning.   |
|   **Revocation and Recovery: Decentralized mechanisms for key rotation and DID recovery**   |   Key pre-rotation is inherent to the DID method. This means that in the unlikely event of a key compromise (due to the use of HSM), DID can continue to be used with the pre-rotated key material.  In addition, the HSM protects the DID, as communication between both parties takes place with the direct involvement of the parties' HSMs. If there is no HSM on one side, this is immediately detected by the second HSM. If an attacker manages to calculate the private key of an actor from their public key, they would then have to import this key into an HSM. Since the HSM applet has no import or export interfaces for private keys, this is effectively prevented.   |
|   **Emerging Markets: Offline-friendly, low-bandwidth**   |   `did:hsm` is offline-friendly and requires only low bandwidth capacities on the communication channel. The intention for the use of `did:hsm` is a decentralized exchange between two actors. The actors can even communicate offline, e.g. via Wi-Fi Direct, Bluetooth or NFC. The direct data exchange between the two HSMs involved requires only a few bytes, which can be embedded in both the DIDComm and OID4VC protocols.   |
|   **Long-lived DIDs needed for long-lived VCs**   |   At its core, `did:hsm` supports the generation of Autonomic Identifiers (AIDs) as described in the Key Event Receipt Infrastructure (KERI) specification. In particular, the HSMs used support the rotation of the key material and the documentation of the process in an event document. This means that the owner of a `did:hsm` can use it over a long period of time and with different actors. This enables the creation of large ecosystems with many actors.  `did:hsm` can be linked using so-called representation credentials. This makes it possible to combine individual DIDs into organizations and to establish DIDs as heirs in the sense of a backup. This enables the longevity of the DID even beyond the end of life of an individual HSM, without ever having to create copies of keys.   |
|   **Low and predictable marginal cost at scale (millions of accounts)**   |   Yes, chip card scale (e.g. credit cards, SIMs)   |
|   **Ability to create and update identifiers rapidly (within seconds)**   |   Yes, DID can be created within less than 2 seconds.   |
|   **Support for key rotation**   |   Yes, key rotation is a core feature of `did:hsm`.   |
|   **Reliable and predictable-latency operation, for updating and resolving**   |   Yes.   |
|   **Resolution should not require additional state or context**   |   Yes.   |
|   **DIDs are permanent and immutable account identifiers**   |   Yes. The service life of a DID generated with `did:hsm` is linked to the service life of the HSM in which it was generated and is operated. The DID is therefore permanent until the end of the HSM's service life.   |
|   **Consider support for various DID Traits:** [**https://identity.foundation/did-traits/**](https://identity.foundation/did-traits/)   |   The majority of the DID Traits are **true** for `did:hsm`.  <br/>The following ones are **false**:  <br/>- Transactional Fees  <br/>- Multi-Signature Verification Method  <br/>- Human-readable  <br/>- Globally resolvable  <br/>- Centrally hosted  <br/>- Privacy Preserving Crypto – niZKPs  <br/>- RSA, any size  <br/><br/>Not intended but **possible**:  <br/>- Enumerable  <br/><br/>**Not evaluated** yet:  <br/>- GOST <br/>- SM  <br/><br/>Privacy Preserving Crypto <br/>- BBS+ is not yet supported by HSMs on the market. `did:hsm` however will support BBS+ as soon as it is available on HSMs.   |
|   **Consider categories defined by DID Rubric:** [**https://www.w3.org/TR/did-rubric/**](https://www.w3.org/TR/did-rubric/)   |   Not yet evaluated.   |
|   **Who WANTS to standardize the DID method and commits to doing the work?**   |   KAPRION Technologies GmbH, University of Applied Sciences Dresden, City Administration of Dresden (Capital of Saxony, Germany) are willing to continue its work on the base specification and implementations.   |
|   **Are there AT LEAST two WG members who support standardization of a DID method?**   |   KAPRION is DIF member and intends to join the WG. Other DIF members seemed to be very interested in `did:hsm`.   |
|   **Are there no trademark or IP issues?**   |   no   |
|   **What type of DID method is this?**   |   Decentralized. `did:hsm` is bound to hardware security modules (in the meaning of secure elements) and intended to be used in direct communication between two actors.   |

## Is this DID method already involved in a standardization process? If so, where?

No. But the implementation and deployment of `did:hsm` refers to the existing standardization of HSMs.

## Supporting use cases

Due to the highest possible security and privacy features `did:hsm` supports a lot of practical use cases by provision of

- DIDs for natural persons, 
- DIDs for organizations and their employees, 
- DIDs for system actors of organizations, 
- DIDs for (smart) objects

Example: In the state capital of Dresden, digital identities of public authorities, their employees and system actors are currently being created and implemented using hardware security modules based on `did:hsm`. The aim is to automate business and administrative processes. One of these processes involves the creation of digital identities for natural persons based on `did:hsm`, including the issuing of verifiable proof of identity from official registers.

Further application scenarios:

- DIDs for Trusted Issuers, Trusted Verifiers and Trust Registries
- DIDs, ID wallets and credentials of organizations and their employees for use in industrial data spaces (GaiaX, ManufacturingX etc.)
- DIDs for digital product passports, supply chain traceability and associated metadata stored as linked resources
- DIDs for AI instances and bots
