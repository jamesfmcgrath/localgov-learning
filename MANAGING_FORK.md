# Managing Your LocalGov Drupal Fork

This repository is a fork of the upstream LocalGov Drupal project. This document explains how to manage your fork and stay synchronized with upstream changes.

## Repository Setup

This is your personal fork where you can:

- Make customizations and experiments
- Track your own changes (including the `LGD_DEMO/` directory)
- Pull in updates from the main LocalGov Drupal project when needed

### Remote Configuration

Your repository should have two remotes configured:

- **`origin`**: Your GitHub fork (localgovdrupal/localgov)
- **`upstream`**: The main LocalGov Drupal repository

To verify your remotes:

```bash
git remote -v
```

If you need to add the upstream remote:

```bash
git remote add upstream https://github.com/localgovdrupal/localgov.git
```

## Staying Up to Date with LocalGov (Upstream)

### Step 1: Prepare Your Local Branch

Make sure you're on your main working branch:

```bash
# Check current branch
git branch

# Switch to your main branch (usually 'main' or '3.x')
git checkout main
```

### Step 2: Fetch Latest Changes from Upstream

```bash
git fetch upstream
```

### Step 3: Identify the Upstream Branch

Check which branches exist in the upstream repository:

```bash
git branch -r
```

Look for entries like `upstream/3.x` or `upstream/main` to identify the primary upstream branch.

### Step 4: Merge Upstream Changes

Merge the appropriate upstream branch into your local branch:

```bash
# If upstream uses the 3.x branch:
git merge upstream/3.x

# Or if upstream uses main:
git merge upstream/main
```

### Step 5: Resolve Conflicts (if any)

If there are merge conflicts, Git will notify you. Resolve them manually, then:

```bash
git add .
git commit -m "Merge upstream changes and resolve conflicts"
```

### Step 6: Update Dependencies and Database

After merging upstream changes:

```bash
# Update Composer dependencies (if composer.lock changed)
composer install

# Optional: Update database and configuration (if using Drush)
# drush updb -y
# drush cim -y
```

### Step 7: Push to Your Fork

Push the merged changes to your GitHub repository:

```bash
git push origin main
```

## Workflow Summary

### Your Regular Work

1. Make changes to your codebase (including `LGD_DEMO/`)
2. Commit changes: `git add . && git commit -m "Your message"`
3. Push to your fork: `git push origin main`

### Pulling Upstream Updates

1. Fetch upstream: `git fetch upstream`
2. Check branches: `git branch -r`
3. Merge upstream: `git merge upstream/<branch-name>`
4. Update dependencies: `composer install`
5. Push to your fork: `git push origin main`

## Tips and Best Practices

### Before Merging Upstream

- **Commit your work**: Always commit or stash your local changes before merging upstream
- **Check status**: Run `git status` to ensure you have a clean working directory

### Handling Conflicts

- Conflicts often occur in `composer.lock` or configuration files
- For `composer.lock`: Accept upstream version, then run `composer update` to regenerate
- For custom changes: Carefully review conflicts to preserve your modifications

### Staying Organized

- **Create feature branches**: For experimental work, create separate branches:
  ```bash
  git checkout -b feature/my-experiment
  ```
- **Merge carefully**: Review the changes being merged with `git log upstream/3.x..HEAD`

### Troubleshooting

If you need help identifying which upstream branch to use, run:

```bash
git branch -r
```

Then look for the primary upstream branch (typically `upstream/3.x` or `upstream/main`).

## Need Help?

If you're unsure which upstream branch to merge, paste the output of `git branch -r` and someone can help identify the correct branch name to use in your merge command.

---

**Last Updated**: November 2025
