# Findings: did:hedera DIF-recommended DID method

This "findings" document summarizes the process that led to the status
of `did:hedera` as a DIF-recommended DID method.

This process is documented here: [https://github.com/decentralized-identity/did-methods/tree/main/dif-recommended](https://github.com/decentralized-identity/did-methods/tree/main/dif-recommended)

**Date of this document:** June 24th, 2026

## Overview

**DID method:** `did:hedera`

**DID method specification:** [v1.0](https://link-to-specification)

**Open issues (3):** [https://github.com/org/didexamplemethod/issues](https://github.com/org/didexamplemethod/issues)

**PRs (1):** [https://github.com/org/didexamplemethod/pulls](https://github.com/org/didexamplemethod/pulls)

## W3C Registry

**Yes**, see here: [https://www.w3.org/TR/did-extensions-methods/](https://www.w3.org/TR/did-extensions-methods/)

## Method Proposal

**Yes**, see here: [https://github.com/decentralized-identity/did-methods/blob/main/method-proposals/PROPOSAL-did-example.md](https://github.com/decentralized-identity/did-methods/blob/main/method-proposals/PROPOSAL-did-example.md)

## W3C Tests

**Yes**, see here: [https://w3c.github.io/did-test-suite/#M00](https://w3c.github.io/did-test-suite/#M00)

Number of tested implementations of `did:example`: **1**

### Implementation: [https://github.com/decentralized-identity/didexample-py](https://github.com/decentralized-identity/didexample-py)

**Results:** [https://github.com/w3c/did-test-suite/blob/main/packages/did-core-test-server/suites/implementations/did-example-dif-py.json](https://github.com/w3c/did-test-suite/blob/main/packages/did-core-test-server/suites/implementations/did-example-dif-py.json)

37 passing

## Universal Resolver

**Yes**, see here:
[https://github.com/decentralized-identity/universal-resolver/blob/0000000000000000000000000000000000000000/docker-compose.yml#L000](https://github.com/decentralized-identity/universal-resolver/blob/0000000000000000000000000000000000000000/docker-compose.yml#L000)

**Docker image:**
[https://ghcr.io/decentralized-identity/uni-resolver-driver-did-example:v1.0.0](https://ghcr.io/decentralized-identity/uni-resolver-driver-did-example:v1.0.0)

**Example query:**
[https://dev.uniresolver.io/#did:example:000](https://dev.uniresolver.io/#did:example:000)

## DID Traits

**Yes**, see here:
[https://identity.foundation/did-traits/#comparison-of-did-methods](https://identity.foundation/did-traits/#comparison-of-did-methods)

## Multiple Implementations

**Yes**, see here:
[https://link-to-information-about-implementations/](https://link-to-information-about-implementations/)

## Deployments

**Yes**, see here:
[https://link-to-information-about-deployments/](https://link-to-information-about-deployments/)

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

All questions answered and issues addressed? **Yes**

**Date:** Jan 01, 2025 00:00 AM

[Recording](https://link-to-recording/)

Main topics and questions by audience:

- (Participant 1) Topic 1
- (Participant 2) Topic 2

All questions answered and issues addressed? **Yes**

### Deep Dive 1

**Date:** Jan 01, 2025 00:00 AM

[Recording](https://link-to-recording/)

Main topics and questions by audience:

- (Participant 1) Topic 1
- (Participant 2) Topic 2

All questions answered and issues addressed? **Yes**

### Deep Dive 2

**Date:** Jan 01, 2025 00:00 AM

[Recording](https://link-to-recording/)

Main topics and questions by audience:

- (Participant 1) Topic 1
- (Participant 2) Topic 2

All questions answered and issues addressed? **Yes**

## Pull Request for DIF-recommended status

[https://github.com/decentralized-identity/did-methods/pull/00](https://github.com/decentralized-identity/did-methods/pull/00) **(3 comments)**

Main questions and topics:

- (Participant 1) Topic 1
- (Participant 2) Topic 2

All questions answered and issues addressed? **Yes**
