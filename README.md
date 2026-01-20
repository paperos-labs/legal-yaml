# legal-yaml

Prototyping what legal YAML might look like

For a comparison with existing legal document template solutions, see:
- [RESEARCH_SUMMARY.md](RESEARCH_SUMMARY.md) - Quick visual comparison
- [EXISTING_SOLUTIONS.md](EXISTING_SOLUTIONS.md) - Detailed analysis
- [DETAILED_EXAMPLES.md](DETAILED_EXAMPLES.md) - Complete NDA examples in each syntax

## Key features

- YAML as LLM output
- whole documents
- clauses
- templates (date, amount, etc)
- variants & versions
- tag search
- semantic search
- incompatibilities
- conditional groups
- required groups

## Draft Syntax

### Base Document

The base document would define common sections and the variables for each.

````mkdn
---
label: Non-Disclosure Agreement
shorthand: NDA # optional
type: nda
variant: delaware-c-corp-2025-q3
revision: 3
id: nda:delaware-c-corp-2025-q3:1
tags:
    - startup
    - formation
    - investors
    - investment
abstract: >
    The signing party agrees to not share non-public information about the issuing
    party's practices, trade secrets, intellectual property, or processes.

    That is all.
---

```yaml
label: Parties and Purpose
type: nda:parties-and-purpose
variant: 2025-q3
revision: 1
id: nda:parties-and-purpose:delaware-c-corp-2025-q3:1
uses:
    - field: issuer:company_name
    - field: recipient:name
      options:
          - recipient:full_name
          - recipient:company_name
    - field: effective_date
```

This Non-Disclosure Agreement ('Agreement') is entered into on [Effective Date]
by and between [Issuer: Company Name] (the Disclosing Party) and [Recipient: Name]
(the Receiving Party), each a 'Party', collectively the 'Parties'.

The Parties wish to explore a potential business relationship, during which the
Disclosing Party may disclose certain Confidential Information to the Receiving
Party solely for the Purpose of mutual benefit.

```yaml
label: Confidential Information
group: nda:terms
option: nda:normal_terms:delaware-c-corp-2025-q3:1
```

Confidential Information means any non-public information disclosed by the
Disclosing Party to the Receiving Party, whether orally, in writing, or by
inspection, that is designated as confidential or that reasonably should be
understood to be confidential given the nature of the information and the
circumstances of disclosure.
This includes, but is not limited to, business plans, technical data, source
code, customer lists, financial information, trade secrets, and know-how.

Confidential Information does **not** include information that:
(a) is or becomes publicly known through no fault of the Receiving Party;
(b) was already known to the Receiving Party prior to disclosure;
(c) is independently developed by the Receiving Party without use of or reference to
the Disclosing Party's Confidential Information;
(d) is lawfully received from a third party without restriction; or
(e) must be disclosed by law (provided the Receiving Party gives prompt notice to the
Disclosing Party to allow it to seek protective measures).

```yaml
group: nda:terms
option: nda:strict_terms:delaware-c-corp-2025-q3:1
```

Confidential Informations means any non-public information, no matter the
source through which it was obtained.

Confidential Information does **not** include information publicly published
by the disclosing party, nor listed in appendix under exclusions.

```yaml
label: CA Disclaimer
revision: 3
optional: true
required_by:
    - california
tags:
    - california
    - cancer
id: nda:california_terms
uses:
    - field: recipient:initials
```

P95 Warning: It is known to the state of California that any actian, legal or
otherwise, may cause birth defects or cancer.

Initial: [Recipient: Initials]

```yaml
label: Signature
id: nda:signature
uses:
    - field: recipient:signature_name
    - field: recipient:signature_date
    - field: issuer:signature_name
    - field: issuer:signature_text
    - field: issuer:signature_date
```

Hereby signed by Disclosing Party:
Name: [Issuer: Signature Text]
Date: [Issuer: Signature Text]
Signature: [Issuer: Signature Text]

Hereby signed by Receiving Party:
Name: [Recipient: Signature Text]
Date: [Recipient: Signature Text]
Signature: [Recipient: Signature Text]

```yaml
label: Appendix
type: nda:appendix
uses:
    - field: exclusions
      multiple: true
      minimum: 0
```

Items explicitly listed as excluded from the document:
{foreach exclusion of exclusions}
{index}. {exclusion}
{- end}
````

Since the document histories might be more tree-like than linear, I'm proposing that instead of semver we use a strategy like this:

- variant: major change, possibly breaking, due to change in law or application (e.g. Delaware v Utah)
- revision: minor change (e.g. typo fix, clarification)
- any revision to a section first increments the document revision, and then applies that to the section \
  (such that document changes are linear, but section changes may jump)
- variant changes to a section create a new document variant which may reference the previous document

### Templated Document

The templated document would have fewer options than the base document and pre-fill some data.

````mkdn
---
from: nda:delaware-c-corp-2025-q3:1
label: Non-Disclosure Agreement
type: nda
variant_label: ACME, Inc v2
---

```yaml
label: Parties and Purpose
replaces: nda:parties-and-purpose:delaware-c-corp-2025-q3
variant: acme-inc-2026-q1
id: nda:acme-inc-2026-q1
# tells the checker not to complain that a variable was not provided
provides:
    - field: issuer:company_name
```

This is a Non-Disclosure Agreement between [ACME, Inc (issuer:company_name)] (Disclosing Party) and
[Recipient: Name] beginning [Effective Date].

```yaml
from: nda:strict_terms:delaware-c-corp-2025-q3:1
```

Confidential Informations means any non-public information, no matter the
source through which it was obtained.

Confidential Information does **not** include information publicly published
by the disclosing party, nor listed in appendix under exclusions.

```yaml
from: nda:signature
```

Hereby signed by Disclosing Party:
Name: [Issuer: Signature Text]
Date: [Issuer: Signature Text]
Signature: [Issuer: Signature Text]

Hereby signed by Receiving Party:
Name: [Recipient: Signature Text]
Date: [Recipient: Signature Text]
Signature: [Recipient: Signature Text]
````

## Practical Problems

- nested yaml is nasty - frontmatter may solve this (think presentation slides)
- whole documents and sections need version info, but it can't get complex
- humans will name variants things like "equity-purchase-acme-inc-final-final-2026-really-final"
- humans will not tag accurately tag incompatible clauses
- automation provides a false sense of security
- need pre-processing, otherwise we have complex template rules that non-programmers aren't good at
- needs post-processing for data structure, otherwise we have empty lists
- pre-processing and post-processing means an LLM is less likely to have good training data to get it right
- duplication is probably better than nesting because humans generally don't get recursion
