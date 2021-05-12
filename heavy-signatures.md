Author: Andrew Dirksen (bddap)

# Abstract

This document introduces an abstraction atop cryptographic signatures, an extensible model for creating general purpose signatures with **stipulations** (or **assertions**).

# Intro

## Problem 1

Multiple implementaions of revokable signatures *as in TLS PKI*.
Signature expiration must be implemented for each data type *as in [jwt expiration claim](https://datatracker.ietf.org/doc/html/rfc7519#section-4.1.4) and TLS PKI*.

## Problem 2

Semantics of cryptographic signatures vary according to use-case. Special care must be taken to avoid payload-reinterpretation.

# Proposal

Multiple useful semantic additions to cryptographic signatures are essentially **stipulations** that restict the validity of some signature.

| Use Case    | Assertion - Signature is invalid unless ...               |
| -           | -                                                         |
| Revocation  | A proof of revocation for the signature is not published. |
| Expiration  | current_time <= `T`                                       |
| Valid After | current_time >= `T`                                       |

If all **stipulations** (**assertions**) of a Heavy Signature are true and the signature is cryptographically valid then the Heavy Signature is valid.
If any **stipulations** (**assertions**) of a Heavy Signature is false or the signature is cryptographically invalid then the Heavy Signature is invalid.

Each **stipulation** reduces the **scope** for which the signature is valid. Stipulations can never increase the scope.

## Encoding

A prefix is added to the body of the signature, that prefix is the encoded list of stipulations. The concatenated data is then signed.

```
sign(serialize(stipulations) + body, secret_key)
```

Each stipulation is encoded as it's ID (a hash), followed by it's associated data (a length-prefixed list of bytes).

When serialized, the list of stipulations is length-prefixed, where the length-prefix represents the number of stipulations in the list.

## Extensibility

Each type of stipulation is uniquely identified by a hash of a utf-8 encoded text stating the assertion.

Anyone can invent a new stipulation by writing it down, and taking the hash of the assertion, and creating a custom checker.

The serialization of the data of a stipulation is defined by its creator. When stipulations expect associated data, that the structure and serialization of that data must be explained in the assertion's text (the utf-8 encoded text which is hashed to obtain the stipulation type ID). As a result, changes to the structure or serialization of the stipulation's ascociated data will cause the stipulation type ID to change.

## Verification

TODO

Check signature.
Deserialize list of stipulations.
Attempt to check each assertion.
If any assertion is false, the Heavy Signature is invalid.
If any assertion is uncheckable, the valididy of the Heavy Signature is unknown.
If the verifier has not implmented a checker for an assertion, that assertion is uncheckable by that verifier.

## Further Questions

Can the intended interpretation of the payload also be expressed as **stipulations**? *The following table is not final, only for brainstorming*

| Use Case    | Assertion - Signature is invalid unless ...                              |
| -           | -                                                                        |
| Data Format | The body is decoded only as the media-type: `T`.                         |
| Data Format | The text language of the body is known to be English.                    |
| Semantics   | The body is interpreted as data that was possesed by the signer.         |
| Semantics   | The body is interpreted as attestation by the signer.                    |
| Semantics   | No further semantics apply.                                              |
| Semantics   | The signature indicates only intent to publish the contents of the body. |

If a verification fails due to an invalid cryptographic signature or due to an assertion being false, do we call the Heavy Signature "invalid" or "unverified"?
