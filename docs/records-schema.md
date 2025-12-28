# OpenIndex Record Schema (v0.1)

**Status:** Draft  
**Purpose:** Define the minimum, durable, append-only representation of a published work in OpenIndex.

----------

## 1. Design Goals (Non-Negotiable)

This schema must be:

1.  **Minimal** — fewer fields = fewer future regrets

2.  **Stable** — safe to store for decades

3.  **Append-only friendly** — supports corrections without mutation

4.  **Format-agnostic** — books today, digital artifacts tomorrow

5.  **Web-native** — URLs first, IDs second

6.  **Human-readable** — JSON a human can inspect


Anything that violates these goals is excluded from v0.1.

----------

## 2. High-Level Shape

Each record represents **one work**.

-   Not a format

-   Not an edition

-   Not a product SKU


Formats, editions, and variants are **references**, not identities.

----------

## 3. Canonical JSON Record

`{  "openindex":  "https://openindex.id/earthpress/tartarian-world",  "type":  "work",  "title":  "Tartarian World",  "creators":  [  {  "name":  "Isaac Horton",  "role":  "author"  }  ],  "publisher":  {  "name":  "Earth Press",  "id":  "https://openindex.id/earthpress"  },  "date_published":  "2024",  "language":  "en",  "subjects":  [  "history",  "alternative history",  "philosophy"  ],  "identifiers":  {  "isbn":  "978-1-23456-789-7"  },  "relations":  {},  "license":  "all-rights-reserved",  "created_at":  "2025-01-01T00:00:00Z",  "record_version":  "v1"  }`

This is intentionally _boring_. That’s a feature.

----------

## 4. Field-by-Field Explanation

### 4.1 `openindex` (Required)

`"openindex":  "https://openindex.id/earthpress/tartarian-world"`

-   The **canonical identifier**

-   Always a resolvable HTTPS URL

-   Unique by construction

-   Never reused


This replaces the need for a separate ID field.

----------

### 4.2 `type` (Required)

`"type":  "work"`

Allowed values (v0.1):

-   `work`


Future versions may add:

-   `dataset`

-   `media`

-   `software`

-   `collection`


But **v0.1 stays narrow**.

----------

### 4.3 `title` (Required)

`"title":  "Tartarian World"`

-   Human-facing primary label

-   Free text

-   No formatting rules


----------

### 4.4 `creators` (Required, ≥1)

`"creators":  [  {  "name":  "Isaac Horton",  "role":  "author"  }  ]`

-   Ordered list

-   Roles are strings (no enums yet)

-   ORCID integration later, not now


We avoid identity overreach in v0.1.

----------

### 4.5 `publisher` (Required)

`"publisher":  {  "name":  "Earth Press",  "id":  "https://openindex.id/earthpress"  }`

-   Publisher is a **namespace**, not an authority

-   `id` is optional but strongly encouraged

-   Enables linking without central control


----------

### 4.6 `date_published` (Required)

`"date_published":  "2024"`

Allowed formats:

-   `YYYY`

-   `YYYY-MM-DD`


Why not timestamps?

-   Publishing dates are often fuzzy

-   Precision should not be forced


----------

### 4.7 `language` (Optional, Recommended)

`"language":  "en"`

-   ISO 639-1

-   Simple, well understood


----------

### 4.8 `subjects` (Optional)

`"subjects":  [  "history",  "alternative history"  ]`

-   Free-text keywords

-   No taxonomy lock-in

-   Searchable, not authoritative


----------

### 4.9 `identifiers` (Optional)

`"identifiers":  {  "isbn":  "978-1-23456-789-7"  }`

-   Bridge to legacy systems

-   Never required

-   No validation enforced by OpenIndex


This is **interoperability, not dependency**.

----------

### 4.10 `relations` (Optional)

`"relations":  {  "supersedes":  "https://openindex.id/earthpress/tartarian-world/v1"  }`

Used for:

-   Corrections

-   Successors

-   Derived works


This is how we stay append-only.

----------

### 4.11 `license` (Required)

`"license":  "all-rights-reserved"`

-   Explicit is better than implicit

-   String-based (no SPDX enforcement yet)

-   Prevents accidental assumptions of openness


----------

### 4.12 `created_at` (Required)

`"created_at":  "2025-01-01T00:00:00Z"`

-   Record creation timestamp

-   Not publication date

-   Used for audit and ordering


----------

### 4.13 `record_version` (Required)

`"record_version":  "v1"`

-   Schema evolution marker

-   Not the same as work edition

-   Enables future migrations


----------

## 5. What We Explicitly Exclude (For Now)

This is as important as what we include.

❌ Pricing  
❌ DRM  
❌ Sales channels  
❌ File hashes  
❌ Authentication data  
❌ User accounts  
❌ Mutable updates  
❌ Ratings / reviews

Those belong in **other layers**, not the index.

----------

## 6. JSON Schema (Validation Skeleton)

This will live in `/schema/openindex-record.schema.json`.

High-level constraints:

-   Required fields enforced

-   URL formats validated

-   No additional properties by default


We keep it strict.

----------

## 7. Append-Only Correction Pattern (Example)

Original:

`"record_version":  "v1"`

Correction:

`{  "openindex":  "https://openindex.id/earthpress/tartarian-world-v2",  "relations":  {  "supersedes":  "https://openindex.id/earthpress/tartarian-world"  }  }`

Old record stays.  
New record points back.

This is **how trust survives**.

----------

## 8. Why This Schema Will Age Well

-   URLs don’t go out of style

-   JSON won’t disappear

-   Minimal assumptions

-   Easy to serialize into:

    -   JSON-LD

    -   RDF

    -   SQL

    -   Search indexes


And most importantly:

> **You can explain this schema to a librarian in five minutes.**

That’s the test.
