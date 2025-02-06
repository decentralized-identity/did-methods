# DID method standardization proposal: did:iden3

This is a proposal to include `did:iden3` in the initial set of DID methods that will be standardized by the DID Methods WG.

## Description

<!--- Include a description of this DID method and rationale for standardizing it. --->
`did:iden3` is a blockchain-based DID Method that runs atop various blockchain networks including Ethereum, Polygon, Linea among others. 

The open source Iden3 protocol leveraged by the did method started its development back in 2018, led by Jordi Baylina, David Schwartz, and Antoni Martin, with the goal of creating decentralized and trusted digital identities that could be used in the scenario of a national referendum via an on-chain voting system. Iden3 is owned by the nonprofit “0KIMS Association” and is managed as a public good. Iden3 is not owned nor controlled by Privado ID, however Privado ID actively contributes to the open-source project along with a few other organizations and a broad open-source community. ZK-Snarks are emerging and promising technology, currently Iden3 libraries have been implemented by more than 9.000 projects some of them are mentioned in the [supporting use cases section](#supporting-use-cases).

A few components of the Iden3 protocol are worth highlighting: 
- [CIRCOM](https://docs.iden3.io/circom-snarkjs/) (world most used language and compiler to create zk-SNARK circuits), also recently referenced in this paper from zk researchers at various universities
- [JWZ (JWT with ZKProofs)](https://iden3-communication.io/docs-temp-public-tutorials/verify-with-zkp-application-level/jwz/) (method of signing and verifying authenticity of JWT payload messages using Zero-Knowledge Proofs)
- [SnarkJS](https://github.com/iden3/snarkjs) (the first general-purpose zk-SNARK prover capable of running on edge devices)
- [ZKQuery Language](https://docs.iden3.io/protocol/querylanguage/) (first general-purpose query language for zkp enabled credentials)

### Privacy Preserving Aspects of the Iden3 Signature Schemes: 
The Iden3 Signature Schemes (BJJ + zk-SNARKs and MTP + zk-SNARKs) enable organizations and users to have a higher degree of data minimization when exchanging credential data over distributed ledger networks. 

In the Iden3 scheme information on credential metadata like issuing date, expiration date, and revocation nonces are not shared in clear text but instead validated via a proof from a zk circuit. This prevents the relying party (RP) to uniquely identify the credential that is being used if the RP attempts to collude with the issuer of the credential. This is not possible in other schemes such as BBS+ where the credentials metadata is shared in clear text. Also in the Iden3 stack, if required by authorities for public interest needs, the user is also able to generate a selective disclosure of this metadata information.

The Iden3 protocol also minimizes data sharing by preventing the RP from inferring the structure and number of fields in the credential. In the case of data being revealed by selective disclosure, only the required attributes are shared without revealing any credential structure information. Contrast this with other schemes (such as BBS+) in which the signature that is sent during the presentation reveals the information on the number of fields to the verifier.

## Existing materials

<!--- Document here any existing draft specifications, implementations, deployments, test suites, etc. related to this DID method. --->
The `did:iden3` method specification [is available here](https://github.com/iden3/did-iden3).

A few major components and libraries related to the did method are listed here:
- Credential issuance methods supported: [BJJSignature2021](https://iden3-communication.io/w3c/proofs/bjj/) and [Iden3SparseMerkleTreeProof](https://iden3-communication.io/w3c/proofs/smt/).
- [iden3comm](https://iden3-communication.io/) didcomm based communication protocol
- 

In addition [Privado ID](https://docs.privado.id/) has implemented a few components utilizing the iden3 protocol which might be helpful for implementers such as the issuer node, verifier libraries, wallet SDKs, and developer tools (schema explorer, schema builder, and query builder).

## Meeting the selection criteria

<!--- Document here how this DID method meets the [DID method selection criteria](../selection-criteria/). --->

## Supporting use cases

<!---  Document here how this DID method supports concrete use cases.  --->
Due to its privacy-first design the `did:iden3` method lends itself well to a variety of use cases such as age verification,  Intellectual Property (IP) Protection, and B2B processes such as know your customer (KYC) for banking). Major web2 and web3 projects and organizations such as the Ethereum Foundation, Deutsche Bank, HBSC, Kaleido, Rarimo, and others are using the Iden3 stack. Organizations and Projects using the `did:iden3` method are listed below with evidence:
### Web3 market:
- Linea / Verax Airdrop - [link with evidence](https://github.com/0xPolygonID/verax-campaign-website/blob/8052073c0c411770e8344c67167ba81c75c78626/src/app/page.tsx#L23)
- Rarimo - [link with evidence](https://github.com/rarimo/rarime/blob/3de12ff67eb291efc823412b1c6abfa43961efd3/packages/zkp-iden3/src/helpers/identity-helpers.ts#L20)
- Blockchain Lab:UM - [link with evidence](https://github.com/blockchain-lab-um/masca/blob/cdaa99e9098f404ac0eb80ac806329a8275fb57c/packages/docs/docs/roadmap.md?plain=1#L20)
- Kaleido - [link with evidence](https://github.com/kaleido-io/kaleido-iden3-samples)
- Targecy.xyz - [link with evidence](https://github.com/targecy/core/blob/ac327e79981eafffb580e39bb70d3dc3755b569e/packages/sdk/src/utils/tracking.ts#L106)
- Tookey - [link with evidence](https://github.com/tookey-io/automation/blob/31fa5395a38020ec9ab782d836f14d62280ffcce/packages/pieces/polygon-id/src/lib/actions/waitForClaim.ts#L39)
- WakeUpLabs - [link with evidence](https://github.com/wakeuplabs-io/opid-contracts/blob/6ac9c60f7d11c55b4f803bf2b9819652a4b0e020/scripts/setPaymentValue.ts#L81)
- Uptick Network - [link with evidence](https://did-docs.uptick.network/docs/verifier/verification-library/zk-query-language/)
- Privado ID - [link with evidence](https://github.com/0xPolygonID/docs/blob/810c9c5f818dbc44f9f9cf7818b9d8c5905f5df8/docs/privado-identity-chain.md?plain=1#L28)

### Web2 market:
- Deutsche Bank - [link with evidence](https://corporates.db.com/files/documents/publications/db-polygo-digital-id-wp-42pp-web-secured.pdf?language_id=1)
- Hovi.id - [link with evidence](https://docs.hovi.id/intro/hovi-support-matrix)
- zk-firma-digital - [link with evidence](https://github.com/kuronosec/zk-firma-web/blob/bc4ae63a2be3dd7764a51c8be40500ecc2efcb66/src/ListVerifiableCredentials.tsx#L9)
- HSBC - [link with evidence 1](https://www.red-dot.org/de/project/hsbc-trusted-identity-reimagine-identities-for-a-collaborative-world-72122) and [link with evidence 2](https://www.privado.id/blog/why-hsbc-is-building-a-decentralized-identity-solution-with-polygon-id)

Here is a list of projects  which have implemented various aspects of the Iden3 stack:
- Ethereum Foundation - PSE Group - [Anon Aadhar](https://github.com/anon-aadhaar) - zero-knowledge protocol that allows Aadhaar ID owners to prove their identity in a privacy-preserving way, leverages the CIRCOM library
- Ethereum Foundation - PSE Group - [Minimal Anti-Collusion Infrastructure (MACI)](https://github.com/privacy-scaling-explorations/maci) - leverages the CIRCOM library
- Ethereum Foundation - [Semaphore Protocol](https://docs.semaphore.pse.dev/glossary#identity) - leverages the Baby Jubjub cryptography which is also utilized by `BJJSignature2021` credential issuance method
- [Masca](https://github.com/blockchain-lab-um/masca) - snap plugin for Metamask - support the `did:iden3` method
<!---  Pending.  --->
