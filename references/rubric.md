# Review rubric

**For use by an independent reviewer** — a separate subagent, or yourself after switching roles.
**Principle**: writers cannot grade their own style problems.

Give the reviewer **the text and this rubric only**. Do not give your reasoning — the reviewer will be persuaded by it.

---

## Grades

| Grade | Meaning |
|---|---|
| **A** | At the level of good human textbook / paper prose |
| **B** | Readable, minor defects |
| **C** | Comprehensible but hard going |
| **D** | Clear structural or linguistic problems |
| **F** | Not acceptable |

---

## G0 — Mathematical correctness — **gate**

**A G0 failure fails the document. Style scores are not counted.**

- [ ] Statements complete (hypotheses, conclusions, quantifier order correct)
- [ ] No skipped steps: each "clearly / obviously" spot-checked and genuinely mechanical
- [ ] No unproved assertion presented as proved
- [ ] Cited theorems and lemmas exist and are stated consistently
- [ ] Counterexamples are actually counterexamples
- [ ] Zero unlabelled uncertainty (conjectures marked as conjectures)

**The reviewer must check the mathematics independently.** Do not assume it is right because the prose reads smoothly. A fluent wrong proof is the most dangerous possible output.

---

## G1 — Structure

- [ ] Genre skeleton complete (against `genres.md`)
- [ ] Dependency order respected (no tool used before it is introduced)
- [ ] Every concept has motivation → content → digestion
- [ ] Long proofs have a strategy paragraph and local signposting
- [ ] Paragraph breaks follow logic, not length

**A scattered structure caps the grade at C, however good the prose.**

---

## G2 — Discourse

- [ ] Motivation before each definition (M1)
- [ ] Two of example / non-example / intuition after each definition (M2)
- [ ] Strategy wording opens each proof (M3)
- [ ] Every displayed formula has an explanatory sentence (M5)
- [ ] Notation on demand, no dumping (M6)
- [ ] Special case before the general statement (M7)
- [ ] Counterexamples next to their claims (M8)
- [ ] Transitions carry information (M9)
- [ ] Closings present (M10)
- [ ] Key ideas flagged (M11)
- [ ] Construct-before-assert, not existence-then-properties (M13)
- [ ] No implicit final step (M14)
- [ ] Each hypothesis visibly used (M15)

---

## G3 — Language

- [ ] No empty opening
- [ ] No invented motivation
- [ ] Evaluations followed immediately by a specific reason
- [ ] "Clearly / obviously" spot-checked (three samples) and legal
- [ ] Person and tense consistent
- [ ] Verb strength matches argument strength
- [ ] No nominalization chains
- [ ] Terminology consistent throughout
- [ ] No metadiscourse roll-call
- [ ] Ending advances rather than recaps
- [ ] No sentence-initial symbols; no symbols used as verbs (H1, H2)
- [ ] No logical symbols as connectives in prose (H3)
- [ ] No colon before a display (H4)
- [ ] Verbosity substitutions applied (Part 5)

**Method**: sample five blacklist hits at random and judge each. **Do not read through and go by feel.**

### Register pass (S17) — does this text describe mathematics, or narrate the research?

Ask of every paragraph: **does this state a mathematical fact, or narrate the process of finding one?**

- [ ] No document meta-commentary (reading guides, "this note should be updated", self-description)
- [ ] No self-justification ("the early experiments were not in vain", "we do not do X for its own sake")
- [ ] No promotional section labels ("the harvest", "the frontier", "the engine is one lemma")
- [ ] No numbered revelation framing ("the first insight is …", "step 2 reveals …")
- [ ] Scope caveats stated as **mathematical facts about the theorem**, not as boilerplate disclaimers about the document
- [ ] No unfalsifiable slogans — every concluding sentence could in principle be false

**⚠️ Do not strip honest caveats.** A remark that a theorem is proved only for $n$ even is mathematics and must stay. The defect is the *register*, not the content: state the boundary as a fact about the result, not as a legal disclaimer about the note.

**⚠️ Genre-dependent.** This register is normal in a private working notebook. Establish what the document is for before flagging any of it. See `slop-blacklist.md` S17 counter-note.

### Disciplinary register pass (S18) — is this mathematics, or a data pipeline?

Grep for computer-science and engineering vocabulary, then judge each hit:

```
input    output    data    setup    channel    mechanism    implement
handle   feature   tool    store    default    robust       process (noun)
performance   valid   test
```

- [ ] No `input` / `output` describing a mathematical relation
- [ ] No `data` where **parameters** or **hypotheses** is meant
- [ ] No `setup` where **notation and conventions** is meant
- [ ] No `channel` where **map** or **transition** is meant
- [ ] No `robust` where **stable under** is meant
- [ ] No `performance` / `implement` / `tool` framing

**The root cause is structural, so the fix is a restructure, not a synonym.** The borrowed words appear where the text describes *what goes into a process and what comes out*, instead of *what the objects are and how they relate*. Repair by naming the mathematical objects — see the worked example in `slop-blacklist.md` S18.

**⚠️ Expected scale is small.** Measured on a 1776-line document: **five genuine instances**. This is a polish pass, not a rewrite. Do not let it expand.

**⚠️ Expect false positives.** `efficient` contains `efficien`; `description` contains `script`; `\texorpdfstring` contains `string`; `mathtools` contains `tool`; `\begin{array}` is LaTeX. **Check the actual word before flagging.**

**⚠️ Overloaded words**: `valid`, `test`, `check`, `process` (as a verb), `default` ("by default") all have legitimate mathematical uses. Flag only the software sense. See also the `trivial` caution in `slop-blacklist.md` Part 4.

---

## G4 — Terminology and abstraction ← the LLM signature failure

Run this as a **separate pass**, not as part of reading for style. See `slop-blacklist.md` S16.

**Step 1** — list every term the document defines, names, or declares a macro for. Also grep `\DeclareMathOperator` and `\newcommand`; a macro for a non-standard name is a commitment to a coinage.

**Step 2** — for each, run the four tests:

| Test | Question | Fail means |
|---|---|---|
| Standard-name | Does the field already have a name for **this meaning**? | Use that name |
| Removal | Delete the definition — does any proof break? | It was packaging |
| Reuse | Is it referenced more than once? | It was bookkeeping |
| Context | Is it standard *in this field, in this sense*? | A standard word with a private meaning is worse than a new word |

- [ ] Every named concept passes at least one test, and the context test outright
- [ ] No standard notion renamed
- [ ] No standard word given a private meaning (the hardest case to spot — it passes the standard-name test superficially)
- [ ] No **case named instead of stated** — a metaphor like "the deep regime" standing where the inequality $n \ge N$ belongs
- [ ] No **mnemonic standing where a formula belongs** — a name for a quantity that the reader has to compute with
- [ ] No framework / paradigm / pipeline register imported from adjacent fields
- [ ] The field's own verbs are used ("by compactness", not "via a finite reduction argument")
- [ ] No abstraction used to make a claim vaguer

**Step 3 — the falsifiability check on summaries.** For each abstract, summary, or "one-sentence takeaway": *can this sentence be false?* If every content word is a coinage, the sentence contains no checkable content and cannot be right or wrong. That is the failure, not a stylistic blemish.

- [ ] Every summary states something that could in principle be false
- [ ] Any boxed "concept map" or arrow diagram encodes a stateable theorem, not just a chain of nouns

**⚠️ Do not overcorrect.** Abstraction is mathematics. A document that names nothing is unreadable for the opposite reason. The question is whether each abstraction **carries content and gets used** — not whether abstraction exists. And note the distinction that resolves the tension: a **transparent label** ("the range $n \ge N$", "nilpotency order") is fine; a **metaphor** ("the deep regime") is not.

---

## G5 — Consistency

- [ ] Every introduced symbol is used
- [ ] No object carries two symbols
- [ ] Cross-references resolve
- [ ] Terminology-symbol correspondence consistent
- [ ] Numbering continuous

**This is the machine-checkable part.** Prefer a script or regex over the eye wherever possible.

---

## G6 — Reader fit

- [ ] Prerequisite assumptions match the target reader
- [ ] No concept used beyond the reader's range (or, if used, explained)
- [ ] Omitted steps are genuinely reconstructible by that reader
- [ ] Length appropriate to the genre

---

## G7 — Content sufficiency

> **Added 2026-10-11 after an A/B test**: this skill's output beat default model output on discourse moves and **lost on content density** — the default gave two counterexamples, three applications and two boundary notes; the skill gave one counterexample. The cause was that this rubric had no content dimension, so all attention went to phrasing.

- [ ] Enough examples for the key concepts (typical **and** boundary)
- [ ] More than one demonstration of the failure mechanism
- [ ] Real applications, not only definitions and theorems
- [ ] Boundary cases and counterexamples cover *different* reasons for failure
- [ ] Conclusions generalized, or connected to other results
- [ ] **No padding** — sufficient ≠ long (balances S10/S11)

**Note**: this dimension pulls against G3 (cutting filler). **Check both.** Slop removal easily leaves the text thin; stylistic discipline must not cost content.

---

## Output format

```
## G0 Mathematical correctness: pass / fail
(if fail, list problems with locations)

## Located problems
| Location | Rule | Problem | Suggestion |
|---|---|---|---|
| §2 before Def 2.3 | M1 | definition unmotivated | add: why we need … |
| §3 proof line 4 | S5 | "clearly" hides one step | expand, or cite Lemma 2.1 |
| §1 | S16 | "framework" wraps one compactness argument | state it directly |

## Mechanical scan
- blacklist hits: N, of which M should change
- formulas with no explanation: K
- definitions with no motivation: J
- named concepts failing all three tests: L

## G4 abstraction audit
(list each named concept and its test results)

## Overall: A / B / C / D / F

## Three highest-value fixes, ranked
1. …
2. …
3. …
```

**The last section matters most.** Do not hand over fifty flat problems — give the top three by return. The writer needs to know what to fix first.

---

## Reviewer discipline

- **Do not let smooth prose excuse wrong mathematics.** Good writing and correct mathematics are separate facts.
- **Do not manufacture problems to seem thorough.** Rules are for judgement, not for filling in blanks. If the text is good, give it an A.
- **Do not rewrite.** The output is located problems and suggestions, unless rewriting was explicitly requested.
- Separate **must fix** (G0, structure) from **could fix** (word-level preference).
