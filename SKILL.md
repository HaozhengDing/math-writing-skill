---
name: math-writing
description: Write and organize mathematics the way readable human textbooks and papers do. Two jobs — (1) turn existing notes, drafts, partial proofs, or multiple sources into one coherent finished text; (2) write new mathematical content to a specified style. English output by default. Carries genre skeletons, discourse-move rules, an anti-slop blacklist (including LLM over-encapsulation), bad→good pairs, and a review rubric. Not for pure LaTeX/typesetting fixes, and not for non-mathematical writing.
when-to-use: The user asks to "write this up", "organize these notes into a chapter/lecture note/paper", "turn this into a proof", "this proof is unclear, rewrite it", "write a section about …", or supplies raw mathematical material (notes, drafts, fragmentary proofs, several sources) and wants a finished document. Also for a readability review of mathematics already written. Chinese phrasings that should also trigger this skill — 把这些材料整理成文 / 写成讲义 / 这段证明讲不清楚，重写一下 / 按这个风格写数学 / 写一份关于…的数学介绍. Not for pure LaTeX layout problems or reference formatting.
---

# Mathematical Writing

Turn mathematics into something a human will actually read to the end. Two things must hold at once: **readability** and **mathematical correctness**. Neither may be traded for the other.

## Stance

1. **Style rules must be operational.** "Clear, rigorous, elegant" are adjectives, not rules. Every rule in this skill has the form **situation → action → counter-example → checkable signal**. If a rule cannot be pointed at a specific sentence, it does not belong in the output.
2. **Correctness outranks style.** Mathematical correctness is a gate, not a bonus. No stylistic rule may cost correctness, completeness, or fidelity.
3. **Rewriting is not re-doing the mathematics.** When organizing existing material, the mathematical content does not change. See *Fidelity constraints*.
4. **Prose carries the logic; formulas carry the computation.** A pile of formulas is not mathematical writing. Every displayed formula is answerable to a sentence.
5. **Use the field's own language.** Three distinct failures, all documented in `references/slop-blacklist.md`:
   - **S16 — over-encapsulation**: inventing abstractions the mathematics does not need.
   - **S17 — process narration**: writing about the research instead of the mathematics.
   - **S18 — disciplinary register leakage**: computer-science vocabulary where mathematical language belongs.

   All three are surface symptoms of one habit: **describing a process where a relation should be stated.**

**Output language: English by default.** If the source material is in another language, translate it and write in English. Do not keep a parallel register. Rules specific to writing mathematics *in Chinese* live in `references/style-rules.md` §Chinese and are pulled in only on request.

---

## Triage first

Classify the job before doing anything. The workflows differ.

| Type | Trigger | Main risk |
|---|---|---|
| **B — Organize** | Several sources or messy notes; "write this up", "整理成文" | Structure is scattered; notation collides; you silently change the mathematics |
| **A — Rewrite** | One existing text; "this is unclear", "rewrite this proof" | Changing the mathematics while polishing |
| **C — Generate** | No source text; write from a topic or specification | Inventing motivation, inventing citations, skipping steps |
| **D — Review** | Only asked to find problems | Picking at wording while missing the mathematics |

**Type B is the hardest and the most common.** It gets the full workflow below. A, C, D reuse its parts.

---

## Workflow B — organizing existing material into a finished text

Do not start writing until steps 1–5 are done. Writing first produces text that is structurally correct and unreadable.

### Step 0 — Fix the reader and the genre

Two things must be settled. If they are not derivable, **ask** — do not silently assume.

- **Reader's background.** Undergraduate / graduate / fellow specialist. This decides what may be omitted and what must be spelled out.
- **Genre and length.** Textbook section, lecture note, paper, survey, solution write-up. The skeletons differ completely — see `references/genres.md`.

If the user supplies a sample ("write it like this"), **read the sample first** and reverse-engineer its skeleton and phrasing habits. The sample outranks this skill's defaults.

### Step 1 — Inventory the mathematics

List what the material actually contains, as mathematical items, not as sections:

- definitions introduced
- statements (lemmas, propositions, theorems) — with their hypotheses
- proofs present, and how complete each is
- examples, counterexamples, computations
- results *used* but not proved

Keep this as a working list. Everything downstream is checked against it.

### Step 2 — Dependency analysis

Work out which item depends on which. Produce a partial order, not a linear list.

The output document must respect this order. A definition must appear before its first use; a lemma before the result that cites it. Human exposition is rarely a straight line — Halmos: *"The plot of an exposition is rarely a straight line."*

### Step 3 — Conflict detection

The step most often skipped, and the one that causes the worst damage. Scan for:

- **Notation collisions** — one symbol for two objects, or two symbols for one object. Both are common across separately written sources.
- **Contradictory statements** — two sources asserting incompatible things.
- **Duplicates** — the same lemma proved twice, possibly differently.
- **Register drift** — different levels of formality, different conventions for the same field.

Log every conflict. Some are resolved by unification; some must be surfaced to the user.

### Step 4 — Gap marking (do not fill)

Mark incomplete arguments. **Do not generate a plausible proof to fill a hole.**

This is the single most damaging thing an LLM does in this task. A fabricated proof in a document that otherwise looks finished is worse than a visible gap, because the gap is honest and the fabrication is not.

Mark each gap explicitly, in the text, in a form the user can find.

### Step 5 — Structure design

Lay out the document before writing prose:

- each section's **function** — not its title, but what problem it solves for the reader
- the **motivation point** for each concept — what concrete difficulty it comes from
- the **dependency order** from step 2
- a **notation table** — which symbols, introduced where, at what level

Show this outline to the user (or at least print it in the reply) before expanding. **Skipping this step is what produces "structurally correct but unreadable" text.**

### Step 6 — Write, applying the discourse moves

Work through `references/style-rules.md`. If you remember only three rules, remember these — they carry most of the readability:

1. **Motivation before definition.** Give the difficulty first, then the definition, then an example.
2. **Strategy paragraph before proof.** Open a proof with 1–3 sentences on the overall route, then go into detail.
3. **Every displayed formula gets a sentence.** After each display, prose saying what it says, why it holds, or why the next step follows.

### Step 7 — Deliver with the three tables

Never hand over a reorganized document without them:

- **Notation change table** — what was renamed to what.
- **Gap list** — every place the argument is incomplete.
- **Suspected-error list** — mathematical problems found in the source material.

And state the structural decisions you made, and where you **deliberately left** source ambiguity alone because resolving it would have changed the mathematics.

---

## Workflow A / C / D (short forms)

**A — Rewrite.** Run steps 0, 1, 6, 7. Establish exactly what the existing text claims before touching it; the claim is the invariant. Deliver the suspected-error list even when not asked.

**C — Generate.** Run steps 0, 5, 6, then the self-check. Extra risks: invented motivation and invented citations. If you cannot find a real motivation for a concept, **you do not understand it well enough yet — go and find out, do not invent one.** Never cite a reference you have not verified; write "citation needed here" instead.

**D — Review.** Use `references/rubric.md`. Do not rewrite. Report located problems with the rule they violate, ranked — and check the mathematics independently rather than assuming it is right because the prose reads smoothly.

---

## Fidelity constraints (types A and B)

Where this task goes wrong:

- **Do not change the mathematics.** Hypotheses, conclusions, and the substance of proofs stay as they are.
- **Do not silently fix mathematical errors.** Preserve the source as written and list the problem under *suspected errors*.
- **Notation changes require a mapping table.** Unifying notation is a large readability win, but the user has to know what became what.
- **Do not write content that "ought to be there".** If a proof is missing, mark it. Do not generate one that looks plausible.
- **Do not invent citations.** Look them up, or say the citation is needed.

---

## Self-check before delivery

Run these mechanically. Hitting one is not automatically wrong, but **every hit must be consciously kept or fixed** — none may pass unnoticed.

- Blacklist phrase hits (`references/slop-blacklist.md` §Banned words).
- **Verbosity substitutions** (`due to the fact that`, `in order to`, `a number of`, …) — deterministic mappings, no judgement needed.
- **Over-encapsulation pass** (S16): list every term the document defines, names, or declares a macro for. For each, run the four tests — standard name for *this meaning*? used more than once? does removing it break a proof? is it standard *in this field, in this sense*? Any term failing all four is packaging, not mathematics.
  - Grep `\DeclareMathOperator` and `\newcommand` for non-standard names — a macro declared for a coined term is a commitment to it.
  - If the project keeps its own vocabulary file, apply it — see `references/terminology-audit.md` §6.
- **Disciplinary register pass** (S18): grep `input`, `output`, `data`, `setup`, `channel`, `mechanism`, `robust`, `implement`, `tool`, `default`, `process` (noun). Repair by naming the mathematical objects — this is a restructure, not a synonym swap. Expected scale is small (≈5 per 1776 lines); expect false positives (`efficient`, `description`, `\texorpdfstring`, `\begin{array}`).
- Logical symbols in running prose: `∴ ∵ ∀ ∃ ⇒`.
- Sentences beginning with a symbol; symbols used as verbs.
- Colon before a displayed formula.
- Does every `definition` have a motivation sentence before it?
- Does every `proof` open with strategy wording?
- Does every displayed formula have an explanatory sentence after it?
- Notation: is every introduced symbol used? Is any object carrying two symbols?

**Reverse check, equally important.** Cutting slop tends to leave the text thin. Against rubric **G7 Content sufficiency**, ask: are there enough examples, counterexamples, applications, and boundary cases? A previous A/B test found this skill's output beat the default on discourse moves and *lost* on content density. Stylistic discipline must not cost content.

---

## Independent review

**Do not grade your own text.** Writers cannot see their own style problems.

- If subagents are available: dispatch one with `references/rubric.md` and the text only. Do not give it your reasoning — it will be persuaded by it.
- Otherwise switch roles explicitly: set the draft aside, then read it as someone encountering the material for the first time, asking of each paragraph "what is this saying, and why is it here?"

Grade with the rubric. **A G0 failure fails the whole document** and style scores are not counted.

---

## Reference files (load as needed, not all at once)

| File | Contents | When |
|---|---|---|
| `references/style-rules.md` | Discourse moves M1–M16, syntax rules H1–H10, notation, Chinese appendix | Before writing; step 6 |
| `references/genres.md` | Skeletons: textbook section, lecture note, paper, survey, solutions, organizing material | Step 0; step 5 |
| `references/slop-blacklist.md` | Anti-patterns S1–S18 (S16 over-encapsulation, S17 process narration, S18 CS register), banned-word lists, verbosity substitutions | Self-check |
| `references/pairs.md` | Bad→good pairs | Before writing; whenever unsure how a passage should read |
| `references/exemplar.md` | **Positive checklist (P1–P23)** + verified clarity-adverb audit — extracted from two real, well-written notes by this group | Before writing; when the negative rules are not enough |
| `references/rubric.md` | Review rubric G0–G7 (G4 is the over-encapsulation audit) | Step 7; hand to the reviewer |
| `references/sources.md` | Provenance, evidence grading (A/B/C), authoritative disagreements | When you need authority for a rule |
| `references/terminology-audit.md` | **Method** for auditing a project's own vocabulary: the four tests, rewrite directions, prevalence ranking | Setting up or running a terminology cleanup |

---

## Boundaries

- **Mathematical correctness is not this skill's job.** It can catch notation inconsistency, dangling references, and suspected skipped steps — it **cannot replace real verification**. For load-bearing results, verify numerically or symbolically, or have a human check.
- **Style is genre-dependent.** A paper may cite earlier results; a textbook must restate them in place. When rules conflict, the genre decides.
- **Rules are an iterable hypothesis, not settled fact.** `references/sources.md` grades every claim by evidence level, and records where authorities disagree with each other and with this skill. When the user says "this still reads wrong", add the case to `pairs.md` or `slop-blacklist.md` — do not just fix the one document.
- **Rules remove defects; they do not create insight.** Halmos held that "effective exposition is not a teachable art." He is not entirely wrong. Use this as a checklist against known failure modes, not as a substitute for knowing what you want to say.
