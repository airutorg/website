# CLAUDE.md - Operating Instructions for airut.org Website

## Project Overview

This is the public website for Airut, hosted on Cloudflare Pages at airut.org.

Currently a placeholder landing page. The site is static HTML/CSS with no build
step required.

## Project Structure

```
public/                 - Published files (Cloudflare Pages root)
  index.html            - Landing page
  assets/               - Logo and image assets
  _redirects            - Cloudflare Pages redirect rules
scripts/                - Utility scripts (not published)
  wait-for-preview      - Wait for Cloudflare Pages preview URL
CLAUDE.md               - This file (not published)
.airut/                 - Airut configuration (not published)
```

## Cloudflare Pages

This site is deployed via Cloudflare Pages:

- **Build command:** None (static site)
- **Build output directory:** `public`
- **Branch deployments:** `main` branch auto-deploys to production

No build tools or dependencies are needed. Just push HTML/CSS/JS files to
`public/`.

## CRITICAL: Always Create PRs

**After completing work that modifies files, create a PR immediately.** Only
skip if: (1) you need user input to finish the task, or (2) user explicitly asks
not to create a PR.

**The task is NOT complete until the PR is created and GitHub CI passes.** This
is the final step of every task, not an optional follow-up.

## Git and PR Workflow

**Before starting work:** Create a feature branch from latest main:

```bash
git fetch origin && git checkout -b feature/descriptive-name origin/main
```

**Standard workflow:**

1. Make changes, commit with clear message
2. Push and create PR:
   ```bash
   git push -u origin HEAD && gh pr create --fill
   ```
3. **Wait for Cloudflare Pages preview (for website changes):**

   If the PR includes changes to `public/`, wait for the Cloudflare Pages preview
   URL and report it back to the user:

   ```bash
   gh pr diff <PR_NUMBER> --name-only | grep -q "^public/" && scripts/wait-for-preview <PR_NUMBER>
   ```

   **Always include the preview URL in your response when available.**
4. Address review comments:
   ```bash
   gh pr view --comments
   ```
5. Merge (repo uses squash merge):
   ```bash
   gh pr merge --squash --delete-branch
   ```
6. Return to main:
   ```bash
   git checkout main && git pull
   ```

**If behind main:**

```bash
git fetch origin main && git rebase origin/main && git push --force-with-lease
```

**PR maintenance:**

- Before merging, rebase on main and squash commits into clean history
- After significant changes, update PR title/description:
  ```bash
  gh pr edit --title "..." --body "..."
  ```
- Multiple fix-up commits:
  ```bash
  git rebase -i origin/main && git push --force-with-lease
  ```

## Git Safety

- NEVER update git config
- NEVER run destructive commands (push --force, reset --hard, checkout .,
  restore ., clean -f, branch -D) unless explicitly requested
- NEVER skip hooks (--no-verify) unless explicitly requested
- NEVER force push to main/master
- Always create NEW commits rather than amending unless explicitly requested
- Stage specific files rather than using `git add -A` or `git add .`
- NEVER commit unless explicitly asked

## CRITICAL: Specs and User Intent Take Priority

**When you encounter issues that require deviating from user-supplied design,
stop and ask for guidance.** Do not prioritize "making things work" over
adhering to the user's intent.

## Development Guidelines

### Static Site Best Practices

- Keep HTML semantic and accessible
- Use CSS custom properties for theming
- Optimize images (SVG preferred for logos/icons)
- Test across browsers before committing

### Adding New Pages

1. Create new `.html` file in `public/`
2. Link from `index.html` if needed
3. Maintain consistent styling
