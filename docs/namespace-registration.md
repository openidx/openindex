# OpenIndex Namespace Registration Rules (v0.1)

**Status:** Draft  
**Applies to:** `openindex.id` canonical registry

---

## 1. Purpose of Namespaces

A namespace in OpenIndex represents a **stable publishing identity**, not ownership of ideas or content.

Namespaces exist to:
- Group related records
- Provide provenance
- Enable discovery
- Reduce ambiguity

They do **not** imply exclusivity, copyright, or control over meaning.

---

## 2. What Can Be a Namespace

Namespaces may represent:
- Publishers
- Organizations
- Imprints
- Individuals (authors, creators)
- Collectives or projects

Examples:
```
/earthpress
/isaac-horton
/openmaps
```

---

## 3. Namespace Format Rules

Namespaces MUST:
- Be lowercase
- Use ASCII characters only
- Use hyphens (`-`) for separation
- Be between 3 and 63 characters
- Not end with a hyphen

Valid:
```
earthpress
open-maps
isaac-horton
```

Invalid:
```
EarthPress
open_maps
123
-press
```

---

## 4. Reserved Namespaces

The following are **reserved**:
- openindex
- admin
- api
- system
- www
- root
- test
- docs

Additional reserved names MAY be added.

---

## 5. First-Come, First-Served (With Guardrails)

Namespaces are generally assigned on a **first-come, first-served** basis, with protections against:
- Impersonation
- Trademark abuse
- Deceptive similarity
- Squatting without use

---

## 6. Proof of Control (Lightweight)

Any ONE of the following is sufficient:
- Control of a matching domain
- Control of a matching GitHub org/user
- Existing publication history
- Public website or imprint page

---

## 7. Registration Mechanism

Namespaces are registered via **Git pull request**.

Required file:
```
records/{namespace}/_namespace.json
```

Required fields:
```json
{
  "openindex": "https://openindex.id/{namespace}",
  "type": "namespace",
  "name": "Human-readable name",
  "description": "Short description",
  "created_at": "ISO-8601 timestamp",
  "record_version": "v1"
}
```

---

## 8. Review Process

- PR-based review
- Focus on rule compliance
- No content censorship
- Target review time: 7 days

---

## 9. Namespace Mutability

Namespaces are **append-only**.

Allowed:
- New records
- Metadata additions

Restricted:
- Renaming
- Reassignment
- Deletion

---

## 10. Disputes

OpenIndex does not adjudicate trademarks.

Resolution methods:
- Maintain status quo
- Request proof
- Encourage disambiguation

---

## 11. Abuse & Revocation

Namespaces may be frozen (not deleted) for:
- Impersonation
- Fraud
- Malware
- Automated spam

Frozen namespaces continue to resolve.

---

## 12. Governance Principle

**Namespaces are stewarded, not owned.**

---

## 13. Design Goals

This policy optimizes for:
- Longevity
- Neutrality
- Trust
- Low friction

---

## 14. Versioning

- v0.1 — Initial rules
- Future changes must be backward-compatible
