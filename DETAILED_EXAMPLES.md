# Detailed Examples: Legal Document Templates

This document provides comprehensive, semantically similar examples for legal template solutions that match the scope and detail of the legal-yaml NDA example in the README.

## Reference: Legal-YAML NDA Example

The legal-yaml example demonstrates:
- Document-level metadata (label, type, variant, revision, id, tags, abstract)
- Multiple sections with embedded YAML blocks
- Field definitions with options
- Variable interpolation: `[Field: Name]`
- Conditional sections (optional, required_by)
- Option groups (multiple variants of same section)
- Template logic (foreach loops)
- Complete legal document structure (parties, terms, disclaimers, signatures, appendix)

---

## 1. Legal Markdown (flotob) - NDA Example

**Repository**: https://github.com/flotob/legalmarkdown  
**Documentation Source**: https://github.com/flotob/legalmarkdown (README.md)

This example shows a comparable NDA using Legal Markdown's syntax.

**Note on Syntax**: Legal Markdown uses square brackets with mixins for optional clauses (`[{{mixin_name}}text]`), where the mixin name corresponds to a boolean field in the YAML frontmatter. Variables are interpolated using double curly braces (`{{variable}}`). Legal Markdown does NOT support `@if/@else/@endif` or `@foreach` constructs in templates—those were incorrect in earlier versions of this document.

````markdown
---
title: Non-Disclosure Agreement
shorthand: NDA
document_type: nda
jurisdiction: Delaware
variant: delaware-c-corp-2025-q3
revision: 3
document_id: nda:delaware-c-corp-2025-q3:1
tags:
  - startup
  - formation
  - investors
  - investment
abstract: >
  The signing party agrees to not share non-public information about the issuing
  party's practices, trade secrets, intellectual property, or processes.
  
  That is all.

# Field definitions
issuer_company_name: "[ISSUER COMPANY NAME]"
recipient_name: "[RECIPIENT NAME]"
recipient_full_name: "[RECIPIENT FULL NAME]"
recipient_company_name: "[RECIPIENT COMPANY NAME]"
effective_date: "[EFFECTIVE DATE]"
recipient_initials: "[INITIALS]"
issuer_signature_name: "[ISSUER SIGNATURE NAME]"
issuer_signature_date: "[ISSUER SIGNATURE DATE]"
recipient_signature_name: "[RECIPIENT SIGNATURE NAME]"
recipient_signature_date: "[RECIPIENT SIGNATURE DATE]"

# Conditional flags
use_strict_terms: false
use_standard_terms: true
include_california_warning: false
signatures_with_california: false
signatures_without_california: true

# Exclusions
exclusion_1: "1. [EXCLUSION 1]"
exclusion_2: "2. [EXCLUSION 2]"
---

# Non-Disclosure Agreement

## 1. Parties and Purpose

This Non-Disclosure Agreement ('Agreement') is entered into on {{effective_date}}
by and between {{issuer_company_name}} (the Disclosing Party) and {{recipient_name}}
(the Receiving Party), each a 'Party', collectively the 'Parties'.

The Parties wish to explore a potential business relationship, during which the
Disclosing Party may disclose certain Confidential Information to the Receiving
Party solely for the Purpose of mutual benefit.

## 2. Confidential Information

[{{use_strict_terms}}

### 2.1 Strict Definition

Confidential Information means any non-public information, no matter the
source through which it was obtained.

Confidential Information does **not** include information publicly published
by the disclosing party, nor listed in appendix under exclusions.

]

[{{use_standard_terms}}

### 2.1 Standard Definition

Confidential Information means any non-public information disclosed by the
Disclosing Party to the Receiving Party, whether orally, in writing, or by
inspection, that is designated as confidential or that reasonably should be
understood to be confidential given the nature of the information and the
circumstances of disclosure.

This includes, but is not limited to, business plans, technical data, source
code, customer lists, financial information, trade secrets, and know-how.

Confidential Information does **not** include information that:
- (a) is or becomes publicly known through no fault of the Receiving Party;
- (b) was already known to the Receiving Party prior to disclosure;
- (c) is independently developed by the Receiving Party without use of or reference to
  the Disclosing Party's Confidential Information;
- (d) is lawfully received from a third party without restriction; or
- (e) must be disclosed by law (provided the Receiving Party gives prompt notice to the
  Disclosing Party to allow it to seek protective measures).

]

[{{include_california_warning}}

## 3. California Disclaimer

**P95 Warning**: It is known to the state of California that any action, legal or
otherwise, may cause birth defects or cancer.

Initial: {{recipient_initials}}

]

## [{{signatures_with_california}}4][{{signatures_without_california}}3]. Signatures

Hereby signed by Disclosing Party:
- Name: {{issuer_signature_name}}
- Date: {{issuer_signature_date}}
- Signature: _________________________

Hereby signed by Receiving Party:
- Name: {{recipient_signature_name}}
- Date: {{recipient_signature_date}}
- Signature: _________________________

## Appendix A: Exclusions

Items explicitly listed as excluded from the document:

{{exclusion_1}}
{{exclusion_2}}

````

**Key Features Demonstrated**:
- ✅ YAML frontmatter with document metadata
- ✅ Field definitions in frontmatter
- ✅ Optional clauses with `[{{condition}}text]` syntax
- ✅ Variable interpolation with `{{variable}}`
- ✅ Multiple sections with legal content
- ✅ Complete document structure

**Comparison to Legal-YAML**:
- Similar: YAML frontmatter, markdown prose, optional sections
- Different: No embedded YAML blocks per section; uses square brackets for optional clauses instead of YAML blocks

**Note on Syntax**: Legal Markdown uses square brackets with mixins for optional clauses (`[{{mixin_name}}text]`), where each mixin name must correspond to a boolean field in the YAML frontmatter (e.g., `use_strict_terms: true/false`). Variables use double curly braces (`{{variable}}`). Loops are not directly supported—lists must be defined as separate fields in YAML.

---

## 2. Accord Project Cicero - NDA Example

**Repository**: https://github.com/accordproject/cicero  
**Documentation Source**: https://docs.accordproject.org/docs/markup-cicero.html

This example shows a comparable NDA using Cicero's CiceroMark syntax with accompanying Concerto model.

**Important Note on Conditionals**: CiceroMark does NOT support `{{#if}}` conditional blocks in the template markup itself. Earlier versions of this document incorrectly showed such conditionals. In CiceroMark, conditional logic must be handled in the Ergo logic layer, which then populates different variable values. The template variables contain the appropriate text based on conditions evaluated in Ergo code.

### Template File (grammar.tem.md)

````markdown
Non-Disclosure Agreement

This Non-Disclosure Agreement ('Agreement') is entered into on {{effectiveDate}}
by and between {{issuerCompanyName}} (the Disclosing Party) and {{recipientName}}
(the Receiving Party), each a 'Party', collectively the 'Parties'.

The Parties wish to explore a potential business relationship, during which the
Disclosing Party may disclose certain Confidential Information to the Receiving
Party solely for the Purpose of mutual benefit.

{{#clause confidentialityTerms}}
## Confidential Information

{{confidentialityDefinition}}

{{confidentialityExclusions}}
{{/clause}}

{{#clause californiaDisclaimer}}
{{californiaWarningText}}
{{/clause}}

{{#clause signatures}}
## Signatures

Hereby signed by Disclosing Party:
- Name: {{issuerSignatureName}}
- Date: {{issuerSignatureDate}}
- Signature: _________________________

Hereby signed by Receiving Party:
- Name: {{recipientSignatureName}}
- Date: {{recipientSignatureDate}}
- Signature: _________________________
{{/clause}}

{{#clause appendix}}
## Appendix A: Exclusions

Items explicitly listed as excluded from the document:

{{exclusionsList}}
{{/clause}}
````

### Model File (model.cto)

```javascript
namespace org.accordproject.nda

import org.accordproject.cicero.contract.* from https://models.accordproject.org/cicero/contract.cto
import org.accordproject.cicero.runtime.* from https://models.accordproject.org/cicero/runtime.cto

/**
 * The template model
 */
asset NDAContract extends AccordContract {
  o String issuerCompanyName
  o String recipientName
  o DateTime effectiveDate
  o Boolean useStrictTerms default=false
  o Boolean includeCaliforniaWarning default=false
  o String recipientInitials optional
  o String issuerSignatureName
  o DateTime issuerSignatureDate
  o String recipientSignatureName
  o DateTime recipientSignatureDate
  o String[] exclusions optional
}

/**
 * Request to acknowledge receipt
 */
transaction AcknowledgeReceipt {
  o String party
}

/**
 * Response confirming acknowledgment
 */
transaction ReceiptAcknowledged {
  o String party
  o DateTime acknowledgedAt
}
```

### Package Metadata (package.json)

```json
{
  "name": "nda-agreement",
  "version": "1.0.0",
  "description": "Non-Disclosure Agreement template with variants",
  "accordproject": {
    "template": "contract",
    "cicero": "^0.22.0",
    "runtime": "ergo"
  },
  "keywords": [
    "nda",
    "confidentiality",
    "startup",
    "investment"
  ]
}
```

**Key Features Demonstrated**:
- ✅ Variable interpolation with `{{variable}}`
- ✅ Clause blocks with `{{#clause}}`
- ✅ Separate schema definition (Concerto model)
- ✅ Type system with optional fields
- ✅ Complete document structure

**Comparison to Legal-YAML**:
- Similar: Markdown prose, variable interpolation, modular clauses
- Different: Mustache-like syntax, separate schema files, blockchain-ready

**Important Note on Conditionals**: CiceroMark does NOT support `{{#if}}` conditionals in the template markup itself. Conditional logic must be handled in the Ergo logic layer, which then populates different variable values. The template uses simple variable placeholders that are populated by logic code.

**CiceroMark Syntax Reference**:
- Variables: `{{variableName}}`
- Formatted variables: `{{variableName as "FORMAT"}}`
- Ergo expressions (formulas): `{{% ergoExpression %}}`
- Clause blocks: `{{#clause clauseName}}...{{/clause}}`

---

## 3. Docassemble - NDA Example

**Repository**: https://github.com/jhpyle/docassemble  
**Documentation Source**: https://docassemble.org/docs/documents.html

This example shows a comparable NDA using Docassemble's interview YAML and template.

**Note on Template Syntax**: Docassemble uses **Mako** syntax for Markdown templates (`% if`, `% endif`, `${ variable }`) and **Jinja2** syntax for DOCX templates (`{% if %}`, `{% endif %}`, `{{ variable }}`). This example shows the Markdown/Mako approach.

### Interview File (nda_interview.yml)

```yaml
---
metadata:
  title: Non-Disclosure Agreement Generator
  short title: NDA
  description: Generate a customizable NDA with optional clauses
  revision_date: 2025-01-20
---
objects:
  - issuer: Individual
  - recipient: Individual
---
mandatory: True
code: |
  # Interview flow
  intro_screen
  issuer.name.first
  recipient_type
  if recipient_type == 'individual':
    recipient.name.first
  else:
    recipient_company
  effective_date
  terms_type
  if jurisdiction == 'california':
    california_warning_needed = True
  else:
    california_warning_needed = False
  if california_warning_needed:
    recipient_initials
  exclusions.gather()
  signature_info
  nda_generated
---
question: Welcome
subquestion: |
  This interview will help you generate a Non-Disclosure Agreement.
field: intro_screen
---
question: What is the name of the Disclosing Party (company)?
fields:
  - Company Name: issuer_company_name
---
question: Who is the Receiving Party?
field: recipient_type
choices:
  - Individual: individual
  - Company: company
---
question: What is the Receiving Party's name?
fields:
  - First Name: recipient.name.first
  - Last Name: recipient.name.last
---
question: What is the Receiving Party's company name?
fields:
  - Company Name: recipient_company
---
question: Agreement Details
fields:
  - Effective Date: effective_date
    datatype: date
  - Jurisdiction: jurisdiction
    choices:
      - Delaware: delaware
      - California: california
      - New York: newyork
---
question: Confidentiality Terms
subquestion: |
  Choose the type of confidentiality definition to use.
field: terms_type
choices:
  - Standard (with detailed exceptions): standard
  - Strict (minimal exceptions): strict
---
question: California Disclaimer
subquestion: |
  California law requires a P95 warning. Please provide your initials to acknowledge.
fields:
  - Your Initials: recipient_initials
    maxlength: 5
---
question: Exclusions
subquestion: |
  List any items explicitly excluded from confidential information.
list collect: True
fields:
  - Exclusion: exclusions[i]
    required: False
---
question: Signature Information
fields:
  - Issuer Signature Name: issuer_signature_name
    default: ${ issuer_company_name }
  - Issuer Signature Date: issuer_signature_date
    datatype: date
  - Recipient Signature Name: recipient_signature_name
    default: ${ recipient.name.full() if recipient_type == 'individual' else recipient_company }
  - Recipient Signature Date: recipient_signature_date
    datatype: date
---
event: nda_generated
question: Your NDA is ready
subquestion: |
  Your Non-Disclosure Agreement has been generated.
  
  You can download it below.
buttons:
  - Download PDF: download
  - Download Word: download_docx
  - Exit: exit
attachment:
  - name: Non-Disclosure Agreement
    filename: NDA_${ issuer_company_name }_${ effective_date }
    description: |
      Non-Disclosure Agreement between ${ issuer_company_name } and 
      ${ recipient.name.full() if recipient_type == 'individual' else recipient_company }
    docx template file: nda_template.docx
    valid formats:
      - pdf
      - docx
    metadata:
      document_type: nda
      jurisdiction: ${ jurisdiction }
      variant: ${ jurisdiction }-corp-2025-q3
      revision: 3
```

### Template File (nda_template.docx - represented as markdown)

```markdown
# NON-DISCLOSURE AGREEMENT

**Document ID**: nda:${ jurisdiction }-corp-2025-q3:1
**Tags**: startup, formation, investors, investment

## Abstract

The signing party agrees to not share non-public information about the issuing
party's practices, trade secrets, intellectual property, or processes.

---

## 1. Parties and Purpose

This Non-Disclosure Agreement ('Agreement') is entered into on ${ format_date(effective_date) }
by and between ${ issuer_company_name } (the Disclosing Party) and 
${ recipient.name.full() if recipient_type == 'individual' else recipient_company }
(the Receiving Party), each a 'Party', collectively the 'Parties'.

The Parties wish to explore a potential business relationship, during which the
Disclosing Party may disclose certain Confidential Information to the Receiving
Party solely for the Purpose of mutual benefit.

## 2. Confidential Information

%if terms_type == 'strict':

**Strict Definition**

Confidential Information means any non-public information, no matter the
source through which it was obtained.

Confidential Information does **not** include information publicly published
by the disclosing party, nor listed in appendix under exclusions.

%else:

**Standard Definition**

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

%endif

%if california_warning_needed:
## 3. California Disclaimer

**P95 Warning**: It is known to the state of California that any action, legal or
otherwise, may cause birth defects or cancer.

Initial: ${ recipient_initials }
%endif

## ${ '4' if california_warning_needed else '3' }. Signatures

Hereby signed by Disclosing Party:
- Name: ${ issuer_signature_name }
- Date: ${ format_date(issuer_signature_date) }
- Signature: _________________________

Hereby signed by Receiving Party:
- Name: ${ recipient_signature_name }
- Date: ${ format_date(recipient_signature_date) }
- Signature: _________________________

## Appendix A: Exclusions

Items explicitly listed as excluded from the document:

%for index, exclusion in enumerate(exclusions, 1):
${ index }. ${ exclusion }
%endfor
```

**Key Features Demonstrated**:
- ✅ YAML-based interview structure
- ✅ Field definitions with types (date, text, choice)
- ✅ Conditional logic in interview flow
- ✅ Object-oriented data (Individual, Company)
- ✅ List collection for multiple items
- ✅ Variable interpolation in template `${ variable }`
- ✅ Conditional sections in template `%if`/`%endif`
- ✅ Loops in template `%for`
- ✅ Complete document structure with metadata

**Comparison to Legal-YAML**:
- Similar: YAML structure, field definitions, conditionals, loops, document metadata
- Different: Separate interview file + template file, interview-driven workflow, Python-like template syntax

---

## 4. OpenLaw - NDA Example

**Website**: https://www.openlaw.io/  
**Documentation Source**: https://docs.openlaw.io/markup-language/

This example shows a comparable NDA using OpenLaw's markup language.

**Note on Conditional Syntax**: OpenLaw uses mustache-style conditional blocks with function calls. For conditionals, use `{{#if condition}}...{{/if}}` where condition can be a boolean variable or a function like `(equals [[Variable]] "value")`. Earlier versions of this document used incorrect comparison syntax (`[[var]] = "value"`)—the correct syntax requires the `equals` function.

````markdown
<%
==Template Name==
Non-Disclosure Agreement (NDA)

==Template Description==
A comprehensive non-disclosure agreement with configurable terms and optional California disclaimer.

==Metadata==
[[Document Type: "nda"]]
[[Jurisdiction: "delaware"]]
[[Variant: "delaware-corp-2025-q3"]]
[[Revision: "3"]]
[[Document ID: "nda:delaware-corp-2025-q3:1"]]
[[Tags: "startup, formation, investors, investment"]]

==Variables==
[[Issuer Company Name]]
[[Recipient Name]]
[[Recipient Type: Choice("Individual","Company")]]
[[Effective Date: Date]]
[[Use Strict Terms: YesNo]]
[[Jurisdiction: Choice("Delaware","California","New York")]]
[[Recipient Initials]]
[[Issuer Signature Name]]
[[Issuer Signature Date: Date]]
[[Recipient Signature Name]]
[[Recipient Signature Date: Date]]
[[Exclusions: Collection<Text>]]
%>

# NON-DISCLOSURE AGREEMENT

**Abstract**: The signing party agrees to not share non-public information about the issuing party's practices, trade secrets, intellectual property, or processes.

---

## 1. Parties and Purpose

This Non-Disclosure Agreement ('Agreement') is entered into on [[Effective Date]]
by and between [[Issuer Company Name]] (the Disclosing Party) and [[Recipient Name]]
(the Receiving Party), each a 'Party', collectively the 'Parties'.

The Parties wish to explore a potential business relationship, during which the
Disclosing Party may disclose certain Confidential Information to the Receiving
Party solely for the Purpose of mutual benefit.

## 2. Confidential Information

{{#if [[Use Strict Terms]]}}

**Strict Definition**

Confidential Information means any non-public information, no matter the
source through which it was obtained.

Confidential Information does **not** include information publicly published
by the disclosing party, nor listed in appendix under exclusions.

{{else}}

**Standard Definition**

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

{{/if}}

{{#if (equals [[Jurisdiction]] "California")}}
## 3. California Disclaimer

**P95 Warning**: It is known to the state of California that any action, legal or
otherwise, may cause birth defects or cancer.

Initial: [[Recipient Initials]]
{{/if}}

## {{#if (equals [[Jurisdiction]] "California")}}4{{else}}3{{/if}}. Signatures

Hereby signed by Disclosing Party:
- Name: [[Issuer Signature Name]]
- Date: [[Issuer Signature Date]]
- Signature: [[Issuer Signature: Signature]]

Hereby signed by Receiving Party:
- Name: [[Recipient Signature Name]]
- Date: [[Recipient Signature Date]]
- Signature: [[Recipient Signature: Signature]]

## Appendix A: Exclusions

Items explicitly listed as excluded from the document:

{{#for exclusion: [[Exclusions]]}}
[[exclusion]]
{{/for}}
````

**Key Features Demonstrated**:
- ✅ Template metadata block with structured info
- ✅ Variable declarations with types (Date, YesNo, Choice, Collection)
- ✅ Variable interpolation with `[[Variable Name]]`
- ✅ Typed variables (including Signature type for e-signatures)
- ✅ Conditional blocks with `{{#if}}`/`{{else}}`/`{{/if}}`
- ✅ Collection iteration with `{{#for}}`
- ✅ Complete document structure
- ✅ Blockchain-ready signatures

**Comparison to Legal-YAML**:
- Similar: Metadata block, conditionals, loops, typed fields
- Different: `[[variable]]` syntax, blockchain integration, e-signature support

**OpenLaw Syntax Reference**:
- Variables: `[[Variable Name]]` or `[[Variable Name: Type]]`
- Conditionals: `{{#if condition}}...{{else}}...{{/if}}`
- Functions: `(equals [[var]] "value")`, `(and cond1 cond2)`, `(or cond1 cond2)`
- Loops: `{{#for item: [[Collection]]}}...{{/for}}`

---

## Solutions Marked Off (Not Similar Enough)

### ❌ HotDocs

**Website**: https://www.hotdocs.com/

**Reason**: HotDocs is a proprietary, desktop-based application that uses Word documents with embedded field codes. It cannot be represented as a comparable plain-text template like the legal-yaml example. The workflow is fundamentally different (GUI-based form builder vs. code-first approach).

**What it would look like**: Variables embedded in Word doc as `«Variable Name»` or `[VarName;te]`, with separate dialog definitions in a proprietary format.

### ❌ Dot Legal Reference

**Website**: https://reference.legal/  
**Repository**: https://github.com/dot-legal/reference

**Reason**: This is a clause library system using URL references, not a template system with variable interpolation. It operates on a completely different paradigm (composition by reference vs. template with variables).

**What it would look like**:
```text
Non-Disclosure Agreement

Incorporate https://reference.legal/v1/provisions/nda/parties/2025-01-01
Incorporate https://reference.legal/v1/provisions/nda/confidential-info/standard/2025-01-01
Incorporate https://reference.legal/v1/provisions/general/signatures/2025-01-01

With the following modifications:
- Effective Date: January 15, 2025
- Disclosing Party: ACME Corp
- Receiving Party: John Smith
```

This doesn't support the detailed field definitions, conditional sections, or embedded metadata that legal-yaml provides.

---

## Summary

### Solutions with Detailed Examples Created:

1. ✅ **Legal Markdown (flotob)** - Complete NDA with YAML frontmatter and optional clauses using `[{{condition}}text]` syntax
2. ✅ **Accord Project Cicero** - Complete NDA with CiceroMark template + Concerto model (logic in Ergo layer)
3. ✅ **Docassemble** - Complete NDA with interview YAML + Mako template file
4. ✅ **OpenLaw** - Complete NDA with markup language and blockchain features

### Solutions Marked Off (Not Comparable):

5. ❌ **HotDocs** - GUI-based Word document system, not plain-text comparable
6. ❌ **Dot Legal Reference** - URL-based clause library, different paradigm

### Accuracy Notes:

All examples have been verified against official documentation:
- **Legal Markdown**: Uses `[{{condition}}text]` for optional clauses, not `@if/@else/@endif`
- **Accord Project Cicero**: Conditionals handled in Ergo logic, not in template with `{{#if}}`
- **Docassemble**: Mako syntax verified (`% if`, `${ variable }`)
- **OpenLaw**: Uses function syntax `(equals [[var]] "value")` for comparisons

Each example demonstrates:
- Complete legal document structure (parties, terms, disclaimers, signatures, appendix)
- Variable interpolation and field definitions
- Conditional sections (where supported by the system)
- Document metadata
- Multiple sections with legal prose

These examples are semantically comparable in scope and detail to the legal-yaml NDA example in the README. Source documentation links are provided for each system.
