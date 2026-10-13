# Terminology audit — a method for cleaning up a project's vocabulary

A procedure for finding and repairing **coined terminology** in a body of mathematical writing. Unlike the rest of this skill, this file is about **how to run an audit**, not about what the words should be.

If a project has its own vocabulary list, keep it in the project, not here — see §6.

---

## 1. Why a banned-word list does not work

The obvious approach — list the bad words, forbid them — fails for two independent reasons, both observed in practice:

**1. The same word is correct in one place and a coinage in another.**
`spectral flow` is standard in one field; `flow` used loosely for "the iterated action of a map" is a coinage. A word list must either ban `flow` (breaking the standard term) or permit it (missing the coinage). There is no setting of the list that works.

**2. The worst offenders look standard.**
A **standard word carrying a private meaning** passes the "does the field already have a name for this?" test trivially, because the field *does* have that word — it just means something else. In one audited corpus, a single such word accounted for more occurrences than all the obviously-invented terms combined, precisely because nobody questioned it.

**Therefore**: audit by **meaning, per occurrence**, using the tests below. Word lists are a starting point for the grep, never the verdict.

---

## 2. The four tests

Apply to every term the document defines, names, or declares a macro for.

| Test | Question | Fail means |
|---|---|---|
| **Standard-name** | Does the field already have a name for **this meaning**? | Use that name. |
| **Removal** | Delete the definition. Does any proof break? | It was packaging. |
| **Reuse** | Is it referenced more than once? | It was bookkeeping. |
| **Context** | Is this word standard *in this field, in this sense*? | A standard word with a private meaning is **worse** than a new word. |

A term should pass at least one of the first three, and **must** pass the context test outright.

---

## 3. The rewrite direction: write it out

The default repair is **not** "find a better name". It is **replace the name with the thing it names** — the inequality, the element form, the operator, the condition.

A name that must be decoded is a detour. A statement of the condition is the content itself.

### But do not overcorrect

Writing a condition out forty times is also bad. The distinction that resolves this:

- **A metaphor** ("the deep regime", "the harvest layer") must be decoded, and it imports intuition that may be **wrong** — a spatial metaphor for two ranges of one parameter suggests structure that is not there.
- **A transparent label** ("the range $c \le -a-1$", "nilpotency order", "the segment $G^{\ge\nu}$") can be read without a lookup, because it says what it is.

**Prefer names that announce their content over names that evoke it.** Either write the condition, or use a label that restates it. Stop naming it with a metaphor.

### The special case: a private meaning on a standard word

This is the hardest category, and it is **not** solved by deletion. A private label is tolerable **if its first use is immediately bound to an explicit mathematical object**:

> ✓ "For **the local case $|x| < 1$**, let $D$ be the open unit disc."
> ✓ "Throughout we work on the open unit disc."

> ✗ `\section{The local case}` … *the local case is treated in §4.*
> *(Local in what sense? On what domain? The reader reconstructs it from context — and reconstructs it wrong.)*

After a binding, every later use resolves to something the reader can see, and the word has become an **abbreviation for something stated** rather than a **label for something implied**.

**The general rule, which softens the anti-pattern usefully**: the target is not the elimination of every non-standard word — it is the elimination of every word **whose referent the reader must guess**.

---

## 4. Diagnostic signals — machine-checkable

1. **A declared macro for a non-standard operator.** `\DeclareMathOperator{\depth}{depth}` is a commitment to the coinage at the tooling level, and it makes the coinage much harder to remove later. Grep `\DeclareMathOperator` and `\newcommand`; check each name against the standard operator inventory (`\Hom`, `\Ext`, `\Tor`, `\rank`, `\soc`, `\rad`, …).

2. **A metaphor in a section title.** Titles are where coinages get legitimised: once the word is a `\section`, later mentions inherit its authority and stop being examined.

3. **A boxed "concept map" or arrow diagram built from coined nouns.** If you can draw the diagram but cannot state a theorem it encodes, the diagram is packaging.

4. **A summary whose content words are all coinages.** Apply the falsifiability test: *can this sentence be false?* If not, it says nothing.

5. **Self-justifying meta-commentary.** If a notation needs a defence paragraph ("this is not a notational game, but the coordinate system of the whole theory"), the notation is the problem.

---

## 5. Measuring prevalence — rank the work before doing it

A raw word list tells you *what* is non-standard. It does not tell you *where to start*. Counting does:

1. Extract the corpus to plain text.
2. For each candidate term, count occurrences **and the number of files it appears in**.
3. Sort by total occurrences.
4. **Check the counts for substring false positives before trusting them** — `efficient` contains `efficien`, `description` contains `script`, `\texorpdfstring` contains `string`, `\begin{array}` contains `array`, `mathtools` contains `tool`. A sweep returning dozens of hits per term is usually matching substrings.

Two things this buys you:

- **The largest single win is usually one term**, and it is usually in the *hardest* category (a standard word with a private meaning), because those are the ones nobody questions. Fixing it is worth more than the rest combined.
- **The file count matters more than the hit count.** A term with 400 hits in 3 files is a local problem; 90 hits in 45 files is a document-wide convention.

---

## 6. Running an audit on a real project

**Keep the project's own vocabulary list in the project**, not in this skill. A file at, e.g., `docs/terminology.md` recording, for each term: the verdict, the reason, and the agreed replacement. Then:

- The list stays correct as the project evolves; this skill does not need updating.
- The list can be versioned with the paper it applies to.
- Reviewers and collaborators can see the convention.

**Order of operations** — this matters:

1. **Structural pass** — the invented abstractions and their definitions.
2. **Terminology pass** — the private meanings on standard words, by binding or replacement.
3. **Register pass** — the borrowed-vocabulary sweep (`slop-blacklist.md` S18).

**Do not merge the passes.** A document can be well written and still need a terminology pass; mixing the two produces edits that fix terminology while damaging prose. See `exemplar.md` §"What these two documents establish".

---

## 7. Worked calibration

The most reliable way to calibrate an audit is a **before/after diff of the same document**: find a version that has been cleaned and the version it came from, diff them, and record what actually changed and why.

That is worth more than any amount of rule-writing, because it shows which rules the author actually applied and in what order. If no such pair exists, the next best thing is to produce one: clean a passage by hand, then compare it against the original.
