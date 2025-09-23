# Findings: did:webvh DIF-recommended DID methods

This "findings" document summarizes the process that led to the status
of `did:webvh` as a DIF-recommended DID method.

This process is documented here: https://github.com/decentralized-identity/did-methods/tree/main/dif-recommended

**Date of this document:** 16th September 2025

## Overview

**DID method:** `did:webvh`

**DID method specification:** [Current Stable v1.0](https://identity.foundation/didwebvh/v1.0/)

**Open issues (3):** https://github.com/decentralized-identity/didwebvh/issues

**PRs (1):** https://github.com/decentralized-identity/didwebvh/pul

## W3C Registry

**Yes**, see here: https://www.w3.org/TR/did-extensions-methods/

## Method Proposal

**Yes**, see here: https://github.com/decentralized-identity/did-methods/blob/main/method-proposals/PROPOSAL-did-webvh.md

## W3C Tests

**Yes**, see here: https://w3c.github.io/did-test-suite/#M53

Number of tested implementations of `did:webvh`: **4**

### Implementation: https://github.com/decentralized-identity/didwebvh-py

**Results:** https://github.com/w3c/did-test-suite/blob/main/packages/did-core-test-server/suites/implementations/did-webvh-dif-py.json

37 passing

### Implementation: https://github.com/decentralized-identity/didwebvh-ts

**Results:** https://github.com/w3c/did-test-suite/blob/main/packages/did-core-test-server/suites/implementations/did-webvh-dif-ts.json

37 passing

### Implementation: Universal Resolver

**Results:** https://github.com/w3c/did-test-suite/blob/main/packages/did-core-test-server/suites/implementations/universal-resolver-did-webvh.json

19 passing

### Implementation: DIF

**Results:** https://github.com/w3c/did-test-suite/blob/main/packages/did-core-test-server/suites/implementations/dereferencer-dif-webvh.json

14 passing, 1 failing

## Universal Resolver

**Yes**, see here:
https://github.com/decentralized-identity/universal-resolver/blob/9029d262436b497f7fc85a7f70c7edd9e7815fb0/docker-compose.yml#L373

**Docker image:**
https://ghcr.io/decentralized-identity/uni-resolver-driver-did-webvh:v2.4.0-1400145

**Example query:**
https://dev.uniresolver.io/#did:webvh:QmVJ5nUYb9iugnUz4yDfbe8UFbhmnsvS2EAzSpSfPScRAn:opsecid.github.io

## DID Traits

**Yes**, see here:
https://identity.foundation/did-traits/#comparison-of-did-methods

## Multiple Implementations

**Yes**, see here:
https://didwebvh.info/latest/implementations/

## Deployments

**Yes**, see here:
https://didwebvh.info/latest/implementations/deployments/

## Standardization Target

**Yes**, W3C

## Presentations and Deep Dives

### Initial Presentation

**Date:** May 28, 2025 08:58 AM

**Recording:** [link](https://us02web.zoom.us/rec/share/AJ5AINNqN0mc-gDtSsKPjgyknBjXViRsVpXklZFcC4vObcrRxAoXQ3c9kCRkmEKA.ZAK46kp3nq77dWIm)

Main topics and questions by audience:
- (Victor Dods) Static or dynamic Linked VPs, validity period
- (bumblefudge) Use of witnesses during resolution
- (Victor Dods) Verification of incremental updates
- (Alex Tweedale) Anchoring verifiable history to a blockchain
- (Otto Mora) Portability between domain names

All questions answered and issues addressed? **Yes**

### Deep Dive 1

**Date:** Jul 16, 2025 08:59 AM

**Recording:** [link](https://us02web.zoom.us/rec/share/6GhsVQ6VCIQiM5YyqkeAr4zg9RxcfxriKSi3tqQp5v0nad7Gdp52uXe5Pm3B26nz.SdHHNRMZJJcWmzZn)

Main topics and questions by audience:
- (Eric Scouten) Available implementations
- (Eric Scouten) Performance, benchmarks
- (Markus Sabadello) Comparison to Cryptographic Event Logs in W3C CCG
- (Otto Mora) Optionality of witness infrastructure
- (bumblefudge) Integer values in metadata structures

All questions answered and issues addressed? **Yes**

### Deep Dive 2

**Date:** Jul 30, 2025 08:58 AM

**Recording:** [link](https://us02web.zoom.us/rec/share/lfV6HHLI9JrbIihvji3aChwKMzpKNuAYstXwHjcAAXbBI6pt1e1GTGheEY-vR0G6.xRejirZnUaAxQB3_)

Main topics and questions by audience:
- (Eric Scouten) Available implementations
- (Ankur Banerjee) Returning DID document and/or metadata for deactivated DID
- (Ankur Banerjee) List of trustworthy watchers, duplicitous watchers
- (Victor Dods) Potential role of Verifiable Data Gateway
- (Sam Curren) Binding between DID and domain name
- (Sam Curren) Timeline of did:webvh

All questions answered and issues addressed? **Yes**

## Pull Request for DIF-recommended status

https://github.com/decentralized-identity/did-methods/pull/67 **(13 comments)**

Main questions and topics:
- (vdods) Pre-rotation keys
- (vdods) Authorized DID updates

All questions answered and issues addressed? **Yes**
