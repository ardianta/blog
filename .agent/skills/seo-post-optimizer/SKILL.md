# Skill: SEO & Content Optimizer (`seo-post-optimizer`)

Use this skill to audit and optimize individual articles or site content for search engine performance, accessibility, and readability.

## Audit Criteria

1. **Title Tag & H1**:
   - Title should be concise, descriptive, and under 60 characters where possible.
   - Post title is generated as H1 by the layout. Ensure no `<h1>` headers are written inside the Markdown content body.

2. **Meta Description**:
   - Every post MUST have a `description` in YAML frontmatter.
   - Recommended length: 120 - 160 characters.
   - Must summarize the core takeaway of the article.

3. **Heading Hierarchy**:
   - Standard sequence: `H2` (`##`) -> `H3` (`###`) -> `H4` (`####`).
   - Do not skip levels (e.g. going directly from `##` to `####`).

4. **Image Optimization**:
   - All images MUST have descriptive alt text (`![Deskripsi Gambar](/img/...)`).
   - Image format should preferably be WebP.
   - Ensure cover image is declared in `image:` frontmatter.

5. **Taxonomy & Tags**:
   - Assign 2-5 relevant, existing tags.
   - Maintain consistent casing for tags (e.g. `Linux`, `Hugo`, `JavaScript`).

6. **URL Slug**:
   - Clean, readable kebab-case (e.g., `cara-install-hugo`).
   - Avoid special characters or date prefixes in slug unless required.
