**This document is normative.**

# OpenIndex Record Immutability & Versioning Specification (v0.1)

**Status:** Draft  
**Scope:** All OpenIndex records  
**Applies to:** `openindex.id`, `openindex.cc`

----------

## 1. Core Principle

> **An OpenIndex record, once published, MUST NOT be altered or deleted.**

This guarantees:

-   Citation stability

-   Historical traceability

-   Resistance to tampering

-   Long-term trust


OpenIndex is **append-only by design**.

----------

## 2. What Is a Record?

A record is any JSON document that resolves from an OpenIndex URI, including but not limited to:

-   Works

-   Editions

-   Digital objects

-   Metadata-only records

-   Namespace records


Example:

`https://openindex.id/earthpress/field-notes`

----------

## 3. Record Identity Is Permanent

A record is uniquely identified by its **canonical URI**:

`https://openindex.id/{namespace}/{slug}`

Once created:

-   The URI MUST always resolve

-   The record MUST remain available

-   The record MUST continue to return its original content


----------

## 4. Immutability Rules

Once a record is accepted into the registry:

❌ NOT allowed:

-   Editing existing fields

-   Removing fields

-   Replacing content

-   Deleting records


✅ Allowed:

-   Creating a new version

-   Creating a related record

-   Appending metadata via version linkage


----------

## 5. Versioning Model (Linear, Explicit)

OpenIndex uses **explicit versioned records**, not in-place updates.

### 5.1 Versioned URI Structure

Versions are expressed as **distinct records**:

`https://openindex.id/earthpress/field-notes@v1 https://openindex.id/earthpress/field-notes@v2`

Rules:

-   `@v1` is implicit if omitted

-   Versions MUST increment monotonically

-   Versions MUST be integers (`v1`, `v2`, `v3`…)


----------

## 6. Canonical (Unversioned) Resolution

The unversioned URI:

`https://openindex.id/earthpress/field-notes`

MUST resolve to:

-   The **latest stable version**, or

-   A resolver response that declares the current version


Example response fragment:

`{  "canonical":  "https://openindex.id/earthpress/field-notes",  "current_version":  "v3",  "resolved":  "https://openindex.id/earthpress/field-notes@v3"  }`

----------

## 7. Required Version Metadata

Every versioned record MUST include:

`{  "openindex":  "https://openindex.id/earthpress/field-notes@v2",  "type":  "work",  "version":  "v2",  "previous_version":  "https://openindex.id/earthpress/field-notes@v1",  "created_at":  "2026-01-04T19:22:00Z",  "change_summary":  "Corrected publication date and added ISBN reference",  "record_version":  "v1"  }`

----------

## 8. What Constitutes a New Version?

A new version MUST be created if:

-   Metadata changes

-   Attribution changes

-   Links change

-   Descriptions change

-   Any semantic meaning changes


A new version MAY be created for:

-   Minor corrections

-   Formatting fixes

-   Metadata enrichment


----------

## 9. Forking & Derivative Records

OpenIndex allows **forking** without overwriting history.

A forked record MUST:

-   Reference the source record

-   Declare its relationship explicitly


Example:

`{  "derived_from":  "https://openindex.id/earthpress/field-notes@v1",  "relationship":  "annotation"  }`

----------

## 10. Deprecation (Not Deletion)

Records MAY be deprecated but MUST continue to resolve.

Deprecation is expressed via metadata:

`{  "status":  "deprecated",  "superseded_by":  "https://openindex.id/earthpress/field-notes@v3"  }`

----------

## 11. Cryptographic Integrity (Recommended)

Each record MAY include a checksum:

`{  "checksum":  {  "algorithm":  "sha256",  "value":  "…"  }  }`

This allows:

-   Independent verification

-   Mirroring

-   Third-party resolvers


(Git already provides this implicitly, which is a feature, not a dependency.)

----------

## 12. Git as the Source of Truth

The canonical registry repository:

-   Is append-only

-   Preserves commit history

-   Provides tamper evidence

-   Enables distributed mirrors


Git history MUST NOT be rewritten.

----------

## 13. Resolver Behavior Requirements

Resolvers MUST:

-   Resolve versioned URIs exactly

-   Never rewrite historical content

-   Clearly indicate version resolution

-   Allow clients to request specific versions


----------

## 14. Design Goals

This model prioritizes:

-   Longevity over convenience

-   Trust over mutability

-   Transparency over control

-   Forkability over central authority


----------

## 15. Versioning of This Spec

-   v0.1 — Initial definition

-   Future versions MUST remain backward compatible


----------

## Why This Is Strong

This gives OpenIndex something ISBN _doesn’t have_:

-   Native versioning

-   Cryptographic verifiability

-   Git-native governance

-   Immutable scholarly references

-   Forkable bibliographic history


It also maps cleanly onto:

-   academic citation norms

-   software versioning

-   web-native resolution

-   decentralized mirrors
