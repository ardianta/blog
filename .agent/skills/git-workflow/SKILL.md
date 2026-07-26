# Skill: Git Workflow & Commit Standards (`git-workflow`)

Use this skill when staging, committing, or pushing changes in this repository.

## Conventional Commits Guideline

Use conventional commit types and clear scope:

- `feat(post): add article about <topic>`
- `feat(project): add new portfolio project <name>`
- `fix(theme): fix layout alignment on mobile`
- `style(theme): update CSS colors and typography`
- `docs: update AGENTS.md or README.md`
- `chore: update hugo dependencies or configuration`

## Rules before committing

1. Run site build check:
   ```bash
   hugo --gc
   ```
2. Verify git status and check modified files:
   ```bash
   git status
   ```
3. Stage relevant files explicitly (avoid blindly committing `public/` folder if generated during local testing unless deployment branch requires it). Check `.gitignore`.
