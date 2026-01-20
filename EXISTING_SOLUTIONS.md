# Existing Solutions Comparison

This document compares legal-yaml with other existing legal document template solutions, focusing on their syntax, style, and approach.

## Legal-YAML Style Summary

The legal-yaml project uses a distinctive hybrid approach:

1. **YAML frontmatter** (`---...---`) for document-level metadata
2. **Embedded YAML blocks** (` ```yaml `) within markdown for section-level configuration
3. **Markdown prose** for the actual legal text
4. **Variable interpolation** using `[Field: Name]` syntax (human-readable)
5. **Template logic** with `{foreach}...{- end}` constructs
6. **Versioning strategy**: variant (major), revision (minor), with tree-like history
7. **Conditional sections**: `optional: true`, `required_by: [list]`
8. **Option groups**: Multiple variants of the same section (`group:`, `option:`)
9. **Template inheritance**: `from:`, `replaces:`, `provides:` for document composition

## Similar Solutions

### 1. Docassemble

**Website**: https://docassemble.org/  
**Repository**: https://github.com/jhpyle/docassemble

#### Similarities to Legal-YAML:
- ✅ Uses YAML as primary structure
- ✅ Separates metadata from content
- ✅ Supports conditional logic
- ✅ Field-based variable system
- ✅ Modular clause/section approach

#### Key Differences:
- **Style**: Interview-based workflow (questions → answers → document)
- **Syntax**: Variables in templates use `${ variable_name }` or `{{ variable_name }}`
- **Architecture**: Separate YAML for logic + separate template files (DOCX/Markdown)
- **Purpose**: More focused on user interviews and data collection
- **Processing**: Server-based application (not just file format)

#### Example:
```yaml
---
metadata:
  title: Simple Contract
mandatory: True
---
question: What is your full name?
fields:
  - Name: client_name
---
attachment:
  - name: Contract Document
    filename: simple_contract.docx
    docx template file: simple_contract_template.docx
```

**Similarity Score**: ⭐⭐⭐⭐ (4/5) - Very similar YAML structure, different workflow model

---

### 2. Accord Project - Cicero (CiceroMark)

**Website**: https://accordproject.org/projects/cicero/  
**Templates**: https://templates.accordproject.org/  
**Repository**: https://github.com/accordproject/cicero

#### Similarities to Legal-YAML:
- ✅ Markdown-based for legal prose
- ✅ Variable interpolation in text
- ✅ Modular clause system
- ✅ Supports conditional logic
- ✅ Designed for legal contracts

#### Key Differences:
- **Style**: Markdown extension (CiceroMark)
- **Syntax**: Variables use `{{variableName}}` (double curly braces)
- **Logic**: Inline calculations with `{{% expression %}}`
- **Clause blocks**: `{{#clause name}}...{{/clause}}`
- **Schema**: Separate Concerto model files for data definitions
- **Purpose**: Smart legal contracts with executable logic (Ergo language)

#### Example:
```markdown
## Fixed rate loan
This is a *fixed interest* loan to the amount of {{loanAmount}} 
at the yearly interest rate of {{rate}}% with a loan term of {{loanDuration}}, 
and monthly payments of {{% monthlyPaymentFormula(loanAmount,rate,loanDuration) %}}.
```

**Similarity Score**: ⭐⭐⭐⭐ (4/5) - Similar markdown approach, different variable syntax

---

### 3. Legal Markdown (flotob)

**Repository**: https://github.com/flotob/legalmarkdown

#### Similarities to Legal-YAML:
- ✅ Markdown-based
- ✅ YAML frontmatter for metadata
- ✅ Modular with `@include` for clauses
- ✅ Supports optional clauses
- ✅ Plain text, version-controllable

#### Key Differences:
- **Style**: Simpler, preprocessor approach
- **Syntax**: `@include {{PARTIAL}}` for modularity
- **Conditionals**: `@if(CONDITION) ... @endif`
- **Variables**: Less structured variable system
- **Purpose**: General legal markdown with preprocessing

#### Example:
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

**Similarity Score**: ⭐⭐⭐⭐⭐ (5/5) - VERY similar! YAML frontmatter + Markdown + preprocessing

---

### 4. Dot Legal Reference

**Website**: https://reference.legal/  
**Repository**: https://github.com/dot-legal/reference

#### Similarities to Legal-YAML:
- ✅ Modular clause approach
- ✅ Version control (via URL dates)
- ✅ Designed for composability
- ✅ Open source

#### Key Differences:
- **Style**: URL-based reference system (not inline)
- **Syntax**: Plain text with hyperlinks
- **Approach**: Library of clauses, not templates
- **Purpose**: Hide boilerplate via hyperlinks
- **Processing**: Reference by inclusion, not variable substitution

#### Example:
```
Incorporate https://reference.legal/v1/provisions/general/counterparts/
Incorporate https://reference.legal/v1/provisions/general/force-majeure/2021-06-30
```

**Similarity Score**: ⭐⭐ (2/5) - Different approach (references vs. templates)

---

### 5. OpenLaw

**Website**: https://www.openlaw.io/  
**Docs**: https://docs.openlaw.io/markup-language/

#### Similarities to Legal-YAML:
- ✅ Structured legal templates
- ✅ Variable interpolation
- ✅ Conditional logic
- ✅ Modular clause system

#### Key Differences:
- **Style**: Custom markup language
- **Syntax**: Variables use `[[Variable Name: Type]]` (double square brackets)
- **Conditionals**: `{% if [[condition]] %} ... {% endif %}`
- **Purpose**: Blockchain-based smart legal contracts
- **Processing**: Integrated with Ethereum blockchain

#### Example:
```
This Confidentiality Agreement is made on [[Effective Date: Date]] 
between [[Discloser Name]] and [[Recipient Name]].

{% if [[IncludeNonCompete: Boolean]] %}
The parties also agree to a non-compete provision for [[Duration: Number]] years.
{% endif %}
```

**Similarity Score**: ⭐⭐⭐ (3/5) - Similar concept, different syntax and integration focus

---

### 6. HotDocs

**Website**: https://www.hotdocs.com/

#### Similarities to Legal-YAML:
- ✅ Variable-based templates
- ✅ Typed variables (text, number, date)
- ✅ Conditional sections
- ✅ Reusable components

#### Key Differences:
- **Style**: Proprietary commercial software
- **Syntax**: Variables use `[VarName;type;options]` or `«VarName»`
- **Format**: Word document-based
- **Purpose**: Enterprise document automation
- **Processing**: Desktop application, not plain text files

#### Example:
```
The client, [ClientName;te;format=upper], hereby rescinds all previous claims.
Payment due: [AmountDue;nu]
Effective date: [EffectiveDate;da]
```

**Similarity Score**: ⭐⭐ (2/5) - Similar goals, proprietary and not markdown-based

---

## Most Similar Solutions

Based on style, syntax, and approach, ranked by similarity:

### 🥇 1st Place: Legal Markdown (flotob) - 5/5
**Most similar overall!**
- YAML frontmatter for metadata
- Markdown for content
- Preprocessor directives (`@include`, `@if`)
- Plain text, git-friendly
- Focus on modularity and simplicity

### 🥈 2nd Place: Docassemble - 4/5
- Heavy YAML usage
- Separation of concerns (metadata vs. content)
- Field-based variable system
- Conditional logic support
- Different workflow (interview-based)

### 🥈 2nd Place (tied): Accord Project Cicero - 4/5
- Markdown-based prose
- Variable interpolation
- Modular clauses
- Legal contract focus
- Different variable syntax (`{{var}}` vs. `[Field: Name]`)

### 🥉 3rd Place: OpenLaw - 3/5
- Structured templates
- Variable and conditional logic
- Different syntax (`[[var]]` vs. `[Field: Name]`)
- Blockchain integration focus

---

## Key Insights

### What Makes Legal-YAML Unique:

1. **Hybrid Structure**: YAML blocks embedded in markdown (not just frontmatter)
2. **Human-Readable Variables**: `[Field: Name]` syntax is more natural than `{{var}}` or `[[var]]`
3. **Tree-like Versioning**: variant/revision model instead of semver
4. **Section-Level Metadata**: Each section has its own YAML config block
5. **Option Groups**: Multiple variants of same section for easy swapping

### Closest Conceptual Match:

**Legal Markdown (flotob)** shares the most DNA with legal-yaml:
- Both use YAML + Markdown combination
- Both emphasize plain text and version control
- Both support modular clauses
- Both designed for legal professionals who understand git/text files
- Main difference: legal-yaml is more structured with embedded YAML blocks per section

### Evolution Insight:

Legal-YAML appears to be an evolution of Legal Markdown's approach, adding:
- More sophisticated section-level metadata
- Structured variant/option system
- Better support for document composition via `from:`/`replaces:`
- More explicit versioning strategy

---

## References

1. Docassemble: https://docassemble.org/docs/overview.html
2. Accord Project Cicero: https://docs.accordproject.org/docs/markup-cicero.html
3. Legal Markdown: https://github.com/flotob/legalmarkdown
4. Dot Legal Reference: https://github.com/dot-legal/reference
5. OpenLaw: https://docs.openlaw.io/markup-language/
6. HotDocs: https://help.hotdocs.com/

---

## Recommendation

For projects or users looking for alternatives to legal-yaml, consider:

1. **Most similar syntax**: Legal Markdown (flotob)
2. **Most features**: Docassemble (if you need interview workflow)
3. **Smart contracts**: Accord Project Cicero or OpenLaw
4. **Enterprise**: HotDocs (commercial solution)
5. **Minimal approach**: Dot Legal Reference (for clause libraries)
