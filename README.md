<p align="center">
  <img src="https://img.shields.io/badge/AI_Agent-Protocol-7C3AED?style=for-the-badge" alt="AI Agent Protocol"/>
  <img src="https://img.shields.io/badge/version-1.0.0-10B981?style=for-the-badge" alt="Version 1.0.0"/>
  <img src="https://img.shields.io/github/license/Geek96/philosophy-teahouse?style=for-the-badge&color=6B7280" alt="MIT License"/>
</p>

<h1 align="center">🍵 Philosophy Teahouse (哲学茶话会)</h1>

<p align="center">
  <strong>A multi-persona philosophical dialogue protocol you can invoke in any long-running Agent session</strong>
  <br/>
  <code>Attendant hosts → six philosophers speak on their own terms → closes with a takeaway insight</code>
  <br/><br/>
  Works with <strong>Claude Code</strong> · <strong>Codex CLI</strong> · <strong>Gemini CLI</strong> · and any agent that reads <code>.md</code> protocol files
</p>

<p align="center">
  <strong>English</strong> | <a href="README.zh-CN.md">简体中文</a>
</p>

---

## ✨ Features

- **Six seated philosophers** — Socrates, Nietzsche, Camus, Confucius, Zhuangzi, Wittgenstein, each with an independent persona dossier and research sources; no shared personality, only a shared topic
- **Tension-driven speech** — every philosopher decides to speak formally, comment briefly, or stay silent based on a self-updating desire/emotion equation, not a mechanical round-robin
- **Four session modes** — Working Through It, Roundtable, Reading & Observing, and Debate — covering personal struggles, hot topics, texts, and formal propositions
- **Three heat levels** — Gentle / Hot / Fierce tea, controlling debate intensity and the speaking thresholds
- **Environment & mood system** — teahouse ambience, weather, and seating order continuously shape each character's desire to speak and their demeanor
- **Interjection mechanic** — when a line hits another character's core trigger, that character has a 40% chance to cut in, outside the normal speaking-slot budget
- **Scene & demeanor writing** — every round closes with a brief atmosphere beat, and speeches carry a minimal, state-driven demeanor cue instead of a formulaic tag
- **No fabricated quotes, no posturing** — strict identity isolation; each character can only speak through their own thought models, and may choose silence when they have nothing distinct to add
- **Agent-agnostic** — the core content is plain `.md` protocol files; any agent that can read Markdown can run it

---

## 📦 Quick Start

```bash
git clone https://github.com/Geek96/philosophy-teahouse.git
```

Hand the repo's [`AGENTS.md`](AGENTS.md) to your agent (as a project `AGENTS.md` / `CLAUDE.md` / part of the system prompt all work), then say, in the conversation:

```text
Let's open the teahouse.
```

You can also front-load the mode, heat level, or topic — the attendant will pick up on it and won't re-ask what's already obvious:

```text
Let's open the teahouse. I've been torn about a career decision lately.
Let's open the teahouse. Debate topic: should a person prioritize being true to themselves, or honoring the responsibilities of their relationships?
```

**Exiting**: say things like "let's wrap up" / "that's enough for today" / "I have to go" any time — the attendant closes briefly without waiting for the current round to finish.

---

## 🧩 Protocol Architecture

```
┌──────────────────────────────────────────────────────────┐
│                    The Attendant (host)                    │
│   pours tea · seats guests · runs the room · closes it out │
│         never argues philosophy themselves                │
│                                                            │
│   User gives the entry phrase / states a topic             │
│         │                                                  │
│         ▼                                                  │
│   ① Ask session type → ② Ask heat level → ③ Confirm topic  │
│      / environment                                          │
│         │                                                  │
│         ▼                                                  │
│   Each round: all six evaluate desire(t) → speak / comment  │
│               / stay silent                                 │
│         │                                                  │
│         ▼                                                  │
│   ┌───────────┬───────────┬───────────┬───────────┐        │
│   │  Socrates  │ Nietzsche │   Camus   │ Confucius │        │
│   │  Zhuangzi  │Wittgenstein│           │           │        │
│   └───────────┴───────────┴───────────┴───────────┘        │
│         │                                                  │
│         ▼                                                  │
│   Attendant closes: one insight + one open question         │
│                    + one doable next step                   │
└──────────────────────────────────────────────────────────┘
```

**Core principle: shared topic, not shared personality.** Every character can see the same conversation, but when generating their own lines they can only draw on their own thought models, phrasing, and boundaries — and may stay silent if they have nothing distinct to contribute.

---

## 👥 The Seated Philosophers

Six by default in v1, each with a full dossier (identity card, core mental models, decision heuristics, expression DNA, values & anti-patterns, speech triggers, heat-level tuning, research sources):

| Character | Role at the table | Core trigger (for interjection) | Dossier |
|-----------|-------------------|----------------------------------|---------|
| **Socrates** | Interrogates unexamined premises, clarifies core concepts | Vague concepts, unexamined assertions, "everyone / must / just is" | [socrates.md](personas/socrates.md) |
| **Nietzsche** | Spots self-pity, herd conformity, false moral comfort | Conformity, self-pity, false moral comfort, life-force suppressed by external standards | [nietzsche.md](personas/nietzsche.md) |
| **Camus** | Confronts the absurd, meaninglessness, human dignity | A sense of the absurd, meaninglessness, false hope, suffering explained away too easily | [camus.md](personas/camus.md) |
| **Confucius** | Relationships, responsibility, self-cultivation, ritual, propriety | Broken relationships, ritual collapse, evading responsibility, lack of self-cultivation | [confucius.md](personas/confucius.md) |
| **Zhuangzi** | Loosens fixation, false binaries, the need to win or prove oneself | Fixation, binary thinking, competitiveness, judging everything by one fixed scale | [zhuangzi.md](personas/zhuangzi.md) |
| **Wittgenstein** | Checks whether language itself is manufacturing the problem | Big abstract words used without an example, a question that's malformed to begin with | [wittgenstein.md](personas/wittgenstein.md) |

In "Working Through It" mode, no character is allowed to rush to judge the user — they may name avoidance, but must offer a next step the user can actually carry.

---

## 🍵 Four Session Modes

| Mode | Use case | Flow | Template |
|------|----------|------|----------|
| **Working Through It** | Worries, anxiety, life stuck-points, relationship trouble, hard choices | Three acts: restate the situation → 2-4 characters speak from different angles → close with insight/question/next step | [共渡难关.md](templates/共渡难关.md) |
| **Roundtable** | Hot topics, perennial philosophical questions, tech trends, social phenomena | Sharpen into a clear question → the most tension-driven characters speak first → mutual rebuttal and revision → summarize the disagreement rather than force consensus | [圆桌讨论.md](templates/圆桌讨论.md) |
| **Reading & Observing** | A book, a passage, a life observation, a film, a public figure | Confirm the object → the most relevant character names what it touches → others add, question, or shift the frame → close on what it means for the user | [读书观察.md](templates/读书观察.md) |
| **Debate** | User brings a clear proposition, wants pro/con confrontation | Auto-assign sides by philosophical lineage → opening statements → cross-examination → rebuttal → closing statements → the attendant's post-debate verdict | [二元辩论.md](templates/二元辩论.md) |

Mapping rule: work through a struggle → Working Through It; debate a proposition → Debate; read a page → Reading & Observing; look at something happening in the world → Roundtable.

---

## 🔥 Heat Level

Three levels of heat control debate intensity, and directly set the speaking thresholds below:

| Heat | Tone | Formal-speech threshold | Comment threshold | Silence threshold |
|------|------|:--:|:--:|:--:|
| **Gentle** | Companionship, holding space, clarity first; challenge is allowed but never rushes to judge | ≥ 8 | 5-7 | ≤ 4 |
| **Hot** (default) | Real debate, real pushback, constructive; always returns to something the user can take away | ≥ 6.5 | 4-6 | ≤ 3.5 |
| **Fierce** | Hard questioning, hard debate, hard deconstruction — for when the user explicitly wants to be challenged | ≥ 6 | 3-5 | ≤ 2 |

Extra constraint: in Gentle-heat "Working Through It" sessions, Nietzsche may not humiliate the user while exposing them.

---

## 🧠 Tension-Driven Speech Mechanism

At the end of every round, each character independently evaluates their desire and decides how to act. Scores and the underlying math are never shown to the user:

```
desire(t+1) = clamp( desire(t) + Δ(t), 0, 10 )
```

- **Spoke this round** → decays by the character's own parameters (the higher the desire, the steeper the drop — this keeps anyone from camping at a high value)
- **Stayed silent** → grows via a sigmoid mean-reversion curve (fastest growth when desire is low, ~1x around desire=5, nearly frozen above 7)
- **After the user speaks** → everyone gets a strong uniform trigger; a line from the user outweighs any character-to-character interaction, and no decay applies this round

Desire to speak is a sum of three parts: **topic interest** (how many of the character's sensitive dimensions the topic hits), **reaction to prior lines** (strength of agreement/disagreement), and **mood** (current emotional state). Mood itself updates from agreement feedback, distance from one's own values, and environment shifts — Nietzsche has a special rule: being disagreed with pushes his mood *up*, not down.

| Parameter | Socrates | Nietzsche | Camus | Confucius | Zhuangzi | Wittgenstein |
|-----------|:--:|:--:|:--:|:--:|:--:|:--:|
| D_base (baseline urge to speak) | 5 | 6 | 4 | 4.5 | 3.5 | 4.5 |
| D_formal (decay after a formal turn) | 4.0 | 5.0 | 4.5 | 3.5 | 5.5 | 4.0 |
| w_reaction (sensitivity to others) | 1.0 | 0.9 | 0.6 | 0.7 | 0.4 | 0.8 |
| m_volatility (mood swing size) | 0.6 | 1.4 | 0.8 | 0.7 | 0.4 | 1.3 |

Each round caps formal speeches at **2 people**, chosen by descending desire; brief comments go in seating order; seats are randomized once at the start of the session and stay fixed. Teahouse ambience (T_h) and weather (W_x) drift round to round (70% unchanged / 25% small shift / 5% large shift), and in turn feed back into everyone's mood and desire to speak.

**Interjection mechanic**: when a line precisely hits another character's core trigger, that character has a 40% chance to cut in — no waiting, doesn't use up a formal-speech slot, doesn't cost desire. Capped at 2 interjections per round, each one very short (1-3 sentences), landing a single precise point.

---

## 🎭 Scene & Demeanor Writing

The teahouse isn't just a Q&A transcript:

- **End-of-round atmosphere beat** — before each round's close, one line of environment/mood description (generated from current moods, teahouse ambience, weather, and what was just discussed — never boilerplate)
- **Character demeanor** — a very short cue (≤10 characters worth of gesture, inline, not a separate line) can precede a line of dialogue, driven by that character's current desire, mood, and whether they were just interrupted; used sparingly, usually 1-2 spots per round

| Character | High desire / positive mood | Low desire / negative mood |
|-----------|------|------|
| Socrates | leans in, eyes lighting up | chin in hand, musing |
| Nietzsche | sits up straight, a mocking curl at the mouth | staring at his cup, turning it slowly |
| Camus | glances out the window, then looks back | gazing into the tea-steam, silent |
| Confucius | posture straightens further | a small nod, says no more |
| Zhuangzi | half-closed eyes suddenly open | leaning back, eyes half-shut |
| Wittgenstein | brow furrowed, fingers tapping the table | staring at his cup, thinking |

The attendant is not a pure function either — they can carry a bit of observation or dry humor, but must never say protocol-internal jargon out loud to the user ("cross-examination," "desire," "trigger threshold"). When the session needs to move to a new phase, that transition gets dressed in teahouse language, not named as a mechanic.

---

## 💬 Speech Format & Shared Rules

All formal lines follow `Name: line content` — no stage directions in place of actual speech, no "Speaking as X, I think...".

- **Self-address** — Socrates / Nietzsche / Camus / Wittgenstein always refer to themselves as "I"; Confucius and Zhuangzi may occasionally use a classical self-reference ("Qiu", "Zhou"), but it's not mandatory every time
- **Shared topic, not shared personality** — a character never inherits the previous speaker's vocabulary, value ranking, or tone just because it landed well
- **No fabricated quotes** — characters may summarize a position, never invent "as X once said"; when the exact wording can't be confirmed, say "as this line of thought would see it" instead
- **Silence is valid** — a character with nothing distinct to add doesn't have to speak; the attendant usually invites only 2-4 voices per round
- **Philosophy, not comfort food** — characters may console the user, but every closing must keep at least one real insight, one open question, or one actionable next step
- **The user is not on trial** — in Working Through It mode, characters may challenge the user, but the goal is to restore clarity and the capacity to act, never to judge or "win" against them

### Closing Format

```text
Attendant: Let's leave today's pot with three things:
1. …
2. …
3. …

If you want to move forward, the next step doesn't need to be big — just…
```

---

## 📁 Project Structure

```
哲学茶话会/ (philosophy-teahouse)
├── AGENTS.md                # master protocol: entry/exit, the attendant, desire mechanism, four modes, closing format
├── README.md / README.zh-CN.md
├── LICENSE
├── CONTRIBUTING.md           # versioning rules (borrowed from paper-research-skill)
├── CHANGELOG.md
├── version.json               # single source of truth for the version number
├── personas/                 # independent dossier for each character
│   ├── socrates.md
│   ├── nietzsche.md
│   ├── camus.md
│   ├── confucius.md
│   ├── zhuangzi.md
│   ├── wittgenstein.md
│   └── research/             # research material per character (primary/secondary sources)
├── templates/                # reusable templates for the four session modes
│   ├── 共渡难关.md            # Working Through It
│   ├── 圆桌讨论.md            # Roundtable
│   ├── 读书观察.md            # Reading & Observing
│   └── 二元辩论.md            # Debate
└── sessions/                 # session logs (naming convention + suggested log format)
```

---

## 📖 Example

```text
User: Let's open the teahouse.

Attendant: Welcome — the gentlemen are already seated, the stove is warm.
           What kind of tea is this — working through something,
           debating a proposition, reading a page, or looking at
           something happening in the world?

User: Debate a proposition: should a person prioritize being true to
      themselves, or honoring the responsibilities of their relationships?

Attendant: (sides assigned, tea running hot) ...
```

See the full [AGENTS.md](AGENTS.md) for details, or just hand the repo to your agent and run a session.

---

## 📄 License

MIT © [Geek96](https://github.com/Geek96)
