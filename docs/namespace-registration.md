## OpenIndex Namespace Registration

### Version

**v1.1 — Web-Based Registration Model**

----------

## 1. Overview

Namespaces are the primary organizational unit of OpenIndex.

To maximize accessibility, OpenIndex supports **web-based namespace registration**, allowing individuals, publishers, businesses, and organizations to apply without requiring developer tools or GitHub access.

Once approved, namespaces are authorized to publish immutable OpenIndex records.

----------

## 2. Namespace Structure

All namespaces are resolved using a path-based structure:

`https://openindex.id/<namespace>/`

Namespaces own all records published beneath their path.

----------

## 3. Who Can Register a Namespace?

Any individual or organization may apply, including:

-   publishers

-   authors

-   businesses

-   institutions

-   collectives

-   open projects


Applicants must:

-   represent a real entity

-   agree to the OpenIndex Terms

-   accept stewardship responsibility


----------

## 4. Web Registration Process

### Step 1: Submit Application

Applicants submit a namespace request via the OpenIndex web interface.

Required fields:

-   **Requested namespace**

-   **Applicant name**

-   **Organization (if applicable)**

-   **Public contact email**

-   **Declared scope**

-   **Intended record types**

-   **Agreement to Terms & Conditions**


All fields are validated automatically.

----------

### Step 2: Automated Pre-Checks

Before human review, the system performs:

-   namespace availability check

-   reserved-name validation

-   naming rule enforcement

-   scope completeness check


Applications that fail validation are rejected immediately with feedback.

----------

### Step 3: Maintainer Review

Valid submissions enter a review queue accessible to authorized maintainers.

Review criteria:

-   impersonation risk

-   scope clarity

-   conflict with existing namespaces

-   completeness and legitimacy


This process is intentionally similar to:

> payment processor onboarding or app store approvals

----------

### Step 4: Approval & Registration

Once approved:

1.  The namespace is marked **Approved**

2.  A canonical namespace record is automatically created

3.  The record is written following immutable record rules

4.  The applicant is notified of approval

5.  Publishing access is enabled


No manual Git operations are required.

----------

## 5. Namespace Record Creation (Automated)

Approval triggers automatic creation of a namespace record:

-   stored in the registry

-   versioned and immutable

-   resolvable immediately

-   linked to the namespace owner


This guarantees:

-   structural consistency

-   auditability

-   zero post-approval drift


----------

## 6. Namespace Permissions

Approved namespaces may:

-   publish records via web UI

-   publish records via API

-   perform bulk imports (where enabled)


Namespaces may not:

-   modify or delete existing records

-   publish outside declared scope

-   impersonate other namespaces


----------

## 7. Maintenance & Status

Namespaces may have the following states:

-   **Pending**

-   **Approved**

-   **Suspended**

-   **Deprecated**


Records remain resolvable in all states.

----------

## 8. Appeals & Updates

Applicants may:

-   appeal rejections

-   request scope clarification

-   update contact information


Scope expansions require maintainer approval.

----------

## 9. Future Extensions

This model supports:

-   delegated maintainer roles

-   automated trust scoring

-   private resolvers

-   federation with other registries

-   franchise and product verticals (future)
