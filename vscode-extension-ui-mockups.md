# SpecKit VSCode Extension - UI/UX Mockups

## Overview

This document provides detailed visual mockups and interaction flows for the SpecKit VSCode extension. These mockups illustrate the user interface components, workflows, and interactions described in the main proposal.

---

## Table of Contents

1. [Main Interface Layout](#main-interface-layout)
2. [Project Initialization Wizard](#project-initialization-wizard)
3. [Feature Explorer](#feature-explorer)
4. [Workflow Visualizer](#workflow-visualizer)
5. [Specification Editor](#specification-editor)
6. [Command Builder](#command-builder)
7. [Quality Dashboard](#quality-dashboard)
8. [Settings & Configuration](#settings--configuration)

---

## Main Interface Layout

### Full IDE Layout with SpecKit Active

```
┌────────────────────────────────────────────────────────────────────────────┐
│ VSCode - my-app (Workspace)                                    [- □ ×]      │
├────────────────────────────────────────────────────────────────────────────┤
│ File  Edit  Selection  View  Go  Run  Terminal  Help                       │
├───┬────────────────────────────────────────────────────────────────────────┤
│   │ ┌──────────────────────────────────────────────────────────────────┐   │
│   │ │ spec.md × plan.md × tasks.md ×                    [Split] [More]  │   │
│ A │ ├──────────────────────────────────────────────────────────────────┤   │
│ c │ │                                                                    │   │
│ t │ │  # Feature Specification: User Authentication                     │   │
│ i │ │  Feature: 001-user-authentication                                 │   │
│ v │ │  Status: Planning Phase (75% complete)                            │   │
│ i │ │                                                                    │   │
│ t │ │  ## Overview                                                      │   │
│ y │ │  [Quality Score: 87/100] [Constitutional Compliance: ✓]          │   │
│   │ │                                                                    │   │
│ B │ │  This feature implements secure user authentication...            │   │
│ a │ │                                                                    │   │
│ r │ │  ## User Stories                                                  │   │
│   │ │                                                                    │   │
│ ┌─┴─┐ │  ### US-1: User Login                    [CodeLens: View Plan]    │   │
│ │   │ │  As a user, I want to log in securely                            │   │
│ │ E │ │  So that I can access my account                                 │   │
│ │ x │ │                                                                    │   │
│ │ p │ │  ⚠️ 2 clarifications needed - Click to review                     │   │
│ │ l │ │                                                                    │   │
│ │ o │ │  **Acceptance Criteria:**                                         │   │
│ │ r │ │  - [ ] User can enter email and password                          │   │
│ │ e │ │  - [ ] System validates credentials                               │   │
│ │ r │ │  - [ ] User is redirected to dashboard on success                 │   │
│ │   │ │  - [×] Session expires after 24 hours                             │   │
│ │ F │ │       ⚠️ Missing: What happens on session expiry?                 │   │
│ │ i │ │                                                                    │   │
│ │ l │ └──────────────────────────────────────────────────────────────────┘   │
│ │ e │                                                                         │
│ │ s │ ┌──────────────────────────────────────────────────────────────────┐   │
│ └─┬─┘ │ TERMINAL                                          [×] [+] [⌄]    │   │
│   │   ├──────────────────────────────────────────────────────────────────┤   │
│ ┌─┴─┐ │ ❯ SpecKit: Generating implementation plan...                     │   │
│ │   │ │ ✓ Loading specification                                          │   │
│ │ S │ │ ✓ Analyzing constitution compliance                              │   │
│ │ p │ │ ▶ Researching authentication best practices...                   │   │
│ │ e │ │   Found: JWT tokens, OAuth 2.0, Session cookies                  │   │
│ │ c │ │ ○ Generating data models                                         │   │
│ │ K │ │ ○ Creating API contracts                                         │   │
│ │ i │ │                                                                    │   │
│ │ t │ │ [⏸️ Pause] [⏹️ Stop] [📋 View Logs]                                │   │
│ │   │ └──────────────────────────────────────────────────────────────────┘   │
│ │   │                                                                         │
│ │ V │ ┌──────────────────────────────────────────────────────────────────┐   │
│ │ i │ │ SPECKIT WORKFLOW                                  [Collapse] [×]  │   │
│ │ e │ ├──────────────────────────────────────────────────────────────────┤   │
│ │ w │ │                                                                    │   │
│ │   │ │  Current Feature: 001-user-authentication                         │   │
│ └─┬─┘ │                                                                    │   │
│   │   │  ┌──────┐   ┌──────┐   ┌──────┐   ┌──────┐   ┌──────┐           │   │
│   │   │  │Const.│──▶│ Spec │──▶│Clarif│──▶│ Plan │──▶│Tasks │───▶       │   │
│   │   │  │  ✓   │   │  ✓   │   │  ⚠️  │   │  ○   │   │  ○   │           │   │
│   │   │  └──────┘   └──────┘   └──────┘   └──────┘   └──────┘           │   │
│   │   │       │          │          │          │          │               │   │
│   │   │     100%       100%        60%        0%         0%               │   │
│   │   │                                                                    │   │
│   │   │  Progress: ████████████░░░░░░░░ 52% Complete                      │   │
│   │   │                                                                    │   │
│   │   │  Current Phase: Clarification                                     │   │
│   │   │  Status: 3 of 5 questions answered                                │   │
│   │   │  Blockers: 2 unanswered clarifications                            │   │
│   │   │                                                                    │   │
│   │   │  Next Steps:                                                      │   │
│   │   │  • Answer remaining clarification questions                       │   │
│   │   │  • Review specification completeness                              │   │
│   │   │  • Run quality validation checklist                               │   │
│   │   │                                                                    │   │
│   │   │  [Answer Clarifications] [Skip to Planning →]                     │   │
│   │   └──────────────────────────────────────────────────────────────────┘   │
├───┴────────────────────────────────────────────────────────────────────────┤
│ 🔧 SpecKit | 001-user-authentication | Phase: Clarification | 52% ✓       │
└────────────────────────────────────────────────────────────────────────────┘
```

**Key UI Elements:**
- **Activity Bar**: SpecKit icon with two main views (Explorer, SpecKit)
- **Sidebar**: Feature explorer tree and SpecKit panel
- **Editor**: Enhanced markdown editor with real-time validation
- **Panel**: Workflow visualizer and terminal output
- **Status Bar**: Current feature, phase, and progress indicator

---

## Project Initialization Wizard

### Step 1: Welcome Screen

```
┌────────────────────────────────────────────────────────────────┐
│  🌱 Welcome to SpecKit for VSCode                              │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Get started with Spec-Driven Development                      │
│                                                                 │
│  SpecKit helps you build high-quality software faster by       │
│  focusing on clear specifications that drive implementation.   │
│                                                                 │
│  What would you like to do?                                    │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐  │
│  │  🆕 Initialize New SpecKit Project                       │  │
│  │     Set up SpecKit in the current workspace              │  │
│  └─────────────────────────────────────────────────────────┘  │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐  │
│  │  📂 Open Existing SpecKit Project                        │  │
│  │     Browse and open an existing SpecKit workspace        │  │
│  └─────────────────────────────────────────────────────────┘  │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐  │
│  │  📚 View Tutorial                                        │  │
│  │     Learn the basics of Spec-Driven Development          │  │
│  └─────────────────────────────────────────────────────────┘  │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐  │
│  │  💡 Browse Examples                                      │  │
│  │     Explore sample projects and templates                │  │
│  └─────────────────────────────────────────────────────────┘  │
│                                                                 │
│                                       [Don't show again] [×]   │
└────────────────────────────────────────────────────────────────┘
```

### Step 2: Project Configuration

```
┌────────────────────────────────────────────────────────────────┐
│  Initialize SpecKit Project                          [Step 1/4] │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Project Name                                                   │
│  ┌─────────────────────────────────────────────────────────┐  │
│  │ my-awesome-app                                           │  │
│  └─────────────────────────────────────────────────────────┘  │
│  This will be used for documentation and display               │
│                                                                 │
│  Location                                                       │
│  ┌─────────────────────────────────────────────────────────┐  │
│  │ /Users/username/projects/my-awesome-app       [Browse]  │  │
│  └─────────────────────────────────────────────────────────┘  │
│  ☑️ Use current workspace (/Users/username/projects/my-app)    │
│                                                                 │
│  Git Repository                                                 │
│  ● Initialize new Git repository                               │
│  ○ Use existing repository                                     │
│  ○ Skip Git initialization                                     │
│                                                                 │
│  ⚠️ Git is required for feature branching and collaboration    │
│                                                                 │
│                                                                 │
│                            [Cancel]  [← Back]  [Next: Agent →] │
└────────────────────────────────────────────────────────────────┘
```

### Step 3: AI Agent Selection

```
┌────────────────────────────────────────────────────────────────┐
│  Select AI Agent                                     [Step 2/4] │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Choose the AI coding assistant you'll use with SpecKit        │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐  │
│  │  ✅ Claude Code (Recommended)                    [✓ v1.2] │  │
│  │  Anthropic's advanced AI coding assistant                │  │
│  │  Full support • CLI tool detected                        │  │
│  └─────────────────────────────────────────────────────────┘  │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐  │
│  │  ☐ GitHub Copilot                              [✓ v1.15] │  │
│  │  GitHub's AI pair programmer                             │  │
│  │  Full support • Extension detected                       │  │
│  └─────────────────────────────────────────────────────────┘  │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐  │
│  │  ☐ Gemini CLI                                  [✗ Not i] │  │
│  │  Google's AI assistant                                   │  │
│  │  Full support • Not installed [Install Guide →]         │  │
│  └─────────────────────────────────────────────────────────┘  │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐  │
│  │  ☐ Cursor                                       [✓ v0.12] │  │
│  │  The AI-first code editor                                │  │
│  │  Full support • CLI tool detected                        │  │
│  └─────────────────────────────────────────────────────────┘  │
│                                                                 │
│  [Show all 14 agents ↓]                                        │
│                                                                 │
│  💡 Tip: You can switch agents later in settings               │
│                                                                 │
│                            [Cancel]  [← Back]  [Next: Script →]│
└────────────────────────────────────────────────────────────────┘
```

### Step 4: Script Configuration

```
┌────────────────────────────────────────────────────────────────┐
│  Script Configuration                                [Step 3/4] │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  SpecKit uses shell scripts for certain operations             │
│  Select your preferred script type:                            │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐  │
│  │  ● Bash/Shell Scripts (.sh) [Recommended for macOS/Linux]│  │
│  │                                                           │  │
│  │  Compatible with: Bash, Zsh, Fish                        │  │
│  │  Platform: macOS, Linux, WSL                             │  │
│  └─────────────────────────────────────────────────────────┘  │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐  │
│  │  ○ PowerShell Scripts (.ps1) [Windows & Cross-platform] │  │
│  │                                                           │  │
│  │  Compatible with: PowerShell Core 7+                     │  │
│  │  Platform: Windows, macOS, Linux                         │  │
│  └─────────────────────────────────────────────────────────┘  │
│                                                                 │
│  ℹ️ Detected: macOS (Darwin) - Bash recommended                │
│                                                                 │
│  Advanced Options                                              │
│  ☐ Skip tool checks (not recommended)                          │
│  ☐ Use custom template repository                              │
│  ☐ Enable debug mode                                           │
│                                                                 │
│                            [Cancel]  [← Back]  [Next: Review →]│
└────────────────────────────────────────────────────────────────┘
```

### Step 5: Review & Confirm

```
┌────────────────────────────────────────────────────────────────┐
│  Review Configuration                                [Step 4/4] │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Please review your settings before initialization:            │
│                                                                 │
│  Project Details                                               │
│  ┌─────────────────────────────────────────────────────────┐  │
│  │  Name:           my-awesome-app                          │  │
│  │  Location:       /Users/username/projects/my-app         │  │
│  │  Git:            Initialize new repository               │  │
│  └─────────────────────────────────────────────────────────┘  │
│                                                                 │
│  AI Agent Configuration                                        │
│  ┌─────────────────────────────────────────────────────────┐  │
│  │  Agent:          Claude Code v1.2                        │  │
│  │  Command Dir:    .claude/commands/                       │  │
│  │  Status:         ✓ Ready                                 │  │
│  └─────────────────────────────────────────────────────────┘  │
│                                                                 │
│  Script Configuration                                          │
│  ┌─────────────────────────────────────────────────────────┐  │
│  │  Type:           Bash/Shell (.sh)                        │  │
│  │  Script Dir:     .specify/scripts/bash/                  │  │
│  └─────────────────────────────────────────────────────────┘  │
│                                                                 │
│  What will be created:                                         │
│  • .specify/ directory with templates and scripts              │
│  • .claude/commands/ directory with slash commands             │
│  • .specify/memory/constitution.md template                    │
│  • Git repository initialized                                  │
│  • Initial README.md with getting started guide                │
│                                                                 │
│                     [Cancel]  [← Back]  [Initialize Project 🚀]│
└────────────────────────────────────────────────────────────────┘
```

### Step 6: Initialization Progress

```
┌────────────────────────────────────────────────────────────────┐
│  Initializing SpecKit Project...                               │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ████████████████████████░░░░░░░░ 75%                          │
│                                                                 │
│  ✓ Created project directory structure                         │
│  ✓ Downloaded latest SpecKit templates (v1.5.2)                │
│  ✓ Initialized Git repository                                  │
│  ✓ Created .claude/commands/ directory                         │
│  ✓ Generated slash commands (8 commands)                       │
│  ▶ Setting up scripts and permissions...                       │
│  ○ Creating initial documentation                              │
│  ○ Finalizing configuration                                    │
│                                                                 │
│  This may take a few moments...                                │
│                                                                 │
│                                              [Cancel] [Hide]   │
└────────────────────────────────────────────────────────────────┘
```

### Step 7: Success & Next Steps

```
┌────────────────────────────────────────────────────────────────┐
│  ✅ Project Initialized Successfully!                           │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Your SpecKit project is ready to use!                         │
│                                                                 │
│  📂 Project: my-awesome-app                                    │
│  📍 Location: /Users/username/projects/my-app                  │
│  🤖 Agent: Claude Code                                         │
│                                                                 │
│  What's Next?                                                  │
│                                                                 │
│  1️⃣ Create Your Constitution                                   │
│     Define your project's governing principles                 │
│     [Create Constitution →]                                    │
│                                                                 │
│  2️⃣ Specify Your First Feature                                │
│     Describe what you want to build                            │
│     [Create Feature Specification →]                           │
│                                                                 │
│  3️⃣ Learn the Workflow                                        │
│     Take a quick tour of Spec-Driven Development               │
│     [Start Interactive Tutorial →]                             │
│                                                                 │
│  Resources                                                     │
│  • 📖 Documentation: docs.speckit.dev                          │
│  • 💬 Community: discord.gg/speckit                            │
│  • 🎥 Video Tutorial: youtube.com/watch?v=...                  │
│                                                                 │
│                    [View Project Dashboard] [Close]            │
└────────────────────────────────────────────────────────────────┘
```

---

## Feature Explorer

### Tree View Structure

```
┌────────────────────────────────────────────┐
│ SPECKIT EXPLORER                    [⚙️ ≡] │
├────────────────────────────────────────────┤
│                                            │
│ 🏠 PROJECT DASHBOARD                       │
│   ├─ 📊 Health Score: 85%                  │
│   ├─ 📈 Active Features: 3                 │
│   └─ ⚡ Quick Actions                      │
│       ├─ 📝 New Feature                    │
│       ├─ 🔍 Analyze Project                │
│       └─ 📤 Export Documentation           │
│                                            │
│ 📚 CONSTITUTION                            │
│   └─ 📄 constitution.md              [✓]  │
│       • 9 Articles Defined                 │
│       • Last updated: 2 days ago           │
│       [Open] [Edit] [Validate]             │
│                                            │
│ 🗂️  FEATURES                         [+]   │
│   │                                        │
│   ├─ 📁 001-user-authentication            │
│   │   ├─ 📊 Status: Planning (75%)         │
│   │   ├─ 🌿 Branch: 001-user-auth          │
│   │   ├─ 📋 Artifacts                      │
│   │   │   ├─ 📄 spec.md              [✓]  │
│   │   │   ├─ 📐 plan.md              [⚠️] │
│   │   │   ├─ 📝 clarifications.md    [✓]  │
│   │   │   ├─ 🔬 research.md          [✓]  │
│   │   │   ├─ 🗂️  data-model.md        [○]  │
│   │   │   ├─ 📋 contracts/            [○]  │
│   │   │   └─ ✅ tasks.md             [○]  │
│   │   ├─ 🔍 Quality: 87/100                │
│   │   └─ ⚠️  2 Blockers                    │
│   │       • Clarification Q4 unanswered    │
│   │       • Plan validation pending        │
│   │                                        │
│   ├─ 📁 002-photo-albums                   │
│   │   ├─ 📊 Status: Specification (45%)    │
│   │   ├─ 🌿 Branch: 002-photo-albums       │
│   │   ├─ 📋 Artifacts                      │
│   │   │   ├─ 📄 spec.md              [✓]  │
│   │   │   └─ 📝 clarifications.md    [⚠️] │
│   │   ├─ 🔍 Quality: 72/100                │
│   │   └─ ⚠️  3 Blockers                    │
│   │       • 5 clarifications needed        │
│   │       • Acceptance criteria incomplete │
│   │                                        │
│   └─ 📁 003-real-time-chat                 │
│       ├─ 📊 Status: Specification (20%)    │
│       ├─ 🌿 Branch: 003-chat-system        │
│       ├─ 📋 Artifacts                      │
│       │   └─ 📄 spec.md              [⚠️] │
│       ├─ 🔍 Quality: 45/100                │
│       └─ ⚠️  5 Blockers                    │
│           • User stories undefined         │
│           • Technical constraints missing  │
│                                            │
│ 📊 TEMPLATES                         [+]   │
│   ├─ 📄 Specification Template             │
│   ├─ 📐 Plan Template                      │
│   ├─ ✅ Tasks Template                     │
│   └─ 📋 Checklist Template                 │
│                                            │
│ ⚙️  SETTINGS                               │
│   ├─ 🤖 AI Agent: Claude Code              │
│   ├─ 📜 Script Type: Bash                  │
│   └─ 🔧 Advanced Settings...               │
│                                            │
└────────────────────────────────────────────┘
```

### Context Menu Actions

**Right-click on Feature:**
```
┌────────────────────────────────┐
│ 📄 Open Specification          │
│ 📐 Open Plan                   │
│ ✅ Open Tasks                  │
├────────────────────────────────┤
│ ▶️  Continue Workflow           │
│ 🔍 View Workflow Status        │
│ 📊 Run Quality Analysis        │
├────────────────────────────────┤
│ 🌿 Checkout Branch             │
│ 🔄 Sync with Remote            │
│ 📤 Create Pull Request         │
├────────────────────────────────┤
│ 🗑️  Delete Feature              │
│ 🏷️  Rename Feature              │
│ 📋 Duplicate Feature           │
└────────────────────────────────┘
```

---

## Workflow Visualizer

### Detailed Workflow Panel

```
┌──────────────────────────────────────────────────────────────────────────┐
│  WORKFLOW: 001-user-authentication                  [Expand] [Pin] [×]   │
├──────────────────────────────────────────────────────────────────────────┤
│                                                                           │
│  Overall Progress: ████████████░░░░░░░░ 52% Complete                     │
│                                                                           │
│  ┌─────────────────────────────────────────────────────────────────────┐ │
│  │                        WORKFLOW PHASES                               │ │
│  ├─────────────────────────────────────────────────────────────────────┤ │
│  │                                                                      │ │
│  │   ┌────────┐      ┌────────┐      ┌────────┐      ┌────────┐      │ │
│  │   │ CONST  │──────│  SPEC  │──────│ CLARIFY│──────│  PLAN  │───┐  │ │
│  │   │   ✓    │      │   ✓    │      │   ⚠️   │      │   ○    │   │  │ │
│  │   └────────┘      └────────┘      └────────┘      └────────┘   │  │ │
│  │      100%            100%             60%             0%         │  │ │
│  │                                        │                         │  │ │
│  │                              ┌─────────┴──────────┐              │  │ │
│  │                              │ 3 of 5 Answered    │              │  │ │
│  │                              │ 2 Pending          │              │  │ │
│  │                              └────────────────────┘              │  │ │
│  │                                                                   │  │ │
│  │   ┌────────┐      ┌────────┐      ┌────────┐                    │  │ │
│  │   │ TASKS  │──────│ANALYZE │──────│IMPLEMENT                    │  │ │
│  │   │   ○    │      │   ○    │      │   ○    │◀───────────────────┘  │ │
│  │   └────────┘      └────────┘      └────────┘                       │ │
│  │      0%              0%              0%                             │ │
│  │                                                                      │ │
│  └──────────────────────────────────────────────────────────────────────┘ │
│                                                                           │
│  ┌─────────────────────────────────────────────────────────────────────┐ │
│  │ 📍 CURRENT PHASE: Clarification                                     │ │
│  ├─────────────────────────────────────────────────────────────────────┤ │
│  │                                                                      │ │
│  │ Status: In Progress (60% complete)                                  │ │
│  │ Started: 2 hours ago                                                │ │
│  │ Last Updated: 15 minutes ago                                        │ │
│  │                                                                      │ │
│  │ Progress Details:                                                   │ │
│  │ • Questions answered: 3/5                                           │ │
│  │ • Specification updated: Yes                                        │ │
│  │ • Quality score impact: +12 points (predicted)                      │ │
│  │                                                                      │ │
│  │ Blockers:                                                           │ │
│  │ ⚠️  Q4: Authentication method not specified                          │ │
│  │ ⚠️  Q5: Session management strategy unclear                          │ │
│  │                                                                      │ │
│  │ [Answer Remaining Questions]  [View All Clarifications]             │ │
│  └──────────────────────────────────────────────────────────────────────┘ │
│                                                                           │
│  ┌─────────────────────────────────────────────────────────────────────┐ │
│  │ 🎯 NEXT STEPS                                                       │ │
│  ├─────────────────────────────────────────────────────────────────────┤ │
│  │                                                                      │ │
│  │ 1. Complete Clarifications                                          │ │
│  │    ⚠️  Required: 2 questions need answers                            │ │
│  │    [Open Clarifications Editor]                                     │ │
│  │                                                                      │ │
│  │ 2. Validate Specification                                           │ │
│  │    ○ Recommended: Run quality checklist                             │ │
│  │    [Run Validation]                                                 │ │
│  │                                                                      │ │
│  │ 3. Proceed to Planning                                              │ │
│  │    ○ Available after clarifications complete                        │ │
│  │    [Generate Implementation Plan] (disabled)                        │ │
│  │                                                                      │ │
│  └──────────────────────────────────────────────────────────────────────┘ │
│                                                                           │
│  ┌─────────────────────────────────────────────────────────────────────┐ │
│  │ 📊 QUALITY METRICS                                                  │ │
│  ├─────────────────────────────────────────────────────────────────────┤ │
│  │                                                                      │ │
│  │ Specification Quality: ████████████████░░░░ 87/100                  │ │
│  │                                                                      │ │
│  │ Breakdown:                                                          │ │
│  │ • Completeness:     ███████████████████░ 95/100 ✓                  │ │
│  │ • Clarity:          ██████████████░░░░░░ 78/100 ⚠️                  │ │
│  │ • Testability:      ████████████████░░░░ 85/100 ✓                  │ │
│  │ • Constitution:     ████████████████████ 100/100 ✓                 │ │
│  │                                                                      │ │
│  │ Issues Found:                                                       │ │
│  │ • 2 NEEDS CLARIFICATION markers remaining                           │ │
│  │ • 1 acceptance criterion missing test details                       │ │
│  │                                                                      │ │
│  │ [View Detailed Report]  [Fix Issues]                                │ │
│  └──────────────────────────────────────────────────────────────────────┘ │
│                                                                           │
│  [Phase History ↓]  [Export Workflow Report]  [Configure Workflow]      │
│                                                                           │
└───────────────────────────────────────────────────────────────────────────┘
```

### Phase Transition Dialog

```
┌──────────────────────────────────────────────┐
│  Phase Transition                            │
├──────────────────────────────────────────────┤
│                                              │
│  You are about to transition from:           │
│  Clarification → Planning                    │
│                                              │
│  Pre-transition Checklist:                   │
│  ✓ All clarifications answered               │
│  ✓ Specification validated                   │
│  ✓ Quality score above threshold (87/100)    │
│  ⚠️  1 optional recommendation pending        │
│                                              │
│  Recommendation:                             │
│  Consider adding edge case documentation     │
│  to user stories for better coverage.        │
│                                              │
│  ☐ Don't show recommendations again          │
│                                              │
│  Proceed with transition?                    │
│                                              │
│      [Cancel]  [Ignore & Proceed]  [Proceed] │
└──────────────────────────────────────────────┘
```

---

## Specification Editor

### Enhanced Markdown Editor with Inline Validation

```
┌──────────────────────────────────────────────────────────────────────────┐
│ spec.md × plan.md × tasks.md ×                 [Preview] [Outline] [⋮]   │
├──────────────────────────────────────────────────────────────────────────┤
│                                                                           │
│ 1  # Feature Specification: User Authentication                          │
│ 2                                                                         │
│ 3  **Feature ID:** 001                                                   │
│ 4  **Feature Name:** user-authentication                                 │
│ 5  **Status:** Clarification Phase (60% complete)                        │
│ 6  **Quality Score:** 87/100 ✓                                           │
│ 7                                                                         │
│ 8  [CodeLens: View Workflow] [Generate Plan] [Run Validation]            │
│ 9                                                                         │
│10  ## Overview                                                            │
│11                                                                         │
│12  This feature implements secure user authentication for the            │
│13  application, allowing users to create accounts, log in, and           │
│14  manage their sessions securely.                                       │
│15                                                                         │
│16  ## User Stories                                                        │
│17                                                                         │
│18  [CodeLens: Add User Story]                                            │
│19                                                                         │
│20  ### US-1: User Registration                                           │
│21  [CodeLens: Edit] [View in Plan] [Generate Tests]                      │
│22                                                                         │
│23  **As a** new user                                                     │
│24  **I want to** create an account with email and password               │
│25  **So that** I can access personalized features                        │
│26                                                                         │
│27  **Acceptance Criteria:**                                              │
│28  - [x] User can enter email address                                    │
│29  - [x] User can enter password (min 8 chars, mix of types)             │
│30  - [x] System validates email format                                   │
│31  - [x] System checks password strength                                 │
│32  - [ ] System sends verification email                                 │
│33        ⚠️ Missing: What happens if email fails to send?                 │
│34        💡 Quick Fix: Add error handling specification                   │
│35                                                                         │
│36  ### US-2: User Login                                                  │
│37  [CodeLens: Edit] [View in Plan] [Generate Tests]                      │
│38                                                                         │
│39  **As a** registered user                                              │
│40  **I want to** log in with my credentials                              │
│41  **So that** I can access my account                                   │
│42                                                                         │
│43  [NEEDS CLARIFICATION: What authentication method should be used?]     │
│44  ❌ Clarification required                                              │
│45  💡 Suggested: Email/password, OAuth, SSO, or combination?              │
│46  [Answer Clarification →]                                              │
│47                                                                         │
│48  **Acceptance Criteria:**                                              │
│49  - [x] User can enter credentials                                      │
│50  - [x] System validates credentials against database                   │
│51  - [ ] User is redirected to dashboard on success                      │
│52  - [×] Session expires after 24 hours                                  │
│53        ⚠️ Missing: Session management strategy not specified            │
│54        💡 Quick Fix: Add session handling details                       │
│55                                                                         │
│56  ## Non-Functional Requirements                                        │
│57                                                                         │
│58  ### Security                                                           │
│59  - Passwords must be hashed using bcrypt (cost factor ≥ 12)            │
│60  - HTTPS required for all authentication endpoints                     │
│61  - Rate limiting: max 5 failed attempts per 15 minutes                 │
│62  - Session tokens must be cryptographically secure                     │
│63                                                                         │
│64  ### Performance                                                        │
│65  - Login response time: < 500ms (p95)                                  │
│66  - Registration: < 1s (p95)                                            │
│67  - Support 1000 concurrent users                                       │
│68                                                                         │
│69  ## Clarifications                                                      │
│70                                                                         │
│71  [CodeLens: View Clarification Status (3/5 answered)]                  │
│72                                                                         │
│73  1. [✓] **Q:** Should we support social login (Google, GitHub)?        │
│74     **A:** No, not in this phase. Email/password only for MVP.         │
│75                                                                         │
│76  2. [✓] **Q:** What is the password complexity requirement?            │
│77     **A:** Minimum 8 characters, must include uppercase, lowercase,    │
│78              number, and special character.                            │
│79                                                                         │
│80  3. [✓] **Q:** Should we implement "Remember Me" functionality?        │
│81     **A:** Yes, extend session to 30 days with secure cookie.          │
│82                                                                         │
│83  4. [⚠️] **Q:** What authentication method should be used (JWT, │
│84               session cookies, etc.)?                                  │
│85     **A:** [PENDING - Click to answer]                                 │
│86                                                                         │
│87  5. [⚠️] **Q:** How should session expiry be handled (redirect,  │
│88               notification, etc.)?                                     │
│89     **A:** [PENDING - Click to answer]                                 │
│90                                                                         │
│                                                                           │
└───────────────────────────────────────────────────────────────────────────┘
```

### Inline Diagnostics Panel

```
┌──────────────────────────────────────────────────────────────────────────┐
│ PROBLEMS (5)  OUTPUT  DEBUG CONSOLE  TERMINAL  SPECKIT DIAGNOSTICS       │
├──────────────────────────────────────────────────────────────────────────┤
│                                                                           │
│ ⚠️  spec.md                                                               │
│   Line 43: [NEEDS CLARIFICATION] marker found                            │
│            Authentication method not specified                           │
│            [Quick Fix: Answer clarification]                             │
│                                                                           │
│ ⚠️  spec.md                                                               │
│   Line 84: Clarification pending                                         │
│            Question 4 requires an answer                                 │
│            [Quick Fix: Open clarification dialog]                        │
│                                                                           │
│ ⚠️  spec.md                                                               │
│   Line 33: Missing error handling specification                          │
│            Consider: What happens if verification email fails?           │
│            [Quick Fix: Add error scenario]                               │
│                                                                           │
│ ℹ️  spec.md                                                               │
│   Line 60: Constitutional compliance check                               │
│            Bcrypt aligns with Article VI (Security)                      │
│            [View Constitution →]                                         │
│                                                                           │
│ ℹ️  spec.md                                                               │
│   Quality Score: 87/100 (Good)                                           │
│   Completeness: 95%, Clarity: 78%, Testability: 85%                      │
│   [View Detailed Report]                                                 │
│                                                                           │
└───────────────────────────────────────────────────────────────────────────┘
```

### Hover Tooltip Example

```
┌──────────────────────────────────────────────────────────────────┐
│ Hover: Line 60                                                    │
├──────────────────────────────────────────────────────────────────┤
│                                                                   │
│ 💡 Constitutional Compliance                                      │
│                                                                   │
│ This requirement aligns with:                                    │
│                                                                   │
│ **Article VI: Security-First Principle**                         │
│ "All authentication systems MUST use industry-standard           │
│  cryptographic algorithms for password storage. Bcrypt with      │
│  cost factor ≥ 12 is the minimum acceptable standard."           │
│                                                                   │
│ ✓ Compliance Status: Approved                                    │
│                                                                   │
│ [View Full Constitution] [View Related Requirements]             │
│                                                                   │
└───────────────────────────────────────────────────────────────────┘
```

---

## Command Builder

### Command Construction Interface

```
┌──────────────────────────────────────────────────────────────────────────┐
│  SpecKit Command Builder                                        [Pin] [×] │
├──────────────────────────────────────────────────────────────────────────┤
│                                                                           │
│  Build and execute SpecKit commands with your AI agent                   │
│                                                                           │
│  Selected Feature: 001-user-authentication                               │
│  ┌─────────────────────────────────────────────────────────────────────┐ │
│  │ 001-user-authentication                                        [▼]  │ │
│  └─────────────────────────────────────────────────────────────────────┘ │
│                                                                           │
│  Command:                                                                │
│  ┌─────────────────────────────────────────────────────────────────────┐ │
│  │ /speckit.plan                                                  [▼]  │ │
│  └─────────────────────────────────────────────────────────────────────┘ │
│                                                                           │
│  Command: /speckit.plan                                                  │
│  Description: Create technical implementation plans                      │
│                                                                           │
│  ┌─────────────────────────────────────────────────────────────────────┐ │
│  │ 📋 PARAMETERS                                                        │ │
│  ├─────────────────────────────────────────────────────────────────────┤ │
│  │                                                                      │ │
│  │ Tech Stack Description (required)                                   │ │
│  │ ┌─────────────────────────────────────────────────────────────────┐ │ │
│  │ │ Node.js with Express backend, React frontend, PostgreSQL      │ │ │
│  │ │ database. Use JWT for authentication. Follow REST principles  │ │ │
│  │ │ for API design.                                                │ │ │
│  │ └─────────────────────────────────────────────────────────────────┘ │ │
│  │                                                                      │ │
│  │ ☑️ Include research phase (recommended)                              │ │
│  │ ☑️ Generate data models                                              │ │
│  │ ☑️ Create API contracts                                              │ │
│  │ ☐ Skip validation (not recommended)                                 │ │
│  │                                                                      │ │
│  └──────────────────────────────────────────────────────────────────────┘ │
│                                                                           │
│  ┌─────────────────────────────────────────────────────────────────────┐ │
│  │ 🔍 COMMAND PREVIEW                                                   │ │
│  ├─────────────────────────────────────────────────────────────────────┤ │
│  │                                                                      │ │
│  │ AI Agent: Claude Code                                               │ │
│  │                                                                      │ │
│  │ Command will execute:                                               │ │
│  │ /speckit.plan Node.js with Express backend, React frontend,         │ │
│  │ PostgreSQL database. Use JWT for authentication. Follow REST        │ │
│  │ principles for API design.                                          │ │
│  │                                                                      │ │
│  │ This will:                                                          │ │
│  │ 1. Read specification from specs/001-user-authentication/spec.md    │ │
│  │ 2. Validate constitutional compliance                               │ │
│  │ 3. Research specified technologies                                  │ │
│  │ 4. Generate implementation plan                                     │ │
│  │ 5. Create data models and API contracts                             │ │
│  │ 6. Update feature artifacts                                         │ │
│  │                                                                      │ │
│  │ Estimated duration: 5-10 minutes                                    │ │
│  │                                                                      │ │
│  └──────────────────────────────────────────────────────────────────────┘ │
│                                                                           │
│  ☐ Save as template "React + Node.js + PostgreSQL Stack"                │
│                                                                           │
│              [Cancel]  [Copy Command]  [Execute Command ▶️]               │
│                                                                           │
└───────────────────────────────────────────────────────────────────────────┘
```

### Command Execution Monitor

```
┌──────────────────────────────────────────────────────────────────────────┐
│  Executing: /speckit.plan                          [Minimize] [Stop] [×]  │
├──────────────────────────────────────────────────────────────────────────┤
│                                                                           │
│  Status: Running (3m 42s elapsed)                                        │
│                                                                           │
│  ██████████████████░░░░░░░ 67% Complete                                  │
│                                                                           │
│  Current Step: Generating API Contracts                                  │
│                                                                           │
│  ┌─────────────────────────────────────────────────────────────────────┐ │
│  │ EXECUTION LOG                                          [Filter] [▼]  │ │
│  ├─────────────────────────────────────────────────────────────────────┤ │
│  │                                                                      │ │
│  │ [14:32:15] ✓ Loaded specification                                   │ │
│  │ [14:32:16] ✓ Validated constitutional compliance                    │ │
│  │ [14:32:17] ▶ Researching technology stack...                        │ │
│  │ [14:32:45]   ✓ Node.js: v20 LTS recommended                         │ │
│  │ [14:32:48]   ✓ Express: v4.18+ with TypeScript support              │ │
│  │ [14:33:02]   ✓ PostgreSQL: v15+ with connection pooling             │ │
│  │ [14:33:15]   ✓ JWT: jsonwebtoken library, HS256 algorithm           │ │
│  │ [14:33:16] ✓ Created research.md                                    │ │
│  │ [14:33:20] ▶ Generating implementation plan...                       │ │
│  │ [14:34:35]   ✓ Architecture design complete                         │ │
│  │ [14:34:50]   ✓ Development phases defined                           │ │
│  │ [14:35:02] ✓ Created plan.md                                        │ │
│  │ [14:35:05] ▶ Generating data models...                              │ │
│  │ [14:35:30]   ✓ User entity model created                            │ │
│  │ [14:35:45]   ✓ Session entity model created                         │ │
│  │ [14:35:50] ✓ Created data-model.md                                  │ │
│  │ [14:35:52] ▶ Creating API contracts...                              │ │
│  │ [14:36:10]   • POST /api/auth/register                              │ │
│  │ [14:36:20]   • POST /api/auth/login                                 │ │
│  │ [14:36:28]   • POST /api/auth/logout                                │ │
│  │                                                                      │ │
│  └──────────────────────────────────────────────────────────────────────┘ │
│                                                                           │
│  Recent Activity:                                                        │
│  • Generated 2 data models                                               │
│  • Created 15 API endpoints                                              │
│  • Identified 3 external dependencies                                    │
│                                                                           │
│  [View Full Output]  [Export Log]                                        │
│                                                                           │
└───────────────────────────────────────────────────────────────────────────┘
```

### Command Completion

```
┌──────────────────────────────────────────────────────────────────────────┐
│  ✅ Command Completed Successfully                            [View] [×]  │
├──────────────────────────────────────────────────────────────────────────┤
│                                                                           │
│  /speckit.plan completed in 7m 23s                                       │
│                                                                           │
│  📊 Summary:                                                             │
│  • Created implementation plan (plan.md)                                 │
│  • Generated research document (research.md)                             │
│  • Created data models (data-model.md)                                   │
│  • Generated API contracts (contracts/auth-api.yaml)                     │
│  • Updated workflow status → Planning Complete                           │
│                                                                           │
│  📈 Quality Impact:                                                      │
│  • Quality score: 87 → 92 (+5)                                           │
│  • Feature completeness: 60% → 85% (+25%)                                │
│                                                                           │
│  🎯 Next Recommended Actions:                                            │
│  1. Review generated implementation plan                                 │
│  2. Validate data models against requirements                            │
│  3. Run cross-artifact consistency analysis                              │
│  4. Proceed to task breakdown (/speckit.tasks)                           │
│                                                                           │
│  ┌─────────────────────────────────────────────────────────────────────┐ │
│  │ Created Files:                                                       │ │
│  │ • specs/001-user-authentication/plan.md              [Open]          │ │
│  │ • specs/001-user-authentication/research.md          [Open]          │ │
│  │ • specs/001-user-authentication/data-model.md        [Open]          │ │
│  │ • specs/001-user-authentication/contracts/           [Open Folder]   │ │
│  └──────────────────────────────────────────────────────────────────────┘ │
│                                                                           │
│        [View Workflow]  [Run Analysis]  [Continue to Tasks →]            │
│                                                                           │
└───────────────────────────────────────────────────────────────────────────┘
```

---

## Quality Dashboard

### Comprehensive Quality Overview

```
┌──────────────────────────────────────────────────────────────────────────┐
│  Quality Dashboard: 001-user-authentication              [Refresh] [Export]│
├──────────────────────────────────────────────────────────────────────────┤
│                                                                           │
│  Overall Quality Score: 92/100                                           │
│                                                                           │
│  ████████████████████████████████████░░░░ Excellent                      │
│                                                                           │
│  ┌─────────────────────────────────────────────────────────────────────┐ │
│  │ QUALITY BREAKDOWN                                                    │ │
│  ├─────────────────────────────────────────────────────────────────────┤ │
│  │                                                                      │ │
│  │ Specification Quality                    ████████████████████ 95/100│ │
│  │  ├─ Completeness                         ████████████████████ 98   │ │
│  │  ├─ Clarity                               ███████████████████░ 92   │ │
│  │  ├─ Testability                          ████████████████████ 95   │ │
│  │  └─ User Story Coverage                  ████████████████████ 100  │ │
│  │                                                                      │ │
│  │ Implementation Plan Quality              ███████████████████░ 90/100│ │
│  │  ├─ Technical Detail                     ███████████████████░ 88   │ │
│  │  ├─ Architecture Clarity                 ████████████████████ 95   │ │
│  │  ├─ Dependency Management                ███████████████████░ 87   │ │
│  │  └─ Risk Assessment                      ████████████████████ 92   │ │
│  │                                                                      │ │
│  │ Constitutional Compliance                ████████████████████ 100/100│ │
│  │  ├─ Article I: Library-First             ████████████████████ ✓    │ │
│  │  ├─ Article II: CLI Interface            ████████████████████ ✓    │ │
│  │  ├─ Article III: Test-First              ████████████████████ ✓    │ │
│  │  ├─ Article VII: Simplicity              ████████████████████ ✓    │ │
│  │  └─ Article VIII: Anti-Abstraction       ████████████████████ ✓    │ │
│  │                                                                      │ │
│  │ Cross-Artifact Consistency               ███████████████████░ 88/100│ │
│  │  ├─ Spec ↔ Plan Alignment                ███████████████████░ 90   │ │
│  │  ├─ Plan ↔ Data Model Alignment          ███████████████████░ 85   │ │
│  │  ├─ Requirements Traceability            ████████████████████ 92   │ │
│  │  └─ No Orphaned Artifacts                ████████████████████ ✓    │ │
│  │                                                                      │ │
│  └──────────────────────────────────────────────────────────────────────┘ │
│                                                                           │
│  ┌─────────────────────────────────────────────────────────────────────┐ │
│  │ ISSUES & RECOMMENDATIONS                                      [2]    │ │
│  ├─────────────────────────────────────────────────────────────────────┤ │
│  │                                                                      │ │
│  │ ⚠️  Moderate Priority                                                 │ │
│  │    Missing edge case documentation in US-1                          │ │
│  │    Location: spec.md:33                                             │
│  │    Recommendation: Add error handling for email delivery failures   │ │
│  │    [Fix Now] [Ignore] [View Details]                                │ │
│  │                                                                      │ │
│  │ ℹ️  Low Priority                                                      │ │
│  │    Consider adding performance benchmarks                           │ │
│  │    Location: plan.md:67                                             │
│  │    Recommendation: Define specific load testing criteria            │ │
│  │    [Fix Now] [Ignore] [View Details]                                │ │
│  │                                                                      │ │
│  └──────────────────────────────────────────────────────────────────────┘ │
│                                                                           │
│  ┌─────────────────────────────────────────────────────────────────────┐ │
│  │ TREND ANALYSIS                                            [Last 7d]  │ │
│  ├─────────────────────────────────────────────────────────────────────┤ │
│  │                                                                      │ │
│  │  Quality Score Over Time:                                           │ │
│  │                                                                      │ │
│  │  100│                                            ●                   │ │
│  │   90│                                  ●────────●                    │ │
│  │   80│                        ●────────●                             │ │
│  │   70│              ●────────●                                        │ │
│  │   60│    ●────────●                                                  │ │
│  │   50│                                                                │ │
│  │     └────────────────────────────────────────────────               │ │
│  │      Day1  Day2  Day3  Day4  Day5  Day6  Day7                       │ │
│  │                                                                      │ │
│  │  • Initial specification created (Day 1): 60/100                    │ │
│  │  • Clarifications completed (Day 3): 75/100                         │ │
│  │  • Implementation plan added (Day 5): 87/100                        │ │
│  │  • Data models & contracts (Day 7): 92/100                          │ │
│  │                                                                      │ │
│  └──────────────────────────────────────────────────────────────────────┘ │
│                                                                           │
│  [View Detailed Report] [Export to PDF] [Compare with Other Features]    │
│                                                                           │
└───────────────────────────────────────────────────────────────────────────┘
```

---

## Settings & Configuration

### SpecKit Settings Panel

```
┌──────────────────────────────────────────────────────────────────────────┐
│  SpecKit Settings                                         [Search] [Reset]│
├──────────────────────────────────────────────────────────────────────────┤
│                                                                           │
│  ┌─────────────────────────────────────────────────────────────────────┐ │
│  │ 🤖 AI AGENT CONFIGURATION                                            │ │
│  ├─────────────────────────────────────────────────────────────────────┤ │
│  │                                                                      │ │
│  │ Active Agent                                                         │ │
│  │ ┌─────────────────────────────────────────────────────────────────┐ │ │
│  │ │ Claude Code v1.2                                           [▼]  │ │ │
│  │ └─────────────────────────────────────────────────────────────────┘ │ │
│  │                                                                      │ │
│  │ Command Directory                                                    │ │
│  │ ┌─────────────────────────────────────────────────────────────────┐ │ │
│  │ │ .claude/commands/                                              │ │ │
│  │ └─────────────────────────────────────────────────────────────────┘ │ │
│  │                                                                      │ │
│  │ ☑️ Auto-detect agent changes                                         │ │
│  │ ☑️ Show agent status in status bar                                   │ │
│  │ ☐ Allow multiple agents simultaneously                              │ │
│  │                                                                      │ │
│  │ [Detect Agents] [Test Connection]                                   │ │
│  │                                                                      │ │
│  └──────────────────────────────────────────────────────────────────────┘ │
│                                                                           │
│  ┌─────────────────────────────────────────────────────────────────────┐ │
│  │ 📝 WORKFLOW CONFIGURATION                                            │ │
│  ├─────────────────────────────────────────────────────────────────────┤ │
│  │                                                                      │ │
│  │ Workflow Enforcement                                                 │ │
│  │ ● Strict (enforce all phase transitions)                            │ │
│  │ ○ Guided (show warnings but allow skipping)                         │ │
│  │ ○ Flexible (minimal validation)                                     │ │
│  │                                                                      │ │
│  │ Quality Thresholds                                                   │ │
│  │ Minimum specification quality score:  [75]                          │ │
│  │ Minimum plan quality score:           [70]                          │ │
│  │ Block on constitutional violations:   [✓]                           │ │
│  │                                                                      │ │
│  │ ☑️ Show workflow visualizer by default                               │ │
│  │ ☑️ Auto-update workflow status                                       │ │
│  │ ☑️ Prompt for validation before phase transitions                    │ │
│  │                                                                      │ │
│  └──────────────────────────────────────────────────────────────────────┘ │
│                                                                           │
│  ┌─────────────────────────────────────────────────────────────────────┐ │
│  │ 🎨 EDITOR ENHANCEMENTS                                               │ │
│  ├─────────────────────────────────────────────────────────────────────┤ │
│  │                                                                      │ │
│  │ ☑️ Enable real-time validation                                       │ │
│  │ ☑️ Show CodeLens actions                                             │ │
│  │ ☑️ Display hover tooltips                                            │ │
│  │ ☑️ Inline diagnostics                                                │ │
│  │ ☑️ Auto-completion for templates                                     │ │
│  │                                                                      │ │
│  │ Validation Delay (ms):  [500]                                       │ │
│  │ Max diagnostics shown:   [50]                                       │ │
│  │                                                                      │ │
│  └──────────────────────────────────────────────────────────────────────┘ │
│                                                                           │
│  ┌─────────────────────────────────────────────────────────────────────┐ │
│  │ 🌿 GIT INTEGRATION                                                   │ │
│  ├─────────────────────────────────────────────────────────────────────┤ │
│  │                                                                      │ │
│  │ ☑️ Auto-create feature branches                                      │ │
│  │ ☑️ Auto-commit after phase completion                                │ │
│  │ ☐ Auto-push to remote                                               │ │
│  │                                                                      │ │
│  │ Branch Naming Pattern                                               │ │
│  │ ┌─────────────────────────────────────────────────────────────────┐ │ │
│  │ │ {number}-{feature-name}                                         │ │ │
│  │ └─────────────────────────────────────────────────────────────────┘ │ │
│  │                                                                      │ │
│  │ Feature Numbering                                                   │ │
│  │ Starting number:  [001]                                             │ │
│  │ Padding digits:   [3]                                               │ │
│  │                                                                      │ │
│  └──────────────────────────────────────────────────────────────────────┘ │
│                                                                           │
│  ┌─────────────────────────────────────────────────────────────────────┐ │
│  │ 📊 ANALYTICS & TELEMETRY                                             │ │
│  ├─────────────────────────────────────────────────────────────────────┤ │
│  │                                                                      │ │
│  │ ☑️ Enable quality trend tracking                                     │ │
│  │ ☑️ Track command usage statistics                                    │ │
│  │ ☐ Send anonymous usage data (helps improve SpecKit)                 │ │
│  │                                                                      │ │
│  │ Data retention period:  [90 days]                                   │ │
│  │                                                                      │ │
│  │ [View Privacy Policy] [Export My Data] [Clear Analytics Data]       │ │
│  │                                                                      │ │
│  └──────────────────────────────────────────────────────────────────────┘ │
│                                                                           │
│  [Reset to Defaults]  [Import Config]  [Export Config]  [Save Changes]   │
│                                                                           │
└───────────────────────────────────────────────────────────────────────────┘
```

---

## Conclusion

These mockups illustrate the comprehensive user interface design for the SpecKit VSCode extension. The design emphasizes:

1. **Visual Clarity** - Clear representation of workflow states and progress
2. **Actionable Feedback** - Inline validation with quick fixes
3. **Guided Workflows** - Step-by-step processes for complex operations
4. **Real-time Updates** - Immediate feedback on quality and compliance
5. **Seamless Integration** - Natural fit within VSCode's existing UI patterns

The mockups serve as the foundation for implementation, providing clear specifications for developers and a shared vision for stakeholders.
