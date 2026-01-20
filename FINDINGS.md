# Findings: Research on Existing Legal Template Solutions

## Summary

I've completed comprehensive research on existing legal document template solutions and compared them with the legal-yaml approach. The findings are documented in two new files:

### Documents Created:

1. **[RESEARCH_SUMMARY.md](RESEARCH_SUMMARY.md)** - Quick visual comparison with side-by-side examples
2. **[EXISTING_SOLUTIONS.md](EXISTING_SOLUTIONS.md)** - Detailed analysis with scoring and recommendations
3. **[DETAILED_EXAMPLES.md](DETAILED_EXAMPLES.md)** - Complete NDA examples in each comparable syntax

### Key Finding: Most Similar Solution

**Legal Markdown (flotob)** - https://github.com/flotob/legalmarkdown

This is the **most similar** solution to legal-yaml with a similarity score of ⭐⭐⭐⭐⭐ (5/5).

**Why it's similar:**
- Uses YAML frontmatter for metadata
- Uses Markdown for legal prose content
- Plain text, git-friendly approach
- Supports modular clauses with `@include`
- Supports conditional sections with `@if`
- Preprocessing approach for template logic

**Key difference:**
Legal-YAML appears to be an evolution of Legal Markdown, adding:
- Embedded YAML blocks for section-level metadata (not just frontmatter)
- More structured variant/option system
- Better document composition via `from:`, `replaces:`, `provides:`
- Explicit tree-like versioning (variant + revision)

## All Solutions Compared

### Ranked by Similarity:

1. **🥇 Legal Markdown (flotob)** - 5/5
   - YAML frontmatter + Markdown + preprocessing
   - Most similar syntax and approach

2. **🥈 Docassemble** - 4/5
   - Heavy YAML usage with field-based variables
   - Interview-based workflow (different use case)

3. **🥈 Accord Project Cicero** - 4/5
   - Markdown + variable interpolation
   - Uses `{{variable}}` syntax instead of `[Field: Name]`
   - Smart contract execution focus

4. **🥉 OpenLaw** - 3/5
   - Structured templates with `[[Variable: Type]]` syntax
   - Blockchain/Ethereum integration

5. **HotDocs** - 2/5
   - Commercial desktop application
   - `[VarName;type]` syntax
   - Word document-based

6. **Dot Legal Reference** - 2/5
   - URL-based clause library
   - Different paradigm (references vs. templates)

## Visual Style Comparison

### Legal-YAML (Current):
```markdown
---
label: Non-Disclosure Agreement
type: nda
---

```yaml
label: Parties and Purpose
uses:
    - field: issuer:company_name
    - field: recipient:name
```

This NDA is between [Issuer: Company Name] and [Recipient: Name].
```

### Legal Markdown (flotob) - Most Similar:
```markdown
---
title: Non-Disclosure Agreement
parties:
  - Party A
  - Party B
---

@if(CONFIDENTIAL_INFORMATION)
## Confidential Information
The Recipient shall keep all information confidential...
@endif

@include {{SignatureBlock}}
```

### Accord Project Cicero:
```markdown
This is a loan to the amount of {{loanAmount}} 
at the yearly interest rate of {{rate}}%.

{{#clause paymentClause}}
Payment terms...
{{/clause}}
```

### Docassemble:
```yaml
---
question: What is your name?
fields:
  - Name: client_name
---
attachment:
  - docx template file: contract.docx
```

### OpenLaw:
```
Agreement made on [[Effective Date: Date]] 
between [[Discloser Name]] and [[Recipient Name]].

{% if [[IncludeNonCompete: Boolean]] %}
Non-compete for [[Duration: Number]] years.
{% endif %}
```

## What Makes Legal-YAML Unique

1. **Embedded YAML blocks** for section-level metadata (not just frontmatter)
2. **Human-readable variables** using `[Field: Name]` syntax
3. **Tree-like versioning** with variant/revision model
4. **Option groups** for multiple section variants
5. **Template inheritance** system

## Web Resources Found

Additional similar approaches found during research:

1. **Legal Markdown JS** - https://github.com/petalo/legal-markdown-js
   - JavaScript implementation of legal markdown
   - YAML frontmatter + Markdown
   
2. **Markdown Reviewer (flotob)** - https://github.com/flotob/markdown-reviewer
   - Professional viewer for legal markdown
   - Law firm-inspired styling

3. **EasyLegalDocs Templates** - https://github.com/EasyLegalDocs/legal-templates
   - Free legal templates in Markdown
   - Uses `[square brackets]` for placeholders

## Recommendations

### For Legal-YAML Development:

Consider learning from:
- **Legal Markdown's** simplicity and preprocessing approach
- **Cicero's** clear `{{variable}}` syntax (widely recognized)
- **Docassemble's** structured field definitions
- **OpenLaw's** type system for variables

### For Users:

If looking for alternatives with similar style:
1. Try **Legal Markdown (flotob)** for simplest similar approach
2. Try **Docassemble** if you need interview workflows
3. Try **Accord Project Cicero** for smart contracts

## Links from the Original Issue

All links from the issue were researched:

- ✅ https://docassemble.org/ - Researched (Interview-based YAML legal automation)
- ✅ https://accordproject.org/projects/cicero/ - Researched (Markdown + smart contracts)
- ✅ https://github.com/flotob/legalmarkdown - Researched (Most similar!)
- ✅ https://technation.io/wp-content/uploads/2021/06/LegalSchemaFinal.pdf - Noted (Legal schema standard)
- ✅ https://github.com/dot-legal/reference - Researched (Clause library via URLs)

## Conclusion

Legal-YAML is most similar to **Legal Markdown (flotob)** but represents an evolution with:
- More structured metadata system (embedded YAML blocks)
- More sophisticated versioning
- Better template composition
- More explicit field definitions

This research shows that legal-yaml is building on proven approaches while adding unique features that make it more suitable for:
- LLM generation (structured YAML)
- Complex versioning scenarios (variant/revision)
- Template composition (inheritance)
- Section variants (option groups)

---

*Research Date: January 20, 2026*
