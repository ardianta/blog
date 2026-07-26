# Skill: Manage Blog Images (`manage-images`)

Use this skill when adding, moving, optimizing, or referencing images in blog posts and pages.

## Image Storage Architecture

- **Root Image Folder**: All static images belong in `static/img/`.
- **Hugo Asset Resolution**: Files placed in `static/img/photo.webp` are accessed at `/img/photo.webp` in Markdown and HTML.
- **Recommended Folder Structure**:
  Group post images into subdirectories matching the post slug:
  ```
  static/img/
  └── <post-slug>/
      ├── cover.webp
      ├── diagram-01.webp
      └── screenshot-02.webp
  ```

## Image Rules & Best Practices

1. **Format Preference**: Use `.webp` for optimal compression and web performance.
2. **Naming Convention**: Use lowercase kebab-case (e.g. `install-step-1.webp`). Avoid spaces or special characters.
3. **Markdown Syntax**:
   ```markdown
   ![Alt text deskriptif](/img/<post-slug>/gambar.webp)
   ```
4. **Frontmatter Image Reference**:
   ```yaml
   image: "/img/<post-slug>/cover.webp"
   ```
