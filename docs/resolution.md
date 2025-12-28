# OpenIndex Resolution Rules (v0.1)

**Status:** Draft  
**Scope:** Defines how OpenIndex identifiers resolve over HTTPS.

----------

## 1. Fundamental Rule

> **Every OpenIndex identifier MUST resolve via HTTPS.**

An OpenIndex identifier **is** a URL, not a pointer to one.

Example:

`https://openindex.id/earthpress/tartarian-world`

If it does not resolve, the system has failed.

----------

## 2. Resolution Is Read-Only

Resolution endpoints:

-   MUST NOT modify records

-   MUST NOT accept writes

-   MUST NOT require authentication


All writes occur **outside** resolution (e.g. via Git).

This guarantees:

-   safety

-   cacheability

-   trust


----------

## 3. Content Negotiation (Core Mechanism)

OpenIndex uses **HTTP content negotiation** to serve different representations of the _same_ identifier.

### 3.1 Default Behavior

If no `Accept` header is provided:

➡️ **Return `text/html`**

This ensures usability for:

-   browsers

-   humans

-   QR code scans


----------

### 3.2 Supported Media Types (v0.1)

Accept Header

Response

`text/html`

Human-readable landing page

`application/json`

Canonical OpenIndex record

`application/ld+json`

JSON-LD representation

Additional formats MAY be added later.

----------

## 4. Canonical JSON Response

When requested with:

`Accept: application/json`

The server MUST return:

-   the **exact OpenIndex record**

-   no derived fields

-   no injected metadata


Example:

`{  "openindex":  "https://openindex.id/earthpress/tartarian-world",  "type":  "work",  "title":  "Tartarian World",  "creators":  [  {  "name":  "Isaac Horton",  "role":  "author"  }  ],  "publisher":  {  "name":  "Earth Press",  "id":  "https://openindex.id/earthpress"  },  "date_published":  "2024",  "language":  "en",  "created_at":  "2025-01-01T00:00:00Z",  "record_version":  "v1"  }`

This response is:

-   cacheable

-   immutable

-   verifiable against Git


----------

## 5. JSON-LD Response (Semantic Web)

When requested with:

`Accept: application/ld+json`

The server MUST:

-   include an `@context`

-   preserve field meaning

-   map cleanly to schema.org where possible


Example (simplified):

`{  "@context":  {  "@vocab":  "https://openindex.id/context/",  "title":  "schema:name",  "creators":  "schema:creator",  "publisher":  "schema:publisher"  },  "@id":  "https://openindex.id/earthpress/tartarian-world",  "title":  "Tartarian World"  }`

This enables:

-   linked data

-   library integration

-   future knowledge graphs


----------

## 6. HTML Representation (Human Layer)

The HTML page MUST:

-   Display core metadata

-   Link to machine-readable formats

-   Be readable without JavaScript


### Minimum HTML requirements:

-   Title

-   Creators

-   Publisher

-   Publication date

-   Link to JSON

-   Link to JSON-LD


Example links:

`<link  rel="alternate"  type="application/json"  href="?format=json"> <link  rel="alternate"  type="application/ld+json"  href="?format=ldjson">`

----------

## 7. Versioned & Superseded Records

If a record has been superseded:

### Behavior:

-   Original URL MUST still resolve

-   HTML SHOULD indicate:

    > “This record has been superseded”

-   JSON MUST include relations field


Example:

`"relations":  {  "superseded_by":  "https://openindex.id/earthpress/tartarian-world-v2"  }`

Never break links.  
Never redirect silently.

----------

## 8. Namespace Resolution

Publisher namespaces MUST also resolve.

Example:

`https://openindex.id/earthpress`

Returns:

-   List of registered works (HTML)

-   Publisher metadata (JSON)


This enables:

-   discovery

-   transparency

-   verification


----------

## 9. HTTP Status Codes

Situation

Status

Record exists

`200 OK`

Record deprecated

`200 OK` + notice

Namespace exists

`200 OK`

Not found

`404 Not Found`

Gone permanently

`410 Gone` (rare)

Never use:

-   `302` for version changes

-   `401` / `403` for reads


----------

## 10. Caching Rules

OpenIndex responses SHOULD:

-   Include `ETag`

-   Include long `Cache-Control` headers

-   Be CDN-cacheable


Immutability = performance.

----------

## 11. Security & Integrity

Resolution endpoints MUST:

-   Be HTTPS-only

-   Use HSTS

-   Disable writes

-   Log access (for ops only)


Integrity is enforced by:

-   Git history

-   Public review

-   Optional cryptographic signatures


----------

## 12. Minimal Query Extensions (Optional)

Optional, non-normative support:

`?format=json ?format=html`

These MUST NOT replace content negotiation — only supplement it.

----------

## 13. Failure Philosophy

If OpenIndex infrastructure disappears:

-   Records still exist in Git

-   Anyone can re-host resolution

-   URLs can be re-pointed or mirrored


> **The identifier must outlive the server.**

----------

## 14. Resolution Rules in One Sentence

> **An OpenIndex identifier is a permanent HTTPS URL that resolves to immutable metadata via content negotiation, without authentication or mutation.**

That sentence is the system.
