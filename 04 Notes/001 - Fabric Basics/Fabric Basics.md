# Fabric Basics — macOS Guide

## What is Fabric?

**Fabric** by Daniel Miessler is an open-source framework for augmenting humans using AI. It provides a modular system for solving specific problems using a crowdsourced set of AI prompts (called **Patterns**) that can be used anywhere.

- **GitHub:** https://github.com/danielmiessler/Fabric
- **Stars:** 40.3k+
- **Language:** Go
- **License:** MIT

> AI doesn't have a capabilities problem — it has an *integration* problem. Fabric solves this by organizing prompts by real-world task.

---

## Prerequisites

### 1. Install Homebrew (if you don't have it)

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### 2. Install Go (optional — only needed if installing from source)

```bash
brew install go
```

---

## Installation

### Option 1: Homebrew (Recommended for macOS)

```bash
brew install fabric-ai
```

> Homebrew installs it as `fabric-ai`. You'll set up the alias below.

### Option 2: One-Line Install

```bash
curl -fsSL https://raw.githubusercontent.com/danielmiessler/fabric/main/scripts/installer/install.sh | bash
```

### Option 3: From Source

```bash
go install github.com/danielmiessler/fabric/cmd/fabric@latest
```

---

## macOS Shell Setup

Fabric uses `zsh` by default on macOS (since Catalina). Add this to your `~/.zshrc`:

```bash
# ─── Fabric ───────────────────────────────────────────────

# Alias (if installed via Homebrew)
alias fabric='fabric-ai'

# Auto-aliases for all patterns (use "summarize" instead of "fabric --pattern summarize")
for pattern_file in $HOME/.config/fabric/patterns/*; do
    pattern_name="$(basename "$pattern_file")"
    alias "$pattern_name"="fabric --pattern $pattern_name"
done

# YouTube transcript shortcut
yt() {
    local video_link="$1"
    fabric -y "$video_link" --pattern summarize
}

# ──────────────────────────────────────────────────────────
```

Reload your shell:

```bash
source ~/.zshrc
```

---

## Setup

```bash
fabric --setup
```

This will:
1. Ask you to pick an AI provider (OpenAI, Anthropic, Ollama, etc.)
2. Prompt for your API key
3. Download all available Patterns to `~/.config/fabric/patterns/`

### Supported AI Providers

**Native:**
- OpenAI / OpenAI Codex
- Anthropic (Claude)
- Google Gemini
- Ollama (local models — runs on your Mac, no API key needed)
- Azure OpenAI
- LM Studio (local models with GUI)
- Perplexity

**OpenAI-Compatible:**
- Groq, Mistral, DeepSeek, OpenRouter, Together, Grok, Cerebras, and many more

List all vendors:
```bash
fabric --listvendors
```

---

## Basic Usage

### List all patterns

```bash
fabric --listpatterns
```

### Use a pattern

```bash
# From clipboard (macOS)
pbpaste | fabric --pattern summarize

# Stream output (see it generate in real-time)
pbpaste | fabric --pattern summarize --stream

# Save output to a file
pbpaste | fabric --pattern summarize -o ~/Desktop/summary.md

# Copy output back to clipboard
pbpaste | fabric --pattern summarize --copy
```

### Using aliases (after shell setup)

```bash
pbpaste | summarize
pbpaste | extract_wisdom
pbpaste | write_essay
pbpaste | explain_code
```

---

## Most Useful Patterns

| Pattern | What it does |
|---------|-------------|
| `summarize` | Summarize any content |
| `extract_wisdom` | Extract key insights & lessons |
| `extract_patterns` | Find patterns in data/text |
| `write_essay` | Write an essay from an idea |
| `write_micro_essay` | Write a short essay |
| `explain_code` | Explain code in plain English |
| `analyze_claims` | Analyze claims with evidence |
| `rate_content` | Rate content quality |
| `improve_prompt` | Improve your prompts |
| `create_command` | Generate shell commands |
| `to_flashcards` | Create study flashcards |
| `summarize_paper` | Summarize academic papers |
| `summarize_newsletter` | Summarize newsletters |
| `summarize_git_changes` | Summarize git diff |
| `write_pull-request` | Write PR descriptions |
| `create_video_chapters` | Create YouTube chapters |
| `label_and_rate` | Rate & label content |
| `show_fabric_options_markmap` | Visual concept map |

---

## YouTube Integration

```bash
# Summarize a YouTube video transcript
fabric -y "https://youtube.com/watch?v=VIDEO_ID" --pattern summarize

# With timestamps
fabric -y "https://youtube.com/watch?v=VIDEO_ID" --transcript-with-timestamps --pattern extract_wisdom

# Get comments and summarize
fabric -y "https://youtube.com/watch?v=VIDEO_ID" --comments --pattern summarize

# Using the yt alias (after shell setup)
yt "https://youtube.com/watch?v=VIDEO_ID"
```

---

## Web Scraping to Markdown

```bash
# Scrape any URL to clean markdown
fabric --scrape_url "https://example.com/article"

# Scrape + summarize in one pipeline
fabric --scrape_url "https://example.com/article" | fabric --pattern summarize

# Scrape + extract wisdom
fabric --scrape_url "https://example.com/article" | fabric --pattern extract_wisdom
```

---

## Adding Custom Patterns (Skills)

Patterns live in `~/.config/fabric/patterns/`. Each pattern is a folder with a `system.md` file.

### Create a custom pattern

```bash
# Create the pattern folder
mkdir -p ~/.config/fabric/patterns/my_custom_pattern

# Create the system prompt
cat > ~/.config/fabric/patterns/my_custom_pattern/system.md << 'EOF'
# IDENTITY and PURPOSE

You are an expert at [your task].

Take a step back and think step-by-step about how to achieve the best possible results.

# STEPS

- Step 1: ...
- Step 2: ...
- Step 3: ...

# OUTPUT INSTRUCTIONS

- Only output Markdown.
- Do not give warnings or notes.
- You use bulleted lists for output.
- Ensure you follow ALL these instructions.

# INPUT

INPUT:
EOF
```

### Use your custom pattern

```bash
pbpaste | fabric --pattern my_custom_pattern
```

### Update all patterns from the repo

```bash
fabric --updatepatterns
```

---

## Contexts & Sessions

### Contexts (background info for patterns)

```bash
fabric --listcontexts          # List available contexts
fabric --context my_context --pattern summarize   # Use with a pattern
fabric --printcontext=my_context                  # View a context
```

### Sessions (persistent conversations)

```bash
fabric --listsessions          # List sessions
fabric --session my_chat --pattern summarize   # Use a session
fabric --wipesession=my_chat   # Clear a session
```

---

## Advanced macOS Tips

### Set a specific model per pattern

Add to `~/.zshrc`:

```bash
export FABRIC_MODEL_SUMMARIZE="anthropic|claude-sonnet-4-5-20250514"
export FABRIC_MODEL_EXTRACT_WISDOM="openai|gpt-4o"
```

### Dry run (preview prompt without spending credits)

```bash
echo "test" | fabric --dry-run --pattern summarize
```

### Save Fabric output directly to your Notes

```bash
pbpaste | fabric --pattern summarize -o "$HOME/04 Notes/000 Inbox/$(date +%Y-%m-%d)-summary.md"
```

### Process a file directly

```bash
fabric --pattern summarize < ~/Documents/report.pdf
```

### REST API Server

```bash
fabric --serve
```

Runs at `http://localhost:8080` with Swagger docs at `/swagger/index.html`.

### Ollama Compatibility Mode (use Fabric as Ollama drop-in)

```bash
fabric --serve --serveOllama
```

---

## TELOS + Fabric — Using Them Together

TELOS is your personal context framework. Fabric is your AI execution engine. Together, they let you run AI-powered tasks that are deeply personalized to your life, goals, and challenges.

### The Concept

```
TELOS (your context) → Fabric (your AI patterns) → Personalized output
```

Every Fabric pattern can be fed your TELOS document so the AI understands **who you are, what you're solving, and why** — instead of giving generic responses.

---

### Step 1: Add TELOS as a Fabric Context

Fabric has a **Contexts** system — background info that gets attached to any pattern. Your TELOS document is the perfect context.

```bash
# Create a TELOS context file
mkdir -p ~/.config/fabric/contexts

# Copy your TELOS doc as a Fabric context
cp "$HOME/04 Notes/002 - Project Thelos/personal_telos.md" ~/.config/fabric/contexts/telos
```

Now you can use it with any pattern:

```bash
pbpaste | fabric --context telos --pattern summarize
pbpaste | fabric --context telos --pattern write_essay
pbpaste | fabric --context telos --pattern extract_wisdom
```

---

### Step 2: Create TELOS-Specific Fabric Patterns

Create custom patterns that work with the TELOS methodology.

#### Pattern: `telos_align` — Check if something aligns with your TELOS

```bash
mkdir -p ~/.config/fabric/patterns/telos_align
cat > ~/.config/fabric/patterns/telos_align/system.md << 'EOF'
# IDENTITY and PURPOSE

You are a TELOS alignment analyst. Your job is to evaluate whether a given idea, project, or task aligns with the user's TELOS framework (Problems → Mission → Narratives → Goals → Challenges → Strategies → Projects).

# STEPS

- Take the user's input (an idea, project, or task).
- Map it against the user's TELOS context.
- Identify which Problem it addresses.
- Identify which Mission it supports.
- Identify which Goal it contributes to.
- Identify which Challenge it helps overcome.
- If it doesn't align with any TELOS element, flag it as "misaligned."

# OUTPUT INSTRUCTIONS

- Only output Markdown.
- Use the following format:
  - **Alignment:** Aligned / Partially Aligned / Misaligned
  - **Problem:** [Which problem it addresses]
  - **Mission:** [Which mission it supports]
  - **Goal:** [Which goal it contributes to]
  - **Challenge:** [Which challenge it helps with]
  - **Notes:** [Any additional observations]
- Be direct and honest. Do not sugarcoat misalignment.

# INPUT

INPUT:
EOF
```

Usage:
```bash
echo "Build a new feature for my app" | fabric --context telos --pattern telos_align
```

---

#### Pattern: `telos_strategy` — Generate strategies from your challenges

```bash
mkdir -p ~/.config/fabric/patterns/telos_strategy
cat > ~/.config/fabric/patterns/telos_strategy/system.md << 'EOF'
# IDENTITY and PURPOSE

You are a strategic advisor using the TELOS framework. Your job is to take a challenge from the user's TELOS document and generate actionable strategies to overcome it.

# STEPS

- Read the user's TELOS context to understand their full picture.
- Take the specific challenge they mention.
- Generate 3-5 concrete, actionable strategies.
- For each strategy, include:
  - The strategy name
  - Specific steps to execute
  - Expected outcome
  - How it maps back to their Mission and Goals

# OUTPUT INSTRUCTIONS

- Only output Markdown.
- Use numbered lists for strategies.
- Use bullet points for steps within each strategy.
- Be specific and actionable. No vague advice.

# INPUT

INPUT:
EOF
```

Usage:
```bash
echo "C1: I'm super stressed at work and never have time to work on SOSS" | fabric --context telos --pattern telos_strategy
```

---

#### Pattern: `telos_journal` — Write a TELOS-aligned journal entry

```bash
mkdir -p ~/.config/fabric/patterns/telos_journal
cat > ~/.config/fabric/patterns/telos_journal/system.md << 'EOF'
# IDENTITY and PURPOSE

You are a TELOS journal assistant. Your job is to help the user write journal entries that connect their daily experiences back to their TELOS framework.

# STEPS

- Take the user's daily notes or thoughts.
- Reflect them through the lens of their TELOS context.
- Identify which Goals were advanced today.
- Identify which Challenges were faced or overcome.
- Note any new Problems, Ideas, or Insights that emerged.
- Suggest one action for tomorrow that aligns with their Mission.

# OUTPUT INSTRUCTIONS

- Only output Markdown.
- Use the following format:
  ## Today's Reflection
  [Summary]
  
  ## TELOS Alignment
  - Goals Advanced: [...]
  - Challenges Faced: [...]
  - New Insights: [...]
  
  ## Tomorrow's Focus
  [One aligned action]
- Keep it concise and honest.

# INPUT

INPUT:
EOF
```

Usage:
```bash
echo "Had a rough day at work but managed to sketch out the SOSS dashboard UI" | fabric --context telos --pattern telos_journal
```

---

#### Pattern: `telos_review` — Weekly TELOS review

```bash
mkdir -p ~/.config/fabric/patterns/telos_review
cat > ~/.config/fabric/patterns/telos_review/system.md << 'EOF'
# IDENTITY and PURPOSE

You are a TELOS weekly review assistant. Your job is to help the user review their week against their TELOS framework and identify course corrections.

# STEPS

- Take the user's weekly summary or journal entries.
- Review against their TELOS context.
- Assess progress on each Goal.
- Identify which Challenges are still blocking progress.
- Flag any drift from the Mission.
- Suggest priorities for next week.

# OUTPUT INSTRUCTIONS

- Only output Markdown.
- Use the following format:
  ## Weekly TELOS Review
  
  ### Goal Progress
  - G1: [status]
  - G2: [status]
  - ...
  
  ### Blocking Challenges
  - [Challenge + suggested workaround]
  
  ### Mission Drift Check
  - [Assessment]
  
  ### Next Week's Top 3 Priorities
  1. [...]
  2. [...]
  3. [...]
- Be direct. Highlight misalignment clearly.

# INPUT

INPUT:
EOF
```

Usage:
```bash
cat weekly-notes.md | fabric --context telos --pattern telos_review
```

---

### Step 3: Common TELOS + Fabric Workflows

#### Analyze content through your TELOS lens

```bash
# Read an article and see how it relates to your mission
fabric --scrape_url "https://example.com/article" | fabric --context telos --pattern extract_wisdom

# Watch a YouTube video and extract wisdom relevant to your goals
fabric -y "https://youtube.com/watch?v=VIDEO_ID" | fabric --context telos --pattern extract_wisdom
```

#### Generate projects from your TELOS challenges

```bash
# Turn a challenge into a project plan
echo "C2: I'm having trouble building the UI/UX for SOSS" | fabric --context telos --pattern telos_strategy -o "$HOME/04 Notes/000 Inbox/ui-ux-strategy.md"
```

#### Daily TELOS check-in

```bash
# Quick morning alignment check
echo "Today I plan to: work on SOSS backend, reply to emails, go to the gym" | fabric --context telos --pattern telos_align
```

#### Update your TELOS document with Fabric

```bash
# Use Fabric to help refine your TELOS doc
cat "$HOME/04 Notes/002 - Project Thelos/personal_telos.md" | fabric --pattern improve_prompt -o "$HOME/04 Notes/000 Inbox/telos-improved.md"
```

---

### Step 4: Quick Reference — TELOS + Fabric

| What you want to do | Command |
|---------------------|---------|
| Check if an idea aligns with TELOS | `echo "idea" \| fabric --context telos --pattern telos_align` |
| Generate strategy for a challenge | `echo "challenge" \| fabric --context telos --pattern telos_strategy` |
| Write a TELOS journal entry | `echo "daily notes" \| fabric --context telos --pattern telos_journal` |
| Weekly TELOS review | `cat weekly.md \| fabric --context telos --pattern telos_review` |
| Analyze content through TELOS lens | `fabric --scrape_url "url" \| fabric --context telos --pattern extract_wisdom` |
| Improve your TELOS doc | `cat personal_telos.md \| fabric --pattern improve_prompt` |

---

## Quick Reference

| Command | Description |
|---------|-------------|
| `fabric --setup` | Initial setup |
| `fabric --listpatterns` | List all patterns |
| `fabric --listmodels` | List all models |
| `fabric --listvendors` | List all AI vendors |
| `fabric --updatepatterns` | Update patterns from repo |
| `fabric -p <pattern>` | Run a pattern |
| `fabric -p <pattern> -s` | Stream output |
| `fabric -p <pattern> -o file.md` | Save to file |
| `fabric -p <pattern> -c` | Copy to clipboard |
| `fabric -y <url>` | YouTube transcript |
| `fabric -u <url>` | Scrape URL to markdown |
| `fabric --serve` | Start REST API server |
| `fabric --dry-run` | Preview prompt |
| `pbpaste \| summarize` | Summarize clipboard (with alias) |

---

## File Locations on macOS

| What | Path |
|------|------|
| Patterns | `~/.config/fabric/patterns/` |
| Contexts | `~/.config/fabric/contexts/` |
| Sessions | `~/.config/fabric/sessions/` |
| Config file | `~/.config/fabric/.env` |
| Shell config | `~/.zshrc` |

---

## Resources

- **GitHub:** https://github.com/danielmiessler/Fabric
- **DeepWiki:** https://deepwiki.com/danielmiessler/Fabric
- **Docs:** https://github.com/danielmiessler/Fabric/tree/main/docs
- **YouTube:** Search "fabric ai" on YouTube
- **CHANGELOG:** https://github.com/danielmiessler/Fabric/blob/main/CHANGELOG.md
