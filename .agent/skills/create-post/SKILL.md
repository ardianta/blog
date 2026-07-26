# Skill: Create Blog Post (`create-post`)

Use this skill whenever you need to create a new blog article in `content/post/`.

## Workflow & Steps

1. **Gather Article Details**:
   - Title / Subject of the post
   - Slug (kebab-case, e.g. `belajar-hugo-agent`)
   - Target Tags (e.g. `Hugo`, `Tutorial`, `Linux`)
   - Short summary/description for SEO

2. **Generate Post File**:
   - Location: `content/post/<slug>.md`
   - Set YAML Frontmatter:
     ```yaml
     ---
     title: "Judul Artikel"
     slug: slug-artikel
     date: YYYY-MM-DDTHH:MM:SS+08:00
     draft: false
     type: post
     tags:
         - Tag1
         - Tag2
     image: "/img/slug-artikel/cover.webp"
     description: "Deskripsi singkat mengenai artikel ini..."
     ---
     ```

3. **Content Structure Rules**:
   - **Introduction**: Brief context about why this topic is relevant.
   - **Main Body**: Break down into clear `## Heading 2` sections.
   - **Code Examples**: Always specify language identifier (`bash`, `javascript`, `go`, etc.).
   - **Images**: Reference as `![Alt Text](/img/slug-artikel/nama-gambar.webp)`.
   - **Conclusion / Summary**: Wrap up key takeaways.

4. **Validation Checklist**:
   - [ ] Frontmatter YAML is valid and enclosed by `---`.
   - [ ] `slug` matches filename (without `.md`).
   - [ ] `draft` is set appropriately (`false` if publishing immediately).
   - [ ] No `H1` (`#`) used in article body (only `##` and `###`).
   - [ ] Tested build with `hugo --gc`.
