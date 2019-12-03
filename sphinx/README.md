# Sphinx-libp2p - A packet format for onion routing and mixnets
> A libp2p transport secure channel handshake built with the Noise Protocol Framework.

| Lifecycle Stage | Maturity      | Status | Latest Revision |
|-----------------|---------------|--------|-----------------|
| 1A              | Working Draft | Active | r0, 2019-11-25  |

Authors: [@Mikerah]

Interest Group: 

[@Mikerah]: https://github.com/Mikerah

See the [lifecycle document][lifecycle-spec] for context about maturity level
and spec status.

[lifecycle-spec]: https://github.com/libp2p/specs/blob/master/00-framework-01-spec-lifecycle.md

## Table of Contents

## Terminology
The key words "MUST", "SHOULD", "SHOULD NOT", "MAY", "RECOMMENDED",
"OPTIONAL", and "REQUIRED" in this document are to be interpreted as
described in RFC 2119. 

`ACN` - An anonymous communication network (ACN) is a network designed to provide anonymity to its users. 


## Notation
For descriptions of algorithms and data structures, we use a Go-like pseudocode. 

Let `k` be a security parameter. As recommended in [SPHINX09], `k` should be set to `128`. 

Let `r` be the maximum number of nodes that a Sphinx packet will traverse before being sent to its destination. As recommended in [SPHINX09], `r` should be set to `5`.

Let `G` be a prime-order cyclic group that satisfies the Decisional Diffie-Hellman (DDH) assumption. 

Let `q` denote the prime order of `G`.

Let `G*` denote the set of non-identity elements in `G`. In other words, all the elements of `G` that are not the identity element. We denote the identity element as `1`.

Let `g` be the generator of `G`. In other words, the order of `g` is `q`.

Let `H_i(x_1, x_2,..., x_n)` denote a hash function where `i` is some identifier, `x_1, x_2,...,x_n` are inputs from `G* x G* x ... G*`, where `x` is the cartesian product applied `n` times and `H_i(x)` is a bit-string.

Let `m(x_1, x_2)` denote a message authentication code (MAC), where `x_1` is a bitstring of size `k`, `x_2` is a bitstring of arbitrary size and `m(x_1, x_2)` is a bitstring of size `k`. 

Let `p(x)` denote a pseudo-random generator (PRG), where `x` is a bistring of size `k` and `p(x)` is of size `(2r+3)k`.

## Overview
The [Sphinx packet format][SPHINX09] is a provably secure mix format for mix networks and onion routing networks. 

This documents specifies sphinx-libp2p, a modification of the sphinx packet format for use with libp2p. As such, it is not a protocol itself, but a building block for building libp2p stacks for ACNs.

## Motivation
Currently, libp2p peers send both plaintext messages and encrypted messages over a libp2p network. However, this isn't sufficient for building secure, anonymous communication protocols on top of libp2p. Many modern designs for ACNs rely on the sphinx packet format. In order to enable the implementation of these proposals on top of libp2p, there needs to be a specification that all libp2p implementations should follow.

## Rationale
TODO

## Goals
TODO

## Sphinx Cryptographic Packet Format Specification

### Threat Model
This is the threat model that was presented in (link to OG paper) and (link to Kate and Goldberg paper). 

__Author's Note__: It is, at the moment of this writing, unclear what Libp2p's threat model is. As such, when the threat model for libp2p has been established, this section should be updated to take that into account.

TODO

### Sphinx Packet Parameters
This section provides guidelines for parameterizing the constants and functions provided in [Notation](#notation).


### Helper Types
These are types are for clarification purposes. Implementers MAY implement these in their language of choice.

```
type struct RoutingInformation {

}
```

### Sphinx Packet Structure
A Sphinx packet consists of two components: `SphinxHeader` and `SphinxPayload`. We define the following data structure as follows:

```
type struct SphinxPacket {
    header SphinxHeader
    payload SphinxPayload
}
```

#### Header 
A `SphinxHeader` is a data structure defined as follows:
```
type struct SphinxHeader {
    groupElement []byte
    routingInformation []RoutingInformation
    MAC           [k]byte
}
```

#### Payload
A `SphinxPayload` is a data structure defined as follows:
```
type struct SphinxPayload {
    payload []byte
}
```

### Sphinx Packet Creation

## Libp2p Considerations

## Security Considerations
TODO

## Anonymity Considerations
TODO

## References
[SPHINX09]: https://www.freehaven.net/anonbib/cache/DBLP:conf/sp/DanezisG09.pdf
[SPHINXONION09]: http://cacr.uwaterloo.ca/techreports/2009/cacr2009-33.pdf
