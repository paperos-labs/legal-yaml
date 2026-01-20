# Accuracy Verification Report for DETAILED_EXAMPLES.md

This document details the verification process and corrections made to ensure accuracy of the examples in DETAILED_EXAMPLES.md.

## Verification Process

Each example was cross-referenced against official documentation and real-world examples from the respective projects.

## Corrections Made

### 1. Legal Markdown (flotob)

**Issues Found:**
- ❌ Used `@if/@else/@endif` syntax - **NOT SUPPORTED**
- ❌ Used `@foreach` loop syntax - **NOT SUPPORTED** 
- ❌ Incorrectly represented conditional logic

**Corrections Applied:**
- ✅ Changed to correct optional clause syntax: `[{{condition}}text]`
- ✅ Removed `@foreach` - Legal Markdown handles lists through YAML field definitions
- ✅ Added note explaining that square brackets with mixins are used for optional clauses
- ✅ Updated YAML frontmatter to use separate boolean fields for each optional section

**Source:** https://github.com/flotob/legalmarkdown - Official README documentation

**Correct Syntax:**
- Variables: `{{variable_name}}`
- Optional clauses: `[{{mixin_name}}Text here]` with `mixin_name: true/false` in YAML
- Imports: `@import filename`

### 2. Accord Project Cicero (CiceroMark)

**Issues Found:**
- ❌ Used `{{#if}}...{{else}}...{{/if}}` conditionals in template - **NOT SUPPORTED**
- ❌ Used `{{#ulist}}` for list iteration - **NOT DOCUMENTED**

**Corrections Applied:**
- ✅ Removed conditional blocks from template
- ✅ Changed to use simple variable placeholders
- ✅ Added note explaining that conditional logic must be handled in Ergo logic layer, not in CiceroMark template
- ✅ Simplified to show that variables are populated by logic, not evaluated in template

**Source:** 
- https://docs.accordproject.org/docs/markup-cicero.html
- Web search results confirming CiceroMark does not support if/else blocks in templates

**Correct Syntax:**
- Variables: `{{variableName}}`
- Clause blocks: `{{#clause clauseName}}...{{/clause}}`
- Computed values: `{{% expressionInErgo %}}`
- **NO** `{{#if}}` support - handle conditionals in Ergo logic

### 3. Docassemble

**Issues Found:**
- ✅ Syntax was CORRECT - no changes needed

**Verified:**
- ✅ Mako syntax for Markdown templates: `% if condition:` and `% endif`
- ✅ Variable interpolation: `${ variable }`
- ✅ Python expressions: `${ '4' if condition else '3' }`
- ✅ For loops: `%for item in list:` and `%endfor`

**Source:** 
- https://docassemble.org/docs/documents.html
- Multiple community guides on Docassemble templating

### 4. OpenLaw

**Issues Found:**
- ❌ Used incorrect conditional syntax: `{{#if [[Variable]] = "value"}}`

**Corrections Applied:**
- ✅ Changed to correct function syntax: `{{#if (equals [[Variable]] "value")}}`
- ✅ For boolean variables, simplified to: `{{#if [[Boolean Variable]]}}`

**Source:**
- https://docs.openlaw.io/markup-language/
- Web search results on OpenLaw conditional expressions

**Correct Syntax:**
- Variables: `[[Variable Name]]` or `[[Variable Name: Type]]`
- Conditionals: `{{#if condition}}...{{else}}...{{/if}}`
- Functions: `(equals [[var]] "value")`, `(and condition1 condition2)`, `(or condition1 condition2)`

## Summary of Accuracy Issues

| Solution | Major Issues | Status |
|----------|-------------|--------|
| Legal Markdown | Invented syntax (@if/@foreach) | ✅ FIXED |
| Accord Project Cicero | Used unsupported {{#if}} blocks | ✅ FIXED |
| Docassemble | No issues found | ✅ VERIFIED |
| OpenLaw | Incorrect conditional syntax | ✅ FIXED |

## Key Lessons

1. **Legal Markdown** uses square brackets `[{{mixin}}text]` for optional content, NOT preprocessor directives like `@if`
2. **CiceroMark** does NOT support conditionals in templates - all logic must be in Ergo code
3. **Docassemble** uses different syntax for Markdown (Mako) vs DOCX (Jinja2) templates
4. **OpenLaw** requires function calls for comparisons: `(equals [[var]] "value")` not `[[var]] = "value"`

## Verification Sources

All corrections were based on:
- Official project documentation
- GitHub repository README files
- Community guides and tutorials
- Web search results cross-referencing multiple sources

No syntax was "guessed" - all examples now reflect actual documented behavior of each system.

---

*Verification completed: January 20, 2026*
