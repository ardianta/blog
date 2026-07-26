# Skill: Hugo Build & Site Audit (`hugo-build-audit`)

Use this skill to validate the integrity of the Hugo site, verify template syntax, check frontmatter correctness, and identify broken image references or missing pages.

## Actions & Steps

1. **Run Hugo Build Check**:
   Execute shell command in terminal:
   ```bash
   hugo --gc --minify
   ```
   - Watch for syntax errors, missing layouts, broken shortcodes, or template rendering failures.

2. **Draft & Future Post Audit**:
   To inspect all draft posts or future-dated posts:
   ```bash
   hugo list drafts
   hugo list future
   ```

3. **Image & Link Verification**:
   - Check if images referenced in frontmatter (`image: "/img/..."`) or body markdown exist inside `static/img/`.
   - Ensure image paths start with `/img/` and not relative paths like `../../img/`.

4. **Frontmatter Integrity**:
   - Confirm all posts under `content/post/` have `title`, `slug`, `date`, `tags`, and `description`.
   - Ensure dates are properly formatted ISO-8601 strings.

5. **Reporting**:
   - Summarize build outputs, list any warnings or errors encountered, and fix any reported issues.
