---
title: GitHub as Claude Memory Brain — Team Setup Guide
tags: [tech, claude, mcp, github, setup]
updated: 2026-05-02
---

# 🧠 GitHub as Claude's Memory Brain — Team Setup Guide

> **GitHub = Memory (Brain) | Claude = Thinking Engine**

This guide walks the entire team through connecting a GitHub repository as Claude's long-term memory. Once set up, Claude can read your team's notes, projects, and knowledge base directly from GitHub — making every conversation smarter and more contextual.

---

## 🏗️ Architecture

```
GitHub Repo         →   MCP Protocol   →   Claude Desktop
(Your Memory Brain)     (The Bridge)       (Thinking Engine)

📁 my-brain/
├── projects/       →   Claude reads   →   Knows your projects
├── knowledge/      →   Claude reads   →   Knows your tech stack
├── people/         →   Claude reads   →   Knows your team
├── daily/          →   Claude reads   →   Knows your daily context
└── meta/           →   Claude reads   →   Knows your summary
```

---

## ✅ Prerequisites

Before starting, make sure you have:

| Requirement | Where to get it |
|-------------|----------------|
| GitHub Account | github.com/signup |
| Claude Desktop App | claude.ai/download |
| Node.js (LTS version) | nodejs.org |
| Mac or Windows PC | — |

---

## 📋 Step-by-Step Setup

### Step 1 — Create Your GitHub Repository

1. Go to **github.com/new**
2. Fill in:
   - **Repository name:** `Claude-memory`
   - **Description:** `My Claude AI memory brain`
   - **Visibility:** ✅ Private
   - ✅ Check "Add a README file"
3. Click **"Create repository"**

```
┌─────────────────────────────────────────┐
│  Create a new repository                │
│  ─────────────────────────────────────  │
│  Repository name: [ Claude-memory     ] │
│  ⦿ Private  ○ Public  ← Select Private  │
│  ☑ Add a README file  ← Check this      │
│  [ Create repository ]  ← Click this   │
└─────────────────────────────────────────┘
```

---

### Step 2 — Upload Brain Files

1. On your empty repo page, find the blue **Quick Setup** box
2. Click **"uploading an existing file"** link
3. Extract the `my-brain.zip` file your team lead shares
4. Drag all the contents into the GitHub upload box
5. Scroll down → Click **"Commit changes"**

```
Quick setup — if you've done this kind of thing before
──────────────────────────────────────────────────────
Get started by creating a new file or
[uploading an existing file]  ← CLICK THIS LINK
```

**Your repo structure after upload:**
```
Claude-memory/
└── my-brain/
    ├── README.md
    ├── daily/
    ├── knowledge/
    ├── meta/          ← Claude reads this first
    ├── people/
    ├── projects/
    └── templates/
```

---

### Step 3 — Install Node.js

Node.js is required to run the GitHub MCP server.

1. Go to **nodejs.org**
2. Download the **LTS version** (left button — recommended)
3. Run the installer — keep all default settings

```
nodejs.org
┌─────────────────┐    ┌─────────────────┐
│  22.x.x (LTS)  │    │  23.x.x (Current│
│  ✅ Download    │    │  ❌ Skip this   │
│  this one       │    │                 │
└─────────────────┘    └─────────────────┘
```

**Verify installation** — open Terminal and run:
```bash
node --version    # Should show v22.x.x
npx --version     # Should show 10.x.x
```

---

### Step 4 — Create a GitHub Personal Access Token

> ⚠️ **IMPORTANT:** Use Classic token, NOT Fine-grained token

1. Go to **github.com/settings/tokens**
2. Click **"Generate new token"** → **"Generate new token (classic)"**
3. Fill in:
   - **Note:** `claude-memory`
   - **Expiration:** 90 days
4. Scroll down to **Select scopes** → Check only ✅ `repo`
5. Click **"Generate token"**
6. **COPY THE TOKEN IMMEDIATELY** — you won't see it again!

```
New personal access token (classic)
────────────────────────────────────
Note:        [ claude-memory     ]
Expiration:  [ 90 days ▼        ]

Select scopes:
☑ repo  ← CHECK THIS ONE ONLY
  ☑ repo:status      (auto-checked)
  ☑ repo_deployment  (auto-checked)
  ☑ public_repo      (auto-checked)
☐ workflow           (leave unchecked)

[ Generate token ]  ← Scroll down, click this
```

> ⚠️ **CRITICAL:** Copy your token (starts with `ghp_`) immediately!
> GitHub will NEVER show it again after you leave the page.

```
✅ Make sure to copy your personal access token now.
   You won't be able to see it again!

  ghp_xxxxxxxxxxxxxxxxxxxxxxxxxxxx  [📋 copy]
```

---

### Step 5 — Configure Claude Desktop

1. **Open Terminal** on your Mac (`Cmd + Space` → type "Terminal" → Enter)

2. **Run this single command** (replace `YOUR_TOKEN_HERE` with your `ghp_` token):

```bash
cat > ~/Library/Application\ Support/Claude/claude_desktop_config.json << 'EOF'
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-github"
      ],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "YOUR_TOKEN_HERE"
      }
    }
  },
  "preferences": {
    "coworkWebSearchEnabled": true,
    "coworkScheduledTasksEnabled": true,
    "ccdScheduledTasksEnabled": true
  }
}
EOF
```

3. **Verify it saved correctly:**
```bash
cat ~/Library/Application\ Support/Claude/claude_desktop_config.json
```

You should see both `mcpServers` AND `preferences` in the output ✅

4. **Fully quit and restart Claude Desktop:**
   - Press `Cmd + Q` (not just close the window)
   - Wait 5 seconds
   - Reopen Claude Desktop from Applications

---

### Step 6 — Test the Connection

1. Open Claude Desktop
2. Start a **New Chat**
3. Type this test message:

```
List all files in my GitHub repo YOUR_USERNAME/Claude-memory
```

**Success looks like this ✅**
```
📁 my-brain/
   📄 README.md
   📁 daily/
   📁 knowledge/
   📁 meta/
   📁 people/
   📁 projects/
   📁 templates/
```

---

## 🚀 How to Use Claude With Your Brain

Once connected, here are powerful prompts to use:

**Read your memory context:**
```
Read my file meta/summary.md from repo YOUR_USERNAME/Claude-memory
and use it as my personal memory context
```

**Get project help:**
```
Read projects/project-alpha.md from my Claude-memory repo.
What should I focus on today?
```

**Update your notes:**
```
Update my daily/2026-05-02.md in Claude-memory with what we discussed today
```

**Search your knowledge:**
```
Search my Claude-memory repo for anything related to API architecture decisions
```

---

## 📁 Repo Folder Guide

| Folder | Purpose | Example Files |
|--------|---------|---------------|
| `projects/` | Active & past project notes | project-alpha.md |
| `knowledge/` | Domain knowledge & tech notes | tech-stack.md |
| `people/` | Team & contact context | team.md |
| `daily/` | Daily logs & journal | 2026-05-02.md |
| `templates/` | Reusable note templates | note-template.md |
| `meta/` | Brain summary — Claude reads this first | summary.md |

---

## 🔧 Troubleshooting

| Problem | Fix |
|---------|-----|
| No hammer 🔨 icon in Claude | Fully quit with `Cmd+Q` then reopen |
| Token not working | Make sure `repo` checkbox was ticked |
| Config not saved | Re-run the `cat >` command, verify with `cat` |
| Connection refused | Token expired — generate a new one |
| Wrong token page | Use Classic token at `github.com/settings/tokens/new` |
| Two `{}` blocks in config | Re-run the single command to overwrite |

---

## 🔒 Security Best Practices

- **Never share your token** in chat, email, or Slack
- **Regenerate tokens** if accidentally exposed
- **Use 90-day expiry** — set a calendar reminder to renew
- **Keep repo Private** — don't make your brain public
- **One token per person** — don't share tokens across team members

---

## ✅ Setup Checklist

Use this checklist to track your progress:

- [ ] GitHub account created
- [ ] Claude Desktop installed
- [ ] Node.js (LTS) installed and verified
- [ ] `Claude-memory` repo created (Private)
- [ ] Brain files uploaded to repo
- [ ] GitHub Classic token generated with `repo` scope
- [ ] Token saved safely
- [ ] Claude Desktop config file updated
- [ ] Claude Desktop restarted
- [ ] Connection tested — Claude can list repo files
- [ ] `meta/summary.md` updated with your personal info

---

*🧠 GitHub = Memory | Claude = Thinking Engine | Setup Complete! 🚀*

*Questions? Contact your team lead or refer to docs.anthropic.com*
