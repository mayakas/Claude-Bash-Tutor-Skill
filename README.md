# Claude-Bash-Tutor-Skill
Claude Skill teaching bash from the ground up: 17 units, prompt basics through security and debugging. Every example runs live in a sandbox. Quizzes test understanding, not recall. Progress tracking follows the learner unit by unit.

# Bash Instructor

A [Claude Skill](https://www.anthropic.com/news/skills) that teaches bash and shell scripting. Claude works through a full curriculum one topic at a time, runs every example live instead of describing it, quizzes for real understanding, and tracks progress as the learner goes.

## Why this exists

Most "explain bash to me" conversations are one-shot: you ask, Claude answers, and that's it. Nothing carries over. No check on whether the explanation landed, no structured path from never having written a script to feeling comfortable with `sed`, `find`, and secure scripting. This skill gives Claude four things instead:

- a fixed **17-unit syllabus** (plus a cheat-sheet unit) to teach from, instead of improvising coverage each session
- a **teaching loop**: explain, demo live, learner tries it, quiz, feedback
- instructions to execute the learner's code in a sandbox and grade it against real output, instead of guessing whether it looks right
- a lightweight **progress tracker** so a multi-session course stays coherent

The curriculum follows the chapter structure of O'Reilly's *Bash Cookbook* (Albing, Vossen & Newham), a well-established sequence of shell topics. Every explanation, example, pitfall, and quiz question here is original writing, not reproduced from that book or any other.

## What's inside

| # | Unit | Covers |
|---|------|--------|
| 1 | Getting oriented | prompt, built-ins vs external commands, file info, quoting basics |
| 2 | Output and input | `echo`/`printf`, redirection, pipes, here-documents, `read` |
| 3 | Running commands | exit status, `&&`/`\|\|`, `$(...)`, backgrounding, error handling |
| 4 | Variables and parameters | export, positional params, `$@` vs `$*`, defaults, arrays |
| 5 | Conditionals, tests, and loops | `[ ]` vs `[[ ]]`, arithmetic, `for`/`while`/`until`, `case`, `getopts` |
| 6 | Searching text | `grep` flags, basic vs extended regex, filtering pipelines |
| 7 | Transforming text | `sort`, `uniq`, `cut`, `tr`, `wc`, `sed`/`awk` one-liners |
| 8 | Finding files | `find` predicates, `-exec` vs `xargs`, `locate` |
| 9 | Functions and reusable code | functions, `source`, `trap`, aliases vs functions |
| 10 | Dates and scheduling | `date` formatting, epoch time, date arithmetic, cron basics |
| 11 | Parsing real data | manual arg parsing, CSV/field parsing, `read` into arrays |
| 12 | Writing secure scripts | `$PATH` hygiene, `mktemp`, input validation, avoiding leaks |
| 13 | Portable and advanced scripting | POSIX portability, process substitution, `/dev/tcp`, logging |
| 14 | Customizing your shell | `PS1`, `$PATH` management, startup files, history options |
| 15 | Everyday admin scripting | batch rename, `diff`/`patch`, archives, process checks |
| 16 | Working faster | history reuse, directory jumping, brace expansion |
| 17 | Common mistakes & debugging | the classic novice bugs, `bash -x`, `set -e`/`-u` |
| 18 | Quick reference | cheat sheet: test operators, parameter expansion, `printf`, `set`/`shopt` |

Each unit file under `references/` is self-contained: a concept summary, a suggestion for how to teach it (usually a broken example first, since bugs stick better than rules), original worked examples, a common-pitfalls list, a bank of quiz questions with answers, and hands-on exercises. `references/00-curriculum-map.md` ties it together with suggested learning paths for different starting points: total beginner, already scripts a bit, interview prep, quick refresher.

## How the tutoring works

1. **Assess.** Claude asks about experience level and goal before picking a starting point, rather than defaulting to Unit 1 for everyone.
2. **Teach one topic at a time.** Explain why it matters, run the example live in a sandbox, show real output, give the learner something small to write, quiz it, then give specific feedback before moving on.
3. **Quiz for understanding, not recall.** Multiple-choice rounds, or flashcards for pure review, mix concept checks, "predict the output," "spot the bug," and realistic scenarios instead of definition lookups.
4. **Verify the work.** When a learner submits an exercise, Claude runs it instead of guessing whether it's correct, then walks through the actual error or output if something's wrong.
5. **Track progress.** A running checklist, mastered / in progress / not started, against the 17-unit list, shown again on request or at the start of a new session.

## Installation

This skill ships as one packaged file, **`bash-instructor.skill`**: a zip containing `SKILL.md` and `references/`.

- **Claude.ai (web/desktop/mobile):** open the skill file's card and click **Save skill** (requires your workspace to allow custom skills), or add it from Settings → Capabilities → Skills.
- **Claude Code / Claude Cowork:** drop the unpacked `bash-instructor/` folder into your skills directory (typically `~/.claude/skills/` or your project's `.claude/skills/`), or install the `.skill` file like any other packaged skill.
- **API / custom integrations:** upload it through the Skills API like any other skill package.

It needs no extra configuration. The skill works better when Claude has **code execution** available, since it runs examples and grades exercises for real, and reads better with an **interactive quiz UI** if your client supports one. Without either, it still works as plain-text Q&A.

## Usage

Talk to Claude the way you normally would. You don't need to name the skill. It triggers on things like:

```
teach me bash from scratch
quiz me on shell scripting
I want to get better at the command line
can you give me a structured review of bash fundamentals?
I'm prepping for a sysadmin interview, drill me on find/grep/sed
explain bash variables and quiz me on it
```

It doesn't trigger for "write me a script that does X." That's a coding request, and Claude writes the script instead of starting a lesson.

A typical first exchange:

> **You:** teach me bash, I've used the terminal a bit but never scripted
> **Claude:** asks a quick question or two about goals and level, then starts Unit 1 or wherever fits. Explains a concept, runs a live example showing a quoting bug in action, gives you a one-line task, checks your answer for real, then runs a short quiz before moving on.

## Repository structure

```
bash-instructor/
├── SKILL.md                              # orchestration: teaching loop, tone, rules
└── references/
    ├── 00-curriculum-map.md              # syllabus + suggested learning paths
    ├── 01-fundamentals.md
    ├── 02-io-basics.md
    ├── 03-executing-commands.md
    ├── 04-variables-and-parameters.md
    ├── 05-logic-and-loops.md
    ├── 06-searching-text.md
    ├── 07-transforming-text.md
    ├── 08-finding-files.md
    ├── 09-functions-and-reuse.md
    ├── 10-dates-and-scheduling.md
    ├── 11-parsing-data.md
    ├── 12-secure-scripts.md
    ├── 13-advanced-scripting.md
    ├── 14-customizing-bash.md
    ├── 15-admin-scripting.md
    ├── 16-working-faster.md
    ├── 17-common-mistakes.md
    └── 18-quick-reference.md
```

`SKILL.md` stays in context once the skill triggers. Each `references/*.md` file loads only when Claude is about to teach that specific unit, so context usage stays low even though the full curriculum is large.

## Shell detection gotcha

Sandboxed code-execution tools sometimes default to `/bin/sh` (`dash`) rather than `bash`. Dash mishandles or rejects bash-only syntax: arrays, `[[ ]]`, process substitution, `${var^^}`, and more. `SKILL.md` instructs Claude to confirm it's running real bash (`bash --version`) and to invoke `bash -c '...'` or `bash file.sh` instead of trusting a tool's default shell, so live demos don't produce wrong output. Worth knowing if you extend this skill with your own examples in a different environment.

## Customizing / extending

- **Add a unit:** create `references/19-your-topic.md` following the existing unit format (concept summary, teach-it-this-way, examples, pitfalls, quiz bank, exercises), then add a row to `00-curriculum-map.md`.
- **Add quiz questions:** append to a unit's "Quiz bank" section. Claude draws from these and generates variations in the same style, so a few good examples go a long way.
- **Change the tone or pacing:** edit the "Tone and pacing" section of `SKILL.md` directly.
- **Retarget the curriculum:** the unit files don't depend on each other's exact content, so reordering, merging, or dropping units in `00-curriculum-map.md` doesn't require touching the rest.

## Limitations

- This is a teaching skill, not a reference manual. For a quick syntax lookup, Unit 18's cheat sheet works better than starting a lesson.
- Progress tracking lives in the conversation, not in persistent storage. A new conversation starts fresh unless you tell Claude where you left off, or it's visible earlier in the same chat.
- Examples target modern GNU bash 5.x unless a unit calls out a platform difference. Several units flag common Linux, macOS, and BSD divergences, for example `date` and `sed -i`.

## Acknowledgments

Curriculum sequencing follows the chapter organization of *Bash Cookbook* (O'Reilly, Albing/Vossen/Newham). Every explanation, example, pitfall, and quiz question in this skill is original.

