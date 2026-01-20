# Legal Template Solutions Research

Research into existing legal document template systems to compare with legal-yaml's approach.

## Research Summary

Analyzed 6 existing solutions for legal document templates:

1. **Legal Markdown (flotob)** - https://github.com/flotob/legalmarkdown
2. **Accord Project Cicero** - https://accordproject.org/projects/cicero/
3. **Docassemble** - https://docassemble.org/
4. **OpenLaw** - https://www.openlaw.io/
5. **HotDocs** - https://www.hotdocs.com/ (commercial)
6. **Dot Legal Reference** - https://github.com/dot-legal/reference

## Key Finding

**Legal Markdown (flotob)** is the most similar solution to legal-yaml:
- YAML frontmatter for document metadata
- Markdown for legal prose
- Preprocessor directives (`@include`, `@if`)
- Plain text, git-friendly
- Supports conditionals and loops

**Legal-YAML's unique features** (evolution beyond Legal Markdown):
- Embedded YAML blocks for section-level metadata (not just frontmatter)
- Structured variant/option system for multiple versions
- Template inheritance (`from:`, `replaces:`, `provides:`)
- Tree-like versioning (variant + revision instead of semver)
- Human-readable variable syntax: `[Field: Name]`

## Similarity Scoring

1. 🥇 **Legal Markdown (flotob)** - ⭐⭐⭐⭐⭐ (5/5)
   - YAML frontmatter + Markdown + preprocessing
   
2. 🥈 **Docassemble** - ⭐⭐⭐⭐ (4/5)
   - YAML-heavy, field-based variables, interview workflow
   
3. 🥈 **Accord Project Cicero** - ⭐⭐⭐⭐ (4/5)
   - Markdown + `{{variables}}`, smart contracts
   
4. 🥉 **OpenLaw** - ⭐⭐⭐ (3/5)
   - `[[Variable: Type]]` syntax, blockchain integration
   
5. **HotDocs** - ⭐⭐ (2/5)
   - Proprietary GUI-based Word system
   
6. **Dot Legal Reference** - ⭐⭐ (2/5)
   - URL-based clause library, different paradigm

## Solutions with Detailed Examples

See [DETAILED_EXAMPLES.md](DETAILED_EXAMPLES.md) for complete NDA examples demonstrating:

**✅ Comparable solutions** (detailed examples created):
1. Legal Markdown (flotob)
2. Accord Project Cicero
3. Docassemble
4. OpenLaw

**❌ Not comparable** (marked off due to different paradigm):
5. HotDocs - GUI-based desktop application
6. Dot Legal Reference - URL reference system, not templates

## Syntax Quick Reference

### Legal-YAML
```markdown
---
label: Non-Disclosure Agreement
type: nda
---
```yaml
label: Parties and Purpose
uses:
    - field: issuer:company_name
```
Agreement between [Issuer: Company Name] and [Recipient: Name].
```

### Legal Markdown (most similar)
```markdown
---
title: Non-Disclosure Agreement
issuer_company_name: "[ISSUER]"
---
Agreement between {{issuer_company_name}} and {{recipient_name}}.

@if(condition)
...
@endif
```

### Accord Project Cicero
```markdown
Agreement for {{loanAmount}} at {{rate}}%.

{{#clause payment}}
...
{{/clause}}
```

### Docassemble
```yaml
---
question: What is your name?
fields:
  - Name: client_name
---
attachment:
  - docx template file: contract.docx
```

### OpenLaw
```
Agreement on [[Effective Date: Date]] between [[Party A]] and [[Party B]].

{{#if [[condition]]}}
...
{{/if}}
```

## References

- Legal Markdown: https://github.com/flotob/legalmarkdown
- Accord Project: https://docs.accordproject.org/docs/markup-cicero.html
- Docassemble: https://docassemble.org/docs/overview.html
- OpenLaw: https://docs.openlaw.io/markup-language/
- HotDocs: https://help.hotdocs.com/
- Dot Legal: https://github.com/dot-legal/reference

---

*Research completed: January 2026*
