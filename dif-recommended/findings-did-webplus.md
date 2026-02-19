# Findings: did:webplus DIF-recommended DID method

This "findings" document summarizes the process that led to the status
of `did:webplus` as a DIF-recommended DID method.

This process is documented here: https://github.com/decentralized-identity/did-methods/tree/main/dif-recommended

**Date of this document:** 2nd February 2026

## Overview

**DID method:** `did:webplus`

**DID method specification:** [Current Stable v1.0](https://ledgerdomain.github.io/did-webplus-spec/)

**Open issues (0):** https://github.com/LedgerDomain/did-webplus-spec/issues

**PRs (0):** https://github.com/LedgerDomain/did-webplus-spec/pulls

## W3C Registry

**Yes**, see here: https://www.w3.org/TR/did-extensions-methods/ ( https://github.com/w3c/did-extensions/blob/main/methods/webplus.json )

## Method Proposal

**Yes**, see here: https://github.com/decentralized-identity/did-methods/blob/main/method-proposals/PROPOSAL-did-webplus.md

## W3C Tests

**Yes**, see here: https://w3c.github.io/did-test-suite/#M53

Number of tested implementations of `did:webplus`: **1**

### Implementation: https://github.com/LedgerDomain/did-webplus (Rust)

**Results:** https://github.com/w3c/did-test-suite/blob/main/packages/did-core-test-server/suites/implementations/did-webplus-ledgerdomain.json

41 passing (v1.1 version)

### Implementation: Universal Resolver

**Results:** n/a

n/a

## Universal Resolver

**NO**; Recommended status contingent on finishing this pending item.

**Docker image:**
n/a

**Example query:**
n/a

## DID Traits

**Yes**, see here:
https://identity.foundation/did-traits/#comparison-of-did-methods

## Multiple Implementations

**No**: the Rust crate is the only end-to-end implementation, although there is some language diversity of verification-side applications.

## Deployments

**Yes**, in the [OC-i](https://www.oc-i.org/dscsa-authorized-trading-partners) multi-DID production messaging context. see here for cross-method testing artefacts:
https://github.com/LedgerDomain/oci-interop

## Standardization Target

**No**, further standardization not currently sought

## Presentations and Deep Dives

### Initial Presentation

**Date:** Sept 24, 2025 08:58 AM

**Recording:** [link](https://us02web.zoom.us/rec/share/1jJ7EIXc72ARQTQLXK6PXV2-cq0oN7gWlDBXwzD-IkEXpRfnxyxpX2IBZ1rRU23U.saBYCUDcfR2tbKps)

Main topics and questions by audience:
- (in chat) - Overlap with other IPFS-/multiformats-based methods
- (jonathan) - "thin"/trustful resolver for universal resolver (resolution via VDG) versus traditional "full node" resolution drivers
- (otto) - parallel development with did:webvh? 
- (otto/jonathan) - multi-signature support
- (drummond) - Relationship between did:webplus SCIDs and [Drummond Reed's and FPP's] concept of SCID
- (otto) - production-scale VDG/CDN-like resolution plans?

All questions answered and issues addressed? **Yes**

### Deep Dive 1

**Date:** Oct 29, 2025 08:59 AM

**Recording:** [link](https://us02web.zoom.us/rec/share/aF-Oyy6vsSHTQVotgcMMpdxAMo_I0e3PyvFHl5Wrqy3PbLMsl283eXGb2OBGV0Dr.-f9s4l5thUU_4JpS)

Main topics and questions by audience:
- (otto, makki) - exact semantics/trust model of VDG/caching infra
- (makki) - how does a did:webplus tlog compare to the C2PA Manifest Store for provenance of an asset? (long sidebar) 

All questions answered and issues addressed? **Yes**

### Deep Dive 2

**Date:** Dec 3, 2025 08:58 AM

**Recording:** [link](https://us02web.zoom.us/rec/share/6yRpfB0ZND2JdmmYr6oQz8kYfFturosnG5ohQKxLNS4UXy80VyLuerzeNppo2XQ-.E74fBnNUdLYo1HFM)

Main topics and questions by audience:
- (bumblefudge) - Update rule DSL is mandatory behavior for all implementations? (Victor) technically, each VDR/hosting server only needs to be able to parse its own DIDs' updates
- (bumblefudge) - range-based GET/jsonlines for efficient caching
- (Eike) - the only magic bytes and prefixes are ALL from the multiformats conventions, right? (victor) yes, 100%
- (Makki) - Why just Blake3, not SHA256? Applicability to NIST-bound developers and implementation contexts would be better served...
    + (victor) followed up on github and in a later meeting in January

All questions answered and issues addressed? **Yes**

## Pull Request for DIF-recommended status

https://github.com/decentralized-identity/did-methods/pull/77 **(14 comments)**

Main questions and topics:
- (Makki & vdods) Following up on [support for additional hash functions](https://github.com/decentralized-identity/did-methods/pull/77#issuecomment-3837715821)

All questions answered and issues addressed? **Yes**
