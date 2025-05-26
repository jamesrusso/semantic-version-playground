# 🧪 Semantic Release Starter Repo

Welcome to the **Semantic Release Starter** project! This repo uses [semantic-release](https://semantic-release.gitbook.io/) for fully automated versioning and changelog management, following the [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) standard.

It supports:

* ✅ Automated version bumps and GitHub releases
* ✅ Pre-releases from `next` branch
* ✅ Production releases from `main` branch
* ✅ GitHub Actions-based CI
* ✅ Developer tooling with Husky + Commitlint

---

## 🏗️ Project Structure

* `main` — production branch → stable releases (e.g. `1.2.3`)
* `next` — staging/QA branch → pre-releases (e.g. `1.3.0-next.1`)
* `feature/*` — developer feature branches → merged into `next`
* `.github/workflows/release.yml` — triggers release pipeline
* `.releaserc.json` — semantic-release configuration

---

## 🛠 Developer Workflow

### 1. Create a Feature Branch

```bash
git checkout next
git pull origin next
git checkout -b feature/your-feature-name
```

### 2. Make Commits Using Conventional Commits

Example:

```bash
git commit -m "feat: add support for dark mode"
```

### 3. Push and Open PR into `next`

```bash
git push -u origin feature/your-feature-name
```

* Use `Squash & Merge` if needed
* After merge, `semantic-release` will create a `next` pre-release (e.g. `1.3.0-next.2`)

---

## 🚀 Releasing to Production

### 1. Open a Pull Request from `next` to `main`

* Use the **Release PR Template**
* Review commit history to confirm Conventional Commit compliance

### 2. Merge into `main`

* Use **Merge Commit** to preserve version history, or
* Use **Squash Merge** with a message like:

  ```
  chore(release): v1.3.0
  ```

### 3. GitHub Actions will:

* Run semantic-release on `main`
* Create a new release (e.g. `1.3.0`)
* Publish changelog

---

## ✍️ Conventional Commit Examples

| Type    | Purpose                    |
| ------- | -------------------------- |
| `feat`  | New feature                |
| `fix`   | Bug fix                    |
| `chore` | Tooling, refactor, cleanup |
| `docs`  | Documentation changes      |
| `test`  | Test changes               |

Example:

```bash
git commit -m "fix(login): correct password hash logic"
```

To indicate a breaking change:

```bash
git commit -m "feat!: drop support for legacy browsers"
```

---

## 🧹 Maintenance & Sync

After a production release:

```bash
git checkout next
git pull origin main
# Keep `next` up to date with `main`
```

---

## 📂 Important Files

| File                    | Purpose                                     |
| ----------------------- | ------------------------------------------- |
| `.releaserc.json`       | Semantic release configuration              |
| `.github/workflows`     | GitHub Actions CI configs                   |
| `.husky/commit-msg`     | Commitlint check hook                       |
| `commitlint.config.cjs` | Conventional Commit rules config (CommonJS) |
| `version.js`            | Holds current version for in-app use        |

---

## 🤖 Manual Release (if needed)

You can trigger a release manually for testing:

```bash
GITHUB_TOKEN=your_token npx semantic-release --no-ci
```

> Normally, semantic-release is triggered automatically by GitHub Actions on push to `main` or `next`.

---

## 👥 Contributors Guide

* Follow Conventional Commit rules
* Create clean PRs with clear commit messages
* Use the provided PR templates for feature vs release merges

---

For questions, contact the repo maintainer or check the [semantic-release documentation](https://semantic-release.gitbook.io/).
