---
name: write-docs
description: Review and edit documentation, READMEs, guides, or technical prose. Use when writing, reviewing, or improving docs.
argument-hint: "[file path or paste content]"
allowed-tools:
    - WebFetch
---

# Writing Documentation

Read the full document first. Note purpose, audience, structure, and whether links or citations are present.

## Review

Launch both agents concurrently. Pass each the full document content.

### Agent 1: Prose & Structure Review

Apply these principles:

**Prose:**

- **State each fact once.** If a phrase implies something, don't state the
  implication separately.
- **Cut, then cut again.** If removing a sentence loses nothing, remove it.
- **Prefer plain framing over jargon.** "No config changes needed" over
  "existing parametric configuration is preserved."
- **Use active voice.** "Draft 5 clarifies the spec" not "The spec is clarified
  by Draft 5."
- **Be concrete.** "Adds three keywords" not "includes several new features."
- **Omit filler.** "To migrate" not "In order to migrate, you will need to."
- **Keep modifiers close.** "Can access only owned files" not "can only access
  owned files."
- **Use parallel structure.** List items and headings follow the same grammatical
  pattern.
- **Intros must not restate the heading.** Start with the first fact.

**Structure:**

- **Lead with the point.** Essential information first. Readers skim.
- **Progress from simple to complex.** Common cases first, edge cases later.
- **Headings enable skipping.** Readers find what they need without reading
  everything before it.
- **Headings need context.** A bare term (`id → $id`) doesn't orient readers.
  Add the domain (`Schema Identification: id → $id`). Words before code.
- **Tables beat repetition.** When comparing items across the same dimensions,
  use a table.
- **Bullets for lists, prose for flow.** Bullets suit independent items.
  Sentences suit connected ideas.
- **Include surrounding structure.** Readers need enough context to understand
  where something belongs.
- **Multiple cases prevent confusion.** If one case might mislead about scope,
  add another.

**Formatting:**

- **Restrain markup.** Overused bold loses impact. Reserve it for defined terms.
- **Prefer plain symbols.** Use `✓` and `✗` over emoji.
- **Reference-style links.** Place link definitions immediately after their
  section, not at the document bottom.
- **Consistent terminology.** One term per concept throughout.

### Agent 2: Link & Citation Review

Skip this agent if the document contains no links or citations.

Fetch every link. Verify at test time; do not assume URLs work.

- Check that the page loads (not 404, 403, ECONNREFUSED)
- Check that anchors resolve to the claimed section
- Check that the content matches the citation's claim

For broken links, find the canonical or closest equivalent. Prefer, in order:

1. The same resource at a new URL (moved, not removed)
2. A primary source covering the same claim (RFC, CVE, original paper)
3. A widely-maintained secondary source (OWASP, PayloadsAllTheThings)

Include citation text in link titles so context survives URL rot:
`[label]: https://example.com "Author, 'Title' (Year)"`

Review information value — every link should teach the reader something the
prose does not:

- Drop or replace links to generic pages that teach nothing about the cited
  concept.
- Keep spec links (RFCs, CWEs) when implementers need exact wording.
- Verify the claim matches the source. A CVE about X cited for a claim about Y
  is misleading. Find a source for the actual claim, or rewrite the prose.
- Citations as filler: "This is well-documented [link]" adds nothing — either
  the prose explains it or the citation does. Pick one.
- Claims need specifics. "Has been used in real-world attacks" is vague. Name the
  incident, CVE, or technique, or drop the claim.

## Fix Issues

Aggregate findings from both agents. Fix each issue; skip false positives.

Summarize what was fixed, or confirm the document was clean.
