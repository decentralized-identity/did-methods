# Findings: did:hedera DIF-recommended DID method

This "findings" document summarizes the process that led to the status
of `did:hedera` as a DIF-recommended DID method.

This process is documented here: [https://github.com/decentralized-identity/did-methods/tree/main/dif-recommended](https://github.com/decentralized-identity/did-methods/tree/main/dif-recommended)

**Date of this document:** June 24th, 2026

## Overview

**DID method:** `did:hedera`

**DID method specification:** [v2.0](https://github.com/hashgraph/did-method)


## W3C Registry

**Yes**, see here: [https://www.w3.org/TR/did-extensions-methods/](https://www.w3.org/TR/did-extensions-methods/)

## Method Proposal

**Yes**, https://github.com/decentralized-identity/did-methods/blob/main/method-proposals/PROPOSAL-did-hedera.md

## W3C Tests

**TBD**

Number of tested implementations : multiple. See hashgraph: https://hedera.com/use-cases/decentralized-identity/

### Implementation: 
https://github.com/hiero-ledger/hiero-did-sdk-js

## Universal Resolver

**Yes**, see here:
[https://dev.uniresolver.io/#did:hedera:testnet:23g2MabDNq3KyB7oeH9yYZsJTRVeQ24DqX8o6scB98e3_0.0.5217215]

**Example query:**
[https://dev.uniresolver.io/#did:example:000](https://dev.uniresolver.io/#did:example:000)

## DID Traits

**Yes**, see here:
[https://identity.foundation/did-traits/#comparison-of-did-methods](https://identity.foundation/did-traits/#comparison-of-did-methods)

## Multiple Implementations

**Yes**, see here:
[https://hedera.com/use-cases/decentralized-identity/]

## Deployments

**Yes**, see here:
https://hedera.com/

## Standardization Target

**Yes**, W3C

## Presentations and Deep Dives

### Initial Presentation

**Date:** June 24th, DID:Methods workgroup

[Recording](https://link-to-recording/)

Main topics and questions by audience:

- Juan asked about Hedera transaction addressing and packaging. Keith answered with an example describing the message structures and network models (private, public, 0.0 public network)
- Otto asked about the Hedera payment model for transactions. Keith answered and described the stable pricing model of Hedera based on charging per topic, and topics being able to themselves contain collections of messages.
- Keith presented the method's capabilities and ran through a demo where a DID was created with a service endpoint added.
- Keith demonstrated new DIDs produced being available in the DIF universal resolver
- Christian asked about public SDKs for developers: github.com/hiero-ledger/hiero-did-sdk-js
- Juan asked about multi-signature functionality. Keith clarified that multi-sig applies to topics, not messages themselves.
- Juan asked about the role of blockchain in signing of transactions. Keith clarified that the blockchain account is not related to the DID document signatures. The DID documents can be stored anywhere, including non-blockchain layers like IPFS.
- Otto asked about relations between DIDs and Verifiable Credentials. Keith clarified that the VCs are not part of the DID method, which focuses on CRUD operations.
- Discussion about registration, trust, and validation of messages.
- Deep Dive 1 could include a discussion about the different trust layers involved in a did:hedera document.

All questions answered and issues addressed? ** Juan to reach out to Keith to discuss blockchain role **

**Date:** Jan 01, 2025 00:00 AM

[Recording](https://link-to-recording/)

Main topics and questions by audience:

- (Participant 1) Topic 1
- (Participant 2) Topic 2

All questions answered and issues addressed? **Yes**

### Deep Dive 1

**Date:** TBD

[Recording](https://link-to-recording/)

Main topics and questions by audience:

- (Participant 1) Topic 1
- (Participant 2) Topic 2

All questions answered and issues addressed? **Yes**

### Deep Dive 2

**Date:** TBD

[Recording](https://link-to-recording/)

Main topics and questions by audience:

- (Participant 1) Topic 1
- (Participant 2) Topic 2

All questions answered and issues addressed? **Yes**

## Pull Request for DIF-recommended status



Main questions and topics:

- (Participant 1) Topic 1
- (Participant 2) Topic 2

All questions answered and issues addressed? **Yes**
