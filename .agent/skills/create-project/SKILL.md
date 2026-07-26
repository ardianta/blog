# Skill: Create Portfolio Project (`create-project`)

Use this skill to create showcase items or portfolio project entries in `content/project/`.

## Workflow & Steps

1. **File Location**:
   `content/project/<project-slug>.md`

2. **YAML Frontmatter Template**:
   ```yaml
   ---
   title: "Nama Project / Application"
   slug: project-slug
   date: YYYY-MM-DDTHH:MM:SS+08:00
   draft: false
   type: project
   tags:
       - Portfolio
       - Web Development
       - Open Source
   image: "/img/projects/project-slug-cover.webp"
   description: "Deskripsi singkat mengenai projek dan dampaknya."
   demo_url: "https://example.com"
   repo_url: "https://github.com/ardianta/repo"
   ---
   ```

3. **Content Structure**:
   - **Overview**: What the project does, background, problem solved.
   - **Features**: Bulleted list of key features.
   - **Tech Stack**: Frontend, Backend, Tools used.
   - **Screenshots / Visuals**: Embedded WebP images.
   - **Installation / Usage**: Quick start guide if applicable.

4. **Validation**:
   - Verify links (demo_url, repo_url).
   - Test build with `hugo --gc`.
