# math-writing

An agent skill for writing and organizing mathematics the way readable human textbooks and papers do.

Two jobs:

1. **Organize existing material** — turn notes, drafts, partial proofs, or several sources into one coherent finished text.
2. **Write new mathematical content** to a specified style.

English output by default.

---

## The problem this addresses

Language models write mathematics competently and unreadably. The failures are consistent and recognizable:

| | What goes wrong | Looks like |
|---|---|---|
| **S16** | **Over-encapsulation** — inventing abstractions the mathematics does not need | `the two-layer localization framework`, an invented name for a standard condition |
| **S17** | **Process narration** — writing about the research instead of the mathematics | "the early experiments were not in vain" |
| **S18** | **Disciplinary register leakage** — computer-science vocabulary where mathematical language belongs | "the **input** weights … the **output** weights" |

Plus the ordinary ones: definitions with no motivation, proofs that open with `Let ε > 0` and no route, formulas with no prose, and clarity adverbs standing where a step should be.

All three signature failures are surface symptoms of one habit: **describing a process where a relation should be stated.**

---

## What is in it

```
SKILL.md                          the orchestrator: triage, the organizing workflow, self-check
references/
  style-rules.md                  discourse moves M1–M16, word choice W1–W8, syntax H1–H10,
                                  notation, person/tense/mood, Chinese appendix
  genres.md                       skeletons: organizing material, textbook section, lecture note,
                                  paper, survey, solution write-up
  slop-blacklist.md               anti-patterns S1–S18, greppable word lists, verbosity tables
  pairs.md                        bad → good pairs
  exemplar.md                     positive checklist P1–P23, and a verified adverb audit
  rubric.md                       review rubric G0–G7, for an independent reviewer
  terminology-audit.md            method for auditing a project's own coined vocabulary
  sources.md                      provenance, evidence grading, authoritative disagreements
```

Every rule has the form **situation → action → counter-example → checkable signal**. If a rule cannot be pointed at a specific sentence, it does not belong here.

---

## Installation

This is packaged in the [DeepSeek Harness](https://github.com/) skill format. Copy the directory into either skills location:

```bash
# user-level: available in every project
git clone https://github.com/<you>/math-writing-skill.git ~/.dsh/skills/math-writing

# or project-level
git clone https://github.com/<you>/math-writing-skill.git .dsh/skills/math-writing
```

The skill loads on demand: only its `name` and `description` occupy context until the model decides it is relevant.

The markdown is otherwise plain — the rules are readable and usable without any particular harness.

---

## Design notes

### Correctness is a gate, not a bonus

Rubric dimension **G0** (mathematical correctness) fails the whole document, and style scores are not counted when it fails. A fluent wrong proof is the most dangerous possible output.

### Fidelity constraints are stated explicitly

When organizing existing material: the mathematics does not change; gaps are **marked, not filled**; suspected errors are **listed, not silently corrected**; notation changes require a mapping table. Generating a plausible proof to fill a hole is the single most damaging thing a model does in this task — a visible gap is honest, a fabrication is not.

### Everything is graded by evidence

`sources.md` marks every claim **A** (quotation verified verbatim against a retained source), **B** (reported by an automated pass with a URL, not page-checked), or **C** (not verifiable). **Level C never enters the rule files.**

During development this caught two quotations attributed to a well-known blog that could not be found in the retained text at all. They were removed. Without evidence grading they would have acquired unearned authority.

It also caught a rule being **wrong**: the original guidance said "use *we*, avoid the passive". Halmos argues explicitly that avoiding *both* is better — *"even better is to avoid both passive voice and the use of 'we' through judicial use of imperative and indicative moods."* The rule was rewritten. **When a source contradicts a rule, the rule changes.**

### The rules were tested, not just written

A controlled A/B (same topic, same reader, same length) compared default model output against skill-guided output.

The honest result: **the default output was not slop.** It was mathematically correct and clearly structured. The skill's gains were local and enumerable — motivation ordering, the strategy paragraph before a proof, flagging the key idea — and it **lost on content density**: the default gave two counterexamples and three applications; the skill gave one.

That finding changed the skill. The rubric gained a **content sufficiency** dimension, and `SKILL.md` gained a reverse check, because cutting filler easily leaves the text thin.

**The wider conclusion**: the largest gains are in what models have no template for — organizing existing material, long-document consistency, fidelity — not in polishing wording on familiar topics.

### The positive checklist came from evidence too

`exemplar.md` was extracted from real, well-written research notes rather than constructed. Its headline finding is a measurement: a 1777-line paper containing **zero** occurrences of `clearly`, `obviously`, `it is easy to see`, `well known`, `straightforward`, or `routine`. That is direct evidence the discipline is achievable at scale, not an aspiration.

The same sweep produced a useful false positive — `trivial` occurs several times, always as the mathematical term (*trivial module*, *meets trivially*). The word list says so explicitly: **grep the word, judge the sense; never blanket-ban a word with a technical use.**

### Two passes, never one

Style and vocabulary are separable, and a document can pass one while failing the other. Run the terminology pass and the style pass **separately**, or a terminology fix will damage prose that was already good.

---

## Known limitations

- **Mathematical correctness is not this skill's job.** It can catch notation inconsistency, dangling references, and suspected skipped steps. It cannot replace real verification. For load-bearing results, verify numerically or symbolically, or have a human check.
- **Style is genre-dependent.** A paper may cite earlier results; a textbook must restate them in place. When rules conflict, the genre decides.
- **Rules remove defects; they do not create insight.** Halmos held that "effective exposition is not a teachable art." He is not entirely wrong. Use this as a checklist against known failure modes, not as a substitute for knowing what you want to say.
- **Provenance is incomplete.** Higham's *Handbook* was unavailable in full (paywalled); the Chinese-language normative literature is largely absent. Both are noted in `sources.md` §5.

---

## Contributing

The most valuable contribution is a **bad → good pair** from real material. `pairs.md` explicitly says: when something reads wrong, add the case there rather than another abstract clause to `style-rules.md` — paired examples execute far more reliably than rules.

Please keep the evidence grading honest: if you add a citation, say whether you read the source.

---

## License

MIT — see [LICENSE](LICENSE).
