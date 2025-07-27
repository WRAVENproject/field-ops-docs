# GitHub & Git Cheat Sheet (WRAVEN Edition)

**Last updated: July 26, 2025**
**Maintained by: WRAVEN Threat Research Team**

> A quick-reference guide for Git and GitHub workflows, commands, and best practices. Ideal for CTF writeups, team collaboration, and keeping your code ops-ready.

---

## 🛠️ Getting Started

```bash
# Configure Git
git config --global user.name "Your Name"
git config --global user.email you@example.com

# Generate or add SSH key for GitHub
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
# Copy ~/.ssh/id_rsa.pub into GitHub -> Settings -> SSH and GPG keys
```

> 🔑 **Tip:** Use SSH for seamless pushes, HTTPS if SSH is blocked.

---

## 📂 Repository Setup

| Task                  | Command / UI Path                                         |
| --------------------- | --------------------------------------------------------- |
| Clone a repo          | `git clone git@github.com:Org/Repo.git`                   |
| Create new repo       | GitHub → New repository → Fill name, description, privacy |
| Initialize local repo | `git init` then add remote: `git remote add origin URL`   |
| Add & commit changes  | `git add .` → `git commit -m "Message"`                   |
| Push to remote        | `git push -u origin main`                                 |

> 🚀 **Advice:** Commit early, commit often—small commits are easier to review.

---

## 🔀 Branching & Merging

```bash
# Create and switch to branch
git checkout -b feature/awesome

# Switch branch
git checkout main

# Merge branch into main
git checkout main
git merge feature/awesome
```

* **Branch naming:** `feature/*`, `bugfix/*`, `hotfix/*`
* **Delete branch:** `git branch -d feature/awesome` or GitHub UI

> 🌿 **Best Practice:** Rebase local changes before opening PR: `git pull --rebase origin main`.

---

## 🔄 Pull Requests (PRs)

1. Push branch to GitHub: `git push origin feature/awesome`
2. On GitHub, click “Compare & pull request”
3. Add title, description, link issues, assign reviewers
4. Respond to review comments, push updates to same branch
5. Merge when approved (Squash & merge or Rebase & merge)

> 📝 **PR Tip:** Keep PRs focused on one change. Reference related issues: `Fixes #123`.

---

## 🐛 Issues & Labels

* **Create issue:** GitHub → Issues → New issue
* **Link PR to issue:** include `Closes #123` in PR description
* **Use labels:** `bug`, `enhancement`, `question` to organize
* **Assign & milestones:** track assignees and target releases

> 📋 **Advice:** Fill out issue templates if provided—gives all needed info.

---

## ⚙️ GitHub Actions & CI/CD

| Workflow File | Path                           | Purpose                         |
| ------------- | ------------------------------ | ------------------------------- |
| Test & Build  | `.github/workflows/test.yml`   | Run tests on push/PR            |
| Linting       | `.github/workflows/lint.yml`   | Code style checks               |
| Deploy        | `.github/workflows/deploy.yml` | Deploy to production or staging |

```yaml
# Example: simple Node CI
name: CI
on: [push, pull_request]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with: node-version: '16'
      - run: npm install
      - run: npm test
```

> ⚙️ **Tip:** Use `actions/cache` to speed up builds by caching dependencies.

---

## 🔐 Security & Permissions

* **Branch protection:** require PR reviews, status checks before merge
* **Secrets:** GitHub Settings → Secrets → Actions for CI secrets
* **Code owners:** `.github/CODEOWNERS` to auto-assign reviewers
* **Dependabot:** enable for automatic security updates

> 🔒 **Advice:** Never commit credentials. Use secrets and environment variables.

---

## 🌐 Collaboration & Projects

* **Projects (Kanban):** track tasks with boards
* **Wiki:** documentation in repo’s Wiki tab
* **Discussions:** for community brainstorming and Q\&A
* **Milestones:** group issues/PRs by release targets

> 🤝 **Workflow Tip:** Use project boards to visualize sprint scope and status.

---

## 💡 Tips & Best Practices

* **Squash & Merge:** keeps history clean for feature branches
* **Semantic commits:** `feat:`, `fix:`, `chore:` for clarity
* **Draft PRs:** create WIP PRs early for feedback
* **Templates:** `.github/ISSUE_TEMPLATE` & `PULL_REQUEST_TEMPLATE` improve consistency

> 🚀 **Pro Tip:** Automate labeling with Actions (e.g., label PRs by type).

---

**WRAVEN Reminder:** GitHub is more than code-it’s collaboration. Keep your workflows consistent and your history clear.
**Repo:** [github.com/WRAVENproject/field-ops-docs](https://github.com/WRAVENproject/field-ops-docs)

---

**Made for the field. Built by WRAVEN.**
