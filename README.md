# Evolving Skills for Claude Code

Most Claude Code skills are static (what sucks) they never improve no matter how many times you use them. These skills help to evolve your projects claude code skills through use, getting better the more you work with them.

## The Three Skills

| Skill | What it does |
|-------|-------------|
| **journey** | Creates session learning logs — the raw material for skill evolution |
| **wrap-up** | End-of-session engine that creates journeys, consolidates learnings, and evolves your skills |
| **reflect** | Periodic meta-review of whether the skill system itself is working well |

These three skills are the **engine**. Your own domain-specific skills (the ones you write for your project) are what actually get evolved. 

## How to Import

The idea is simple: add the evolving skills alongside your existing project skills. If you already have a `.claude/skills/` folder with your own skills, just drop these in next to them. That way `/wrap-up` and `/reflect` can see your project skills and evolve them based on what you learn during sessions.

```bash
# Clone this repo
git clone https://github.com/MeshJS/evolving-claude-skills.git

# Copy the skills into your project's existing .claude/skills/ folder
cp -r evolving-claude-skills/.claude/skills/ your-project/.claude/skills/
```

Your project should end up looking like this:
```
your-project/
  .claude/
    skills/
      journey/SKILL.md        # ← from this repo
      wrap-up/SKILL.md         # ← from this repo
      reflect/SKILL.md         # ← from this repo
      _patterns.md             # ← from this repo
      your-api-skill/SKILL.md  # ← your existing project skills
      your-auth-skill/SKILL.md # ← these are what get evolved
```

The evolving skills scan `.claude/skills/*/SKILL.md` to find all your project skills — so keeping everything in the same folder is what makes the system work.

## Usage

### Daily flow: `/wrap-up`

At the end of a coding session, run:

```
/wrap-up API Auth Refactor
```

This triggers the full learning loop:
1. Gathers all file changes from git
2. Creates a journey log at `.claude/journeys/`
3. Finds and consolidates any `<!-- LEARNING -->` notes left in skills during work
4. Analyzes which of your skills can be improved based on the session
5. Evolves those skills with new patterns, gotchas, and checklist items
6. Cross-pollinates shared patterns to `_patterns.md`
7. Updates the journey with a summary of what evolved

### Quick capture: `/journey`

For a quick learning capture without the full evolution process:

```
/journey Database Migration Fix
```

### Periodic review: `/reflect`

Every ~10 sessions, or when skills feel stale:

```
/reflect
```

This reviews all skills for staleness, bloat, drift, and structural issues — then proposes improvements.

## How It Works

The system mirrors natural learning:

```
Experience (coding session)
    → Awareness (learning notes during work)
        → Consolidation (/wrap-up)
            → Reflection (/reflect)
```

**During work**: Leave inline learning notes in any skill file:
```markdown
<!-- LEARNING 2026-02-08: The retry logic needs exponential backoff, not linear -->
```

**At session end**: `/wrap-up` absorbs these notes into the skill's proper text, creates a journey log, and evolves skills based on what was learned.

**Periodically**: `/reflect` steps back and evaluates whether the whole system is working — are skills actually improving? Is anything stale or bloated?

## What Gets Created

```
your-project/
  .claude/
    skills/
      _patterns.md              # Shared cross-cutting patterns (grows over time)
      your-skill/SKILL.md       # Your skills (evolved by wrap-up)
    journeys/
      2026-02-08-api-auth.md    # Session learning logs (created by wrap-up/journey)
```

## Why This Exists

Git commits track *what* changed. These skills track *why* and *what was learned*. Over time, your skills accumulate the institutional knowledge that makes Claude increasingly effective at working in your specific codebase.


Note*
The skills are for sure not perfect yet, which is the whole thing of it isnt it, start somewhere and become better. 
