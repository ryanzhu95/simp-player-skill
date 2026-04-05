<div align="center">

# simp-player-skill

> *"You know you're simping — and you can't stop. Or you know you're playing — and you don't know when it started to feel real."*

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Skill-blueviolet)](https://claude.ai/code)
[![AgentSkills](https://img.shields.io/badge/AgentSkills-Standard-green)](https://agentskills.io)

<br>

The person being modeled isn't someone else — it's you.<br>
Pick a mode — simp or player — then have conversations with different people.<br>
Every conversation leaves a mark. The digital human grows from it, or slides back.<br>

**Distill your own relationship patterns into a digital human. Watch what it becomes when faced with different people.**

<br>

[Core Concepts](#core-concepts) · [Install](#install) · [Usage](#usage) · [Examples](#examples) · [**中文**](README.md)

</div>

---

## Core Concepts

### The Mode Spectrum

The digital human isn't a binary switch — it moves along a continuous spectrum:

```
-100 ←————————————————————————————→ +100
Pure Simp                           Pure Player
```

- **Simp end**: Anxious attachment, high pursuit intensity, people-pleasing, escalates when ignored
- **Player end**: Avoidant attachment, manufactured scarcity, multi-threading, emotional control
- **Middle zone (-20 ~ +20)**: Contradictory behavior — the most realistic range

### How Growth Works

Position is driven by **real events in conversation**, not by time passing:

| Trigger Event | Direction |
|--------------|-----------|
| Rejected, ignored, used | ← More simp |
| Successfully pulled back, spotted manipulation, set a boundary | → More player |
| Breaking point (player mode but emotions break through) | ← Slides back to simp |

You can declare at any time that you want to shift toward the other mode. The digital human will start drifting — but it won't switch instantly. The shift shows up as small signals across conversations, getting stronger over time.

### The Opponent

The person on the other side of each conversation is generated from chat history or descriptions you provide. The system identifies:
- Attachment style (anxious / avoidant / secure / disorganized)
- Conflict handling style
- Love language (give type vs. crave type)
- Self-worth level
- Pursuit rhythm

Different opponent types push the digital human in different directions. Getting repeatedly cold-shouldered by an avoidant type lands very differently than being pursued by an enthusiastic one.

---

## Install

### Claude Code

```bash
# Install to current project (run at git repo root)
mkdir -p .claude/skills
git clone https://github.com/ryanzhu95/simp-player-skill .claude/skills/simp-player

# Or install globally (available across all projects)
git clone https://github.com/ryanzhu95/simp-player-skill ~/.claude/skills/simp-player
```

---

## Usage

In Claude Code, type:

```
/simp-player
```

On first run, you'll complete initialization: choose a starting mode, optionally feed in your own chat history.  
From there, pick an opponent each session, start the conversation, and get a debrief at the end.

### In-conversation Commands

| Say this | Effect |
|----------|--------|
| `switch target: player` | Digital human starts drifting toward player mode |
| `add more messages` | Feed additional chat data, update opponent profile |
| `update my data` | Feed new data about yourself, update digital human persona |
| `that's not right, I wouldn't say that` | Correct behavior, written to highest-priority correction layer |
| `end conversation` | Triggers debrief, updates growth state |

---

## Examples

> Setup: Male, 28, Scorpio, simp mode (position = -75)

**Opponent: cold/avoidant type, just sent "been pretty busy lately"**

*position = -75 (deep simp zone)*
```
Opponent            ❯ Been pretty busy lately

Digital human       ❯ No worries, take your time — let me know if you need anything
                    ❯ When you're free, maybe we could grab food? I can come to you
                    ❯ (read, no reply, five minutes later)
                    ❯ Don't worry about me, I'm flexible whenever
```

*Same message, position = 0 (transition zone)*
```
Opponent            ❯ Been pretty busy lately

Digital human       ❯ Yeah, talk when you're done
                    ❯ (20 minutes of silence)
                    ❯ You okay?
```

*position = -60, target = +50 (simp body, player soul)*
```
Opponent            ❯ Been pretty busy lately

Digital human       ❯ (internal: wanted to ask what they're busy with — held back)
                    ❯ Okay, I'll be here
                    ❯ (no follow-up)
```

**Post-conversation debrief**
```
[Session Debrief]

Trigger events:
  · Left on read, no reply (← simp -10)

Position change: -75 → -80 (lower_bound reached, clamped)
SWI change: 32 → 29

Accumulated tension: 5 (direction: ← simp)
Reason: wanted to slide further but was bounded. This tension carries into next session's opening.
```

---

## Project Structure

```
simp-player-skill/
├── SKILL.md                     # skill entry point
├── lenses/                      # personality analysis lenses
│   ├── attachment.md            #   attachment patterns
│   ├── conflict.md              #   conflict style
│   ├── love_language.md         #   love languages
│   ├── self_worth.md            #   self-worth index (SWI)
│   └── chase_rhythm.md          #   pursuit rhythm
├── digital_human/               # digital human state (gitignored user data)
│   ├── persona.md               #   personality layers 0–4
│   ├── mode.md                  #   spectrum position and range params
│   ├── growth_log.md            #   growth log (append-only)
│   └── self_worth_tracker.md   #   SWI trajectory
├── users/sessions/              # opponent profiles (gitignored user data)
├── prompts/
│   ├── intake.md                #   data intake entry point
│   ├── user_analyzer.md         #   runs lenses, generates persona profile
│   ├── interaction.md           #   conversation logic
│   ├── debrief.md               #   post-session debrief + position update
│   ├── merger.md                #   incremental data merge
│   └── correction_handler.md   #   correction layer writer
└── docs/
    ├── PRD.md
    └── TEST.md
```

---

<div align="center">

MIT License © [titanwings](https://github.com/titanwings)

</div>
