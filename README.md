# Auto-Tagging Project

This project includes a GitHub Action that automatically creates semantic version tags when new commits are pushed to the main/master branch.

## How the Auto-Tagging Works

The GitHub Action (`.github/workflows/auto-tag.yml`) automatically:

1. **Triggers on push** to `main` or `master` branches
2. **Analyzes commit messages** to determine the type of version bump:
   - **Major version** (x.0.0): Commits with `!` suffix or `BREAKING CHANGE:` in message
   - **Minor version** (x.y.0): Commits starting with `feat:` or `feature:`
   - **Patch version** (x.y.z): Commits starting with `fix:` or `bugfix:`, or any other commits
3. **Creates a new tag** following semantic versioning (semver)
4. **Creates a GitHub release** with the new tag

## Commit Message Examples

To trigger different version bumps, use these commit message formats:

```bash
# Patch version bump (1.0.0 → 1.0.1)
git commit -m "fix: resolve login issue"
git commit -m "docs: update README"
git commit -m "chore: update dependencies"

# Minor version bump (1.0.0 → 1.1.0)
git commit -m "feat: add user authentication"
git commit -m "feature: implement dark mode"

# Major version bump (1.0.0 → 2.0.0)
git commit -m "feat!: redesign API endpoints"
git commit -m "fix!: remove deprecated methods"
git commit -m "feat: add new feature

BREAKING CHANGE: This changes the API structure"
```

## First Tag

If no tags exist in the repository, the workflow will start with `v0.0.1` for the first commit.

## Requirements

- The workflow uses `GITHUB_TOKEN` which is automatically provided by GitHub Actions
- No additional setup or secrets are required
- The workflow runs on Ubuntu latest
