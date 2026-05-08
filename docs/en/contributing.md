---
title: "Contributing Guide"
lang: en
version: "1.0"
---

<div align="right">
  <a href="../zh-CN/contributing.md">🇨🇳 中文</a> |
  <strong>🇺🇸 English</strong>
</div>

# 🤝 Contributing Guide

> Thank you for contributing to the Hermes Windows Native Guide!

---

## 📋 How to Contribute

| Method | When to Use | Difficulty |
|--------|-------------|------------|
| 🐛 Report a Bug | Documentation errors / broken links | ⭐ |
| ✨ Request a Feature | Suggest new content or improvements | ⭐ |
| 📝 Translate | Chinese-English translation | ⭐⭐ |
| ✏️ Fix Documentation | Directly resolve an issue | ⭐⭐ |
| 🖼️ Provide Screenshots | Add operation screenshots / GIFs | ⭐⭐ |

---

## 🔧 Development Environment Setup

### Clone the Repository

```powershell
git clone https://github.com/markwang2658/hermes-windows-native-guide.git
cd hermes-windows-native-guide
```

### Configure Git Proxy (for users in mainland China)

```powershell
git config http.proxy http://127.0.0.1:10808
git config https.proxy http://127.0.0.1:10808

# Verify
git config --get http.proxy
# Expected output: http://127.0.0.1:10808

# Test connection
git ls-remote --heads https://github.com/markwang2658/hermes-windows-native-guide.git
# Should return refs/heads/main
```

### Remove Proxy (if needed)

```powershell
git config --unset http.proxy
git config --unset https.proxy
```

---

## 📝 Commit Convention

### Format Requirements

Follow the **Conventional Commits** format:

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Type Values

| Type | Description | Example |
|------|-------------|---------|
| `docs` | Documentation addition or modification | `docs: add chat configuration guide` |
| `fix` | Bug fix | `fix: broken link in troubleshooting` |
| `style` | Formatting adjustment (no content change) | `style: adjust table alignment` |
| `i18n` | Internationalization update | `i18n: update English translation for vision-config` |
| `chore` | Engineering file updates | `chore: add .gitignore rules for venv` |

### Scope (Optional)

| Scope | Description |
|-------|-------------|
| `readme` | README.md / README.zh-CN.md |
| `installation` | Installation guide |
| `configuration` | Configuration guide (chat/vision/audio/text) |
| `architecture` | Architecture design |
| `troubleshooting` | Troubleshooting |
| `examples` | Configuration example files |
| `assets` | Screenshots / resource files |

### Subject Rules

- Use **English** (consistent with document language)
- No more than 50 characters
- Do not end with a period
- Use imperative mood (not past tense)

**✅ Correct Examples**:
```
docs(chat-config): add Kimi K2.6 API Key expiration handling notes
fix(troubleshooting): correct proxy port number in connection-issues.md
i18n(vision-config): update English LM Studio installation steps
```

**❌ Incorrect Examples**:
```
update some files
fixed bug
modified some stuff
```

### Body (Optional but Recommended)

```markdown
docs(chat-config): add Kimi K2.6 API Key expiration handling notes

## Changes
- Added "API Key expired" FAQ entry
- Updated cost control section with free tier information
- Corrected model list entry from kimi-k2.0711-preview to kimi-k2.6

## Related Issue
Closes #12
```

---

## ✅ Pre-Submission Checklist

### Content Quality (All Must Pass)

- [ ] All `.md` file contents reviewed, no sensitive information exposed
- [ ] Bidirectional links work (`zh-CN <-> en` language toggle functional)
- [ ] New content does not conflict with existing documentation
- [ ] PowerShell commands are copy-paste ready (tested)

### Format Standards (All Must Pass)

- [ ] Front Matter includes `title` / `lang` / `version`
- [ ] Each page has language switch button at the top (🇨🇳 / 🇺🇸)
- [ ] Tables properly formatted (aligned, no overflow)
- [ ] Code blocks annotated with language (`powershell` / `yaml` / `bash`)

### Example File Safety (If Applicable)

- [ ] `examples/.env.example` contains no real keys (use placeholders)
- [ ] `examples/config.yaml.example` has sufficient comments
- [ ] If screenshots included, sanitized (no API Key / personal paths / IP addresses)

### Link Validation (All Must Pass)

- [ ] Internal links (`../xxx.md`) point to correct files
- [ ] External links (GitHub Issues/Discussions) accessible
- [ ] Anchor links (`#section-name`) navigate correctly

---

## 🌿 Branching Strategy

```
main (protected branch)
  │
  ├── feature/docs-xxx    # feature branch
  ├── fix/link-broken     # fix branch
  └── i18n/en-update      # i18n branch
```

### Branch Naming Convention

```
<type>-<short-description>

Examples:
- feature/vision-screenshots
- fix/troubleshooting-link-404
- i18n/chat-config-en-translation
```

---

## 🔄 PR Workflow

### 1. Create a Branch

```powershell
git checkout -b feature/your-feature-name
```

### 2. Edit Files

Modify `.md` files following the conventions above.

### 3. Preview Locally

```powershell
# Preview Markdown in VS Code
code .

# Or use online tools
# https://markdownlivepreview.com/
```

### 4. Commit and Push

```powershell
git add .
git commit -m "docs(scope): brief description"
git push origin feature/your-feature-name
```

### 5. Create a Pull Request

Create a PR on GitHub and fill in the template fields.

### 6. Wait for Review

Maintainers will check:
- [ ] Content accuracy
- [ ] Format compliance
- [ ] Link validity
- [ ] No sensitive information leaked

### 7. After Merge

Post-merge actions triggered automatically (if CI is configured):
- Link checking
- Format validation
- Auto-deploy to GitHub Pages

---

## 📂 Directory Structure Convention

```
hermes-guide/
├── .github/
│   ├── PULL_REQUEST_TEMPLATE.md    # PR template
│   └── ISSUE_TEMPLATE/
│       ├── bug_report.md          # Bug report template
│       └── feature_request.md     # Feature request template
├── docs/
│   ├── zh-CN/                     # Chinese documentation (primary version)
│   │   ├── index.md              # Main navigation
│   │   ├── installation/         # Installation guide
│   │   ├── configuration/        # Configuration guide
│   │   ├── architecture/         # Architecture design
│   │   └── troubleshooting/       # Troubleshooting
│   └── en/                        # English documentation (mirrored structure)
├── examples/                      # Configuration examples
│   ├── .env.example
│   └── config.yaml.example
├── screenshots/                   # Screenshot assets
├── assets/                        # Other static resources
├── README.md                      # English landing page
├── README.zh-CN.md                # Chinese landing page
├── LICENSE                        # MIT License
└── .gitignore                     # Ignore rules
```

---

## 🎨 Writing Style

### Language

- Chinese: Simplified Chinese, keep technical terms in English (e.g., API / GPU / CUDA)
- English: American English, concise and clear

### Formatting

- Heading levels: maximum 4 levels (`#` → `####`)
- Lists: prefer ordered lists for steps, unordered tables for comparisons
- Code blocks: annotate with specific language (`powershell` / `yaml` / `bash`)
- Tables: align column widths, avoid horizontal scrolling

### Emoji Usage Guidelines

| Scenario | Recommended Emoji | Example |
|----------|-------------------|---------|
| Section headings | 🎯🔧⚙️📚💬👁️🎤📄🏗️🐛 | `## 🎯 Target Audience` |
| Status markers | ✅❌⚠️ | `✅ Completed` / `❌ Not supported` |
| Difficulty indicators | ⭐ | `⭐` `⭐⭐` `⭐⭐⭐` |
| Language indicators | 🇨🇳🇺🇸 | Toggle buttons |
| Model types | ☁️🔒 | Cloud / Local |

**Prohibited**: Adding emoji to every line of body text (overuse undermines professionalism)

---

## ❓ Frequently Asked Questions

### Q: Can I contribute only translations without writing new content?

A: Absolutely! Internationalization contributions are equally valuable.

### Q: I found a typo. Do I need to open a PR?

A: Minor issues can be reported as an Issue with the `[typo]` label.

### Q: I want to add screenshots. Are there any requirements?

A: Refer to the production guidelines in `screenshots/README.md`. All screenshots must be sanitized.

### Q: What if I make a mistake in my commit message?

A: If not yet pushed, use `git commit --amend` to correct it. If already pushed, create a new commit to fix it.

---

## 💬 Contact Channels

| Channel | Purpose |
|---------|---------|
| 🐛 [Issues](https://github.com/markwang2658/hermes-windows-native-guide/issues) | Bug reports |
| 💬 [Discussions](https://github.com/markwang2658/hermes-windows-native-guide/discussions) | Q&A and discussions |
| 📧 Other | Contact via Issues |

---

Thank you again for your contribution! 🎉
