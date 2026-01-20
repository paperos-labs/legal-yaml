# Research Summary: Existing Legal Template Solutions

This document provides a concise summary of the research into existing legal document template solutions and their comparison with legal-yaml.

## Executive Summary

After researching existing solutions (docassemble, Accord Project Cicero, legalmarkdown, dot-legal, OpenLaw, and HotDocs), we found that **Legal Markdown (flotob)** shares the most similar style with legal-yaml.

### Top 3 Most Similar Solutions:

1. **🥇 Legal Markdown (flotob)** - YAML frontmatter + Markdown + preprocessing directives
2. **🥈 Docassemble** - Heavy YAML usage with field-based variables
3. **🥈 Accord Project Cicero** - Markdown with variable interpolation for smart contracts

## Visual Style Comparison

### Legal-YAML Style

```markdown
---
label: Non-Disclosure Agreement
type: nda
variant: delaware-c-corp-2025-q3
revision: 3
tags:
    - startup
    - formation
---

```yaml
label: Parties and Purpose
type: nda:parties-and-purpose
uses:
    - field: issuer:company_name
    - field: recipient:name
    - field: effective_date
```

This Non-Disclosure Agreement ('Agreement') is entered into on [Effective Date]
by and between [Issuer: Company Name] (the Disclosing Party) and [Recipient: Name]
(the Receiving Party).
```

**Key Features:**
- YAML frontmatter for document metadata
- Embedded YAML blocks for section metadata
- `[Field: Name]` syntax for variables (human-readable)
- Markdown for legal prose

---

### Legal Markdown (flotob) - MOST SIMILAR ⭐⭐⭐⭐⭐

```markdown
---
title: Non-Disclosure Agreement
effective_date: 2024-01-01
parties:
  - Party A
  - Party B
---

# 1. Definitions

@if(CONFIDENTIAL_INFORMATION)
## 2. Confidential Information
The Recipient shall keep all information confidential...
@endif

@include {{SignatureBlock}}
```

**Similarities:**
- ✅ YAML frontmatter for metadata
- ✅ Markdown for content
- ✅ Plain text, git-friendly
- ✅ Preprocessor approach
- ✅ Modular with includes

**Differences:**
- Uses `@include` and `@if` directives (vs. embedded YAML blocks)
- Simpler variable system
- Less structured section metadata

---

### Accord Project Cicero (CiceroMark) ⭐⭐⭐⭐

```markdown
## Fixed rate loan

This is a *fixed interest* loan to the amount of {{loanAmount}} 
at the yearly interest rate of {{rate}}% with a loan term of {{loanDuration}}, 
and monthly payments of {{% monthlyPaymentFormula(loanAmount,rate,loanDuration) %}}.

{{#clause paymentClause}}
Payment terms...
{{/clause}}
```

**Similarities:**
- ✅ Markdown-based
- ✅ Variable interpolation
- ✅ Modular clauses
- ✅ Legal contract focus

**Differences:**
- Uses `{{variable}}` syntax (Mustache-like)
- Inline calculations with `{{% expression %}}`
- Separate Concerto schema files
- Smart contract execution (Ergo)

---

### Docassemble ⭐⭐⭐⭐

```yaml
---
metadata:
  title: Simple Contract
  description: Interview to generate a basic contract
---
question: What is your full name?
fields:
  - Name: client_name
---
question: What is the contract start date?
fields:
  - Date: contract_start
---
attachment:
  - name: Contract Document
    filename: simple_contract.docx
    docx template file: simple_contract_template.docx
```

**Similarities:**
- ✅ Heavy YAML usage
- ✅ Separation of metadata and content
- ✅ Field-based variables
- ✅ Conditional logic

**Differences:**
- Interview workflow (questions → answers → document)
- Separate template files (not inline)
- Variables in templates: `${ variable }` or `{{ variable }}`
- Server-based application

---

### OpenLaw ⭐⭐⭐

```
This Confidentiality Agreement is made on [[Effective Date: Date]] 
between [[Discloser Name]] and [[Recipient Name]].

{% if [[IncludeNonCompete: Boolean]] %}
The parties also agree to a non-compete provision for [[Duration: Number]] years.
{% endif %}
```

**Similarities:**
- ✅ Variable interpolation
- ✅ Typed variables
- ✅ Conditional logic

**Differences:**
- Uses `[[Variable Name: Type]]` syntax
- Blockchain/Ethereum integration
- Custom markup language
- Designed for smart legal contracts

---

### HotDocs ⭐⭐

```
The client, [ClientName;te;format=upper], hereby rescinds all previous claims.
Payment due: [AmountDue;nu]
Effective date: [EffectiveDate;da]
```

**Similarities:**
- ✅ Variable-based templates
- ✅ Typed variables

**Differences:**
- Proprietary commercial software
- Word document-based
- `[VarName;type;options]` or `«VarName»` syntax
- Desktop application, not plain text

---

### Dot Legal Reference ⭐⭐

```
Incorporate https://reference.legal/v1/provisions/general/counterparts/
Incorporate https://reference.legal/v1/provisions/general/force-majeure/2021-06-30
```

**Similarities:**
- ✅ Modular approach
- ✅ Version control

**Differences:**
- URL-based references (not inline templates)
- Clause library, not template system
- Different paradigm (include vs. define)

---

## What Makes Legal-YAML Unique

1. **Embedded YAML Blocks**: Section-level metadata within the document (not just frontmatter)
2. **Human-Readable Variables**: `[Field: Name]` is more natural than `{{var}}` or `[[var]]`
3. **Tree-like Versioning**: variant/revision model instead of semver
4. **Option Groups**: Multiple variants of same section with easy swapping
5. **Template Inheritance**: `from:`, `replaces:`, `provides:` for composition

## Key Insight

Legal-YAML appears to be an **evolution** of Legal Markdown's approach, adding:
- More sophisticated section-level metadata (embedded YAML blocks)
- Structured variant/option system for multiple versions
- Better document composition via inheritance
- More explicit versioning strategy (variant + revision)

## Recommendations

### For Users Seeking Alternatives:

1. **Most similar syntax**: [Legal Markdown (flotob)](https://github.com/flotob/legalmarkdown)
2. **Most features**: [Docassemble](https://docassemble.org/) (if you need interview workflow)
3. **Smart contracts**: [Accord Project Cicero](https://accordproject.org/) or [OpenLaw](https://www.openlaw.io/)
4. **Enterprise**: [HotDocs](https://www.hotdocs.com/) (commercial solution)
5. **Minimal approach**: [Dot Legal Reference](https://reference.legal/) (for clause libraries)

### For Legal-YAML Development:

Consider adopting or learning from:
- **Legal Markdown's** simplicity in preprocessing
- **Cicero's** clear variable syntax
- **Docassemble's** structured field definitions
- **OpenLaw's** type system for variables

## Additional Resources

See [EXISTING_SOLUTIONS.md](EXISTING_SOLUTIONS.md) for detailed comparisons, examples, and references.

---

*Research completed: January 2026*
