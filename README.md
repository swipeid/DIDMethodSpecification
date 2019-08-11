# SwipeId DID Method Specification

## Abstract

This document defines a SwiftId DID Method that conforms to the DID Spec. The method is implemented on top of Textile and ipfs, and is intended to be cheap, fast, scalable, and secure. It is suitable for both public and most private relationships between people, organizations, and things. As far as possible we adhere to the PeerId specification [Peer DID Method Specification](https://openssi.github.io/peer-did-method-spec/index.html)

## Status of This Document

A very first draft

Would it be possible to use multiformats and make this actually *be* a peer id?

## 1. Introduction

###  1.1 Overview

*This section is non-normative.*

We intend for this method to provide all the different types of DID

* **Anywise** Publically resolvable and published
* **Pairwise** Used only for a one-to-one peer relationship
* **N-wise** Used for N-peers

## 2. Core Characteristics

### 2.1 Method Name

The method name that identifies this DID method SHALL be: ``` swipe ```

A DID that uses this method MUST begin with the following prefix: ``` did:swipe: ```. Per the DID specification, this string MUST be in lowercase. The remainder of the DID, after the prefix, is the method specific identifier described below.

### 2.2 Target System(s)

This DID method applies to any identity management implementation that meets the following two requirements:

* Generation Algorithm — The DIDs are created using the algorithm described below, endowing them with properties vital to trust between peers that is not dependent on a central source of truth.
* Protocol — The metadata for DIDs (what would be stored in an on-chain DID doc in other methods) is communicated and maintained as described in the Protocols section.

### 2.3 Method Specific Identifier

The SwipeId DID scheme is defined by the following ABNF (see [RFC5234] for syntax):

**FIXME** 

EXAMPLE 1: ABNF for peer DIDs
peer-did = "did:swipe:" numalgo encalgo "-" numbasis
numalgo = "1"
encalgo = "1"
numbasis = 64*HEXDIGCI
HEXDIGCI = HEXDIG / "a" / "b" / "c" / "d" / "e" / "f"

### 2.4 Namestring Generation Method

**FIXME** Describe how *we* do this

The unique numeric basis underlying a Peer DID MUST be generated as follows:

Create a genesis version of JSON text of the DID doc for the DID. The genesis version MUST include enough keys and authorization that the genesis version of the doc can be signed (see Binding of Identity in the DID spec), to prevent man-in-the-middle attacks during initial DID exchange. It SHOULD also include enough state that subsequent evolutions to the doc are authorized; otherwise, the doc is a dead end. It MUST NOT include the DID itself (either the root id property or its value). This lets the doc be created without knowing the DID's value in advance. Suppressing the DID value creates a stored variant of peer DID doc data, as opposed to the resolved variant that would have an actual DID value in the root id property. (In either the stored or resolved variant of the doc, anywhere else that the DID value would appear, it should appear as a relative reference rather than an absolute value. For example, each controller property of a publicKey that is owned by this DID would say "controller": "#id".)
Calculate the SHA256 [RFC4634] hash of the bytes of the stored variant of the genesis version of the DID doc, and make this value the new DID's numeric basis.
By basing the numeric value of the DID on the genesis version of the DID doc, the DID can begin its lifecycle with any number of keys and endpoints, and when the doc is signed or auth-encrypted by one of the keys, the recipient can know it has not been modified since creation. This guarantees the initial integrity of the DID's chain of custody.

By hashing the stored variant, we avoid the circular problem of including the DID in the data that's being hashed. This means that a peer DID doc must be resolved by converting a stored variant of DID doc data into a resolved variant by inserting the value of the DID being resolved, during resolution.

### 2.5 Recognizing and handling Swipe DIDs

## 3. DID docs

### 3.1 Backing Storage

### 3.2 CRDTs

Since we are using Textile we have built-in, automatic support for CRDTs.

### 3.3 publicKey

#### 3.3.1 Adding a key
#### 3.3.2 Deleting a key
    
### 3.4 authentication
#### 3.4.1 Adding a key
#### 3.2.2 Deleting a key

### 3.5 authorization

This section seems to be a new one and deals with [SGL (Simple Grant Language)](https://evernym.github.io/sgl/)

**FIXME** We leave this for later.

## 4. Protocols

### 4.1 Roles and Agents

