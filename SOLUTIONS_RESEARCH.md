# Legal Template Solutions Research

Context summary for comparing legal-yaml with existing solutions.

## Solutions Analyzed

1. Legal Markdown (flotob) - https://github.com/flotob/legalmarkdown
2. Accord Project Cicero - https://github.com/accordproject/cicero
3. Docassemble - https://docassemble.org/
4. OpenLaw - https://www.openlaw.io/
5. HotDocs - Commercial GUI-based system
6. Dot Legal Reference - URL-based clause library

## Most Similar: Legal Markdown (flotob)

Legal-YAML most closely resembles Legal Markdown with key differences:
- Both: YAML frontmatter, Markdown prose, plain text
- Legal Markdown: Optional clauses via `[{{condition}}text]` syntax
- Legal-YAML adds: Embedded YAML blocks per section, variant/option system, template inheritance, tree-like versioning

## Key Syntax Differences

**Legal Markdown**: `[{{optional_clause}}text]` for conditionals, `{{variable}}` for variables
**Accord Project Cicero**: `{{variable}}` for variables, `{{#clause name}}` for sections, no template conditionals (handled in Ergo logic)
**Docassemble**: Separate interview YAML + template, Mako syntax (`% if`, `${ var }`)
**OpenLaw**: `[[Variable: Type]]` for variables, `{{#if (equals [[var]] "value")}}` for conditionals

## Detailed Examples

See DETAILED_EXAMPLES.md for complete NDA examples with verified syntax for Legal Markdown, Accord Project Cicero, Docassemble, and OpenLaw. HotDocs and Dot Legal Reference excluded as not comparable (GUI-based and URL-reference paradigms respectively).
