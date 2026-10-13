# Style rules

Form: **situation → action → counter-example → checkable signal.**
A *checkable signal* is something a reviewer can point at in the text and say "done" or "not done" — not an impression.

---

## 1. Discourse moves

This is where the readability gap actually lives. The difference between human mathematical prose and default model output is mostly not word choice — it is whether these moves happen at all.

### M1 Motivate before defining
- **Situation**: about to introduce a concept, notation, or construction.
- **Action**: 1–3 sentences on *why it is needed* — from a concrete difficulty, a failed earlier approach, a question you want answered. Then the definition.
- **Counter-example**: `Definition 1.1. Let X be a set. If … then X is called a Y.` (Reader has no reason to care about Y.)
- **Signal**: every definition environment is preceded by non-empty prose naming a specific difficulty (not "this is important").

### M2 Justify the definition
- **Situation**: a definition has just been given.
- **Action**: immediately supply at least two of — (a) a concrete example; (b) a **non**-example or boundary case; (c) one sentence on what intuition it captures.
- **Counter-example**: definition, then straight into the next definition; examples deferred to a later chapter.
- **Signal**: between a definition and the next environment there is "for example", "but if … then not", "intuitively".

### M3 Strategy paragraph before proof
- **Situation**: starting a proof, especially one over ~5 lines.
- **Action**: 1–3 opening sentences giving the route: "We proceed in two steps: first … then …" / "The key is to reduce to …" / "Suppose not …". Then the details.
- **Counter-example**: the proof opens with `Let ε > 0. Take δ = …` — the reader does not know where this is going.
- **Signal**: strategy wording appears within the first three sentences of a `proof` environment.

### M4 Local signposting
- **Situation**: an independent technical step inside a proof.
- **Action**: one sentence before it saying what is being reached; one sentence after saying it has been reached. Long proofs stay navigable on this alone.
- **Counter-example**: twenty consecutive lines of computation with no landmarks.
- **Signal**: in proofs over ~15 lines, goal-setting and closing sentences recur at intervals.

### M5 Every formula is answerable to prose
- **Situation**: a displayed formula appears.
- **Action**: prose after it stating **what it says**, **why it holds**, or **why the next step follows**. At least one sentence.
- **Counter-example**: three `align` lines, then the next paragraph, with no text between.
- **Signal**: non-empty prose immediately follows each display (`\[ \]`, `equation`, `align`).

### M6 Introduce notation on demand
- **Situation**: a new symbol is needed.
- **Action**: introduce it at its **first genuine use**, saying what it denotes and why it earns a symbol.
- **Counter-example**: fifteen symbols listed at the head of a chapter, eight of them first used thirty pages later.
- **Signal**: distance between a symbol's definition and its first use is short.

### M7 Special case first
- **Situation**: about to state or prove something general.
- **Action**: do n = 2, two dimensions, a concrete function, a concrete matrix first, so the mechanism is visible; then generalize.
- **Counter-example**: stating it for an arbitrary index set or arbitrary category, leaving the reader nothing to stand on.
- **Signal**: a general statement is preceded by a special case, explicitly flagged as generalizing.

### M8 Counterexamples sit next to the claim
- **Situation**: an assertion whose limits you know.
- **Action**: put the counterexample or boundary case immediately after it, not in a later chapter.
- **Signal**: short textual distance between claim and counterexample.

### M9 Transition sentences do work
- **Situation**: between paragraphs and sections.
- **Action**: a transition must carry out *continuation*, *contrast*, or *preview* — and carry information.
- **Counter-example**: "Next we continue our discussion." / "Now we move to the next part."
- **Signal**: if the sentence survives being replaced by "Furthermore / However / To see this we need" with no loss, it was empty.

### M10 Close
- **Situation**: a proof or section ends.
- **Action**: say "this completes the proof", "so we have shown …", and point to what comes next or what it means. Do not just stop.
- **Counter-example**: the last line is a formula, then a new section begins.
- **Signal**: closing wording at the end of a `proof` environment.

### M11 Flag the key idea
- **Situation**: a non-mechanical trick appears in a proof.
- **Action**: say so — "the key observation is …", "the idea here is …". Separate the trick from the verification.
- **Counter-example**: the trick is buried in the second line of an `align`.
- **Signal**: non-trivial proofs contain explicit idea-flagging.

### M12 Genre decides restate vs cite
- **Situation**: you need a result from earlier or elsewhere.
- **Action**: **textbook / lecture note** — restate it in place; do not send the reader back thirty pages. **Paper** — cite it; do not restate.
- **Signal**: in textbook prose, cross-section citations are restated in place.

### M13 Construct first, then state properties
- **Situation**: introducing an object and asserting things about it.
- **Action**: **build the object, then say what it is.** Do not write "Theorem 1. There exists f. Theorem 2. f is continuous."
- **Why** (Serre): the two-part form slides the reader from the indefinite to the definite article, and "because you have switched from the indefinite article to the definite one, you are able to say things that you have really not proven at all."
- **Signal**: existence claims and their properties are merged into construct-then-assert.

### M14 Never leave the last step to the reader
- **Situation**: the end of a proof.
- **Action**: write the final step out. Do not close with "and the theorem follows" while skipping the actual last link.
- **Why** (Serre): "people want to prove Theorem 1… Then they give an argument, then they stop… And that's where the mistake was… very often, mistakes in proofs are in the non-written part, the implicit part."
- **Signal**: no unexplained inferential leap at the end of a proof.

### M15 Say where each hypothesis is used
- **Situation**: a theorem with several hypotheses.
- **Action**: use each one visibly. If a hypothesis is never used, say so.
- **Why** (Lombardo): a hypothesis absent from the proof usually means one of three things — (a) it is unnecessary; (b) the proof is wrong; (c) it is being used surreptitiously.
- **Signal**: each hypothesis has an identifiable point of use, or an explicit note.

### M16 Prove it checkably, not just convincingly
- **Situation**: writing a proof.
- **Action**: prefer more detail over less.
- **Why** (Serre): "I prefer a more detailed proof on paper. Because on paper, if you find it too long you just go to the next page. But if it is too short and if something is missing you may spend a lot of time trying to reconstruct it."
- **Note**: this does **not** conflict with "do not reprove standard lemmas" — that rule is about textbook-standard results, this one about the paper's own new steps. Judge them separately.

---

## 2. Word choice

### W1 Use the field's standard vocabulary
- **Situation**: naming a concept, or describing a step.
- **Action**: use the name the field already uses. If the field has a word for it, use that word.
- **Counter-example**: inventing "the two-layer localization framework" for what is called a compactness argument; calling a standard object "tame"; dressing a routine estimate as "a controlled approximation scheme".
- **Signal**: every named concept either (a) has a standard name in the field and uses it, or (b) is genuinely new and needed more than once.
- **Full treatment**: `slop-blacklist.md` S16 — this is the failure mode LLMs fall into most.

### W2 Do not invent named abstractions to hold one fact
- **Situation**: tempted to define "Property (P)", "Condition (C)", "an admissible pair".
- **Action**: do not name a one-use observation. State it where it is used.
- **Test**: delete the definition. Does any proof break? If not, it was bookkeeping.
- **Signal**: every named entity is referenced more than once, or carries real mathematical content.

### W3 Plain verbs beat nominalizations
- **Situation**: reaching for "perform a discussion of", "carry out a proof of", "achieve a factorization of".
- **Action**: use the verb — discuss, prove, factor.
- **Signal**: no `-tion of` / `-ance of` chains where a verb would do.

### W4 Precise verbs, graded by strength
Do not use one verb for every claim:

| Strength | Verbs | Use for |
|---|---|---|
| weakest | observe, note | directly visible |
| weak | verify, check | mechanical verification |
| medium | show, establish | substantive step |
| strong | prove | complete argument |
| derived | deduce, derive, conclude | follows from what is proved |

- **Counter-example**: "prove" for something that is substitution; "observe" hiding a three-step argument.

### W5 "Clearly" has a legal use
- **Legal**: the omitted step is **genuinely mechanical** (substitution, expansion, swapping summation order) and the intended reader would agree.
- **Illegal**: hiding a skipped step, hiding a needed lemma, hiding the fact that you have not thought it through.
- **Test**: if the reader is stuck for more than ten seconds, it is not obvious.
- **Words in scope**: clearly, obviously, trivially, it is easy to see, it is clear that, certainly, surely; 显然, 显而易见, 不难看出, 易知.
- **Audit** (Merry): before writing one, ask — *If the statement is obvious, do I need to state it at all? If I do, is it actually obvious? Should I be giving a proof after all?*

### W6 State uncertainty explicitly
- Unproved, assumption-dependent, or genuinely uncertain steps must be labelled: "this step requires an additional hypothesis", "we conjecture", "this remains open".
- The converse matters too: **do not hedge what you have proved.**

### W7 Conditions early
- Put hypotheses near the front of the sentence. Avoid long-distance dependencies.

### W8 One idea per sentence
- Sentence complexity should come from the mathematics, not from nested subordinate clauses.
- No long chains of noun modifiers: "the packet switched data communication network protocol problem."

---

## 3. Syntax — hard rules

These are mechanically checkable. Violating one is a defect, not a preference. All verified verbatim against the sources (see `sources.md`).

### H1 Do not start a sentence with a symbol
Knuth rule 2: "Don't start a sentence with a symbol."
- ✗ `f'' − a has n distinct zeroes.`
- ✓ `The polynomial f'' − a has n distinct zeroes.`

### H2 Do not use a symbol as a verb
Serre: "please don't use, if possible, symbols for verbs." His example was a paper whose main theorem was a string of formulas in which **the only verb was `∈`**.
- ✗ `The number x ∈ Q.`
- ✓ `The number x is rational.`

### H3 No logical symbols in running prose
Knuth rule 3: "Don't use the symbols ∴, ∋, ∀, ∃, ⇒; replace them by the corresponding words. (Except in works on logic, of course.)"
- Quantifiers in a **displayed** formula are fine; as connectives inside a sentence they are not.
- ✗ `Then ∀ε>0, ∃δ>0 such that …` → ✓ `Then for every ε > 0 there exists δ > 0 such that …`

### H4 No colon before a displayed formula
Knuth rule 23 — "those colons are wrong." Introduce a display with a complete sentence or a full stop.

### H5 Separate adjacent formulas with words
Knuth rule 1: "Symbols in different formulas must be separated by words."
- ✗ `Consider S_n, q < p.` → ✓ `Consider S_n, where q < p.`

### H6 The "blah" test
Knuth rule 13: replace every non-trivial formula with "blah" — the sentence should still read smoothly. Fastest check for whether formulas sit inside grammatical sentences.
Related: **every formula is part of a sentence**, punctuated normally (Friesecke; UC Davis).

### H7 Do not use `=` for "the next step is" or "implies"
UC Davis. Arrows are a slight improvement, still not good.

### H8 The sentence before a theorem is a complete sentence
Knuth rule 4: `We now have the following` is bad; `We can now prove the following result.` is good.
**Better still: make it a motivation sentence** tying the theorem to the preceding discussion.

### H9 The opening paragraph is the best paragraph
Knuth rule 24: "The opening paragraph should be your best paragraph, and its first sentence should be your best sentence."
**Worst possible opening: "An X is a Y."**
- ✗ `An important method for internal sorting is quicksort.`
- ✓ `Quicksort is an important method for internal sorting, because…`

### H10 Proofs are prose, not symbol chains
Knuth rule 10: "Don't use the style of homework papers, in which a sequence of formulas is merely listed. Tie the concepts together with a running commentary."

---

## 4. Person, tense, mood

### Person
**Choose one of three, by which reads most naturally:**

1. **we** — meaning *author and reader together*, **not** a formal stand-in for "I". Knuth rule 6: "this use of 'we' should be used in contexts where it means 'you and me together', not a formal equivalent of 'I'." ✅ verified
2. **Imperative / indicative** — Halmos argues this is **better**: "even better is to avoid both passive voice and the use of 'we' through judicial use of imperative and indicative moods." ✅ verified. Example: `We can now prove the following result:` → `Replace z by 7 throughout.`
3. ~~Passive throughout~~ — the thing to avoid.

- Avoid **"I"** in formal technical writing (Knuth, Halmos, Merry agree). Avoid **"one"** — it reads as stilted; "we" is better.
- Halmos adds a texture note: "we" carries a lighter tone, and "he isn't sure he wants that tone in his writing." **Tone is a legitimate part of the choice.**

### Tense
- Definitions and theorem statements: **present**. Merry: "Mathematical statements should be universal truths, and are traditionally stated in the present tense." ✅ verified
- Reasoning inside proofs: **present** ("Suppose x ∈ A. Then …").
- Historical commentary and prior work: **past** ("Hilbert proved …").
- **Pick one tense for citing others and keep it throughout**: `Gabai proves …` and `Lebesgue proved …` are both fine, **not in the same text**.
- Counter-example: `We will have shown that the theorem held.`

### Mood as a diagnostic
Merry: formal mathematics uses almost only the **indicative and imperative**.
**If you find yourself writing conditionals or subjunctives, go back and check the mathematics** — it usually means your grip on the theory is shaky. Grammar as a diagnostic instrument.

### Numbers
Spell out numbers used for counting; use numerals for numbers used as names. Do not begin a sentence with a numeral.

---

## 5. Notation

- **Design the notation before writing.** Halmos: "ad hoc decisions about notation, made mid-sentence in the heat of the composition, are almost certain to result in bad notation."
- **One symbol, one thing; one thing, one symbol.** Knuth rule 14. These are the two commonest errors on any notation checklist.
- **Introduce notation by reuse.** An expression used once does not need a name; one used repeatedly probably does. (The specific "three or more times" threshold attributed to Tao's blog **could not be verified** — see `sources.md` §2 — so only the weaker principle is kept here.)
- **`The` or `A`?** Match the article to uniqueness. A wrong `the` **presupposes a construction you have not proved** — the root of Serre's "the map of Theorem 1" error.
- **No clever notation.** It must not be cleverer than the mathematics.
- **Compatibility with the literature.** If you must diverge, **restate the cited results in your own notation** rather than making the reader translate.
- **Symbol budget.** Define before use; do not introduce unnecessary symbols; use conventional notation; watch for accidental clashes; be consistent.

---

## 6. Readability levers, ranked by return

1. Correct skeleton (the right sections, in dependency order)
2. Motivation before definition
3. A strategy paragraph for every proof
4. Every formula explained
5. Clean, consistent notation
6. Precise wording, no filler

If time is short, work down from 1. Polishing wording on top of a scattered skeleton returns approximately nothing.

---

## 7. Do not

- **Do not mechanically add motivation to every definition.** That produces a template. Add it **only where the reader would actually ask "why this?"** M1 is a judgement, not a form to fill in.
- **Do not break a continuous argument into bullet points.** Lists suit parallel items, not proof chains — a chain loses its direction when chopped up.
- **Do not add a summary paragraph that repeats what you said.** The end of a mathematics text should advance, not recap.
- **Do not attach emotional evaluations** ("deep", "beautiful") without an immediate, specific reason. See `slop-blacklist.md` S8.

---

## Appendix — writing in Chinese

Load this only when the output is to be in Chinese. The default is English.

**"我们" is contested; there is no universal norm.**
- Textbooks use 我们 to mean **author + reader**, not the author, and it can stand for mathematicians generally.
- **But forcing a subject where Chinese would omit it is Europeanised Chinese.** Chinese omits subjects far more readily than English — quantified: in one book, the Chinese translation has 62 instances of 我们有 against 369 instances of "we have" in the English translation.
- **Some journals and universities forbid subjective phrasing, including 我们.** Older formal register uses 笔者.
- **Check the target venue's style requirements first.** This skill defaults to 我们; that is a choice, not a standard.

**Chinese proof register — connectors in common use:** 设 / 定义 / 那么 / 注意到 / 任取 / 存在 / 于是 / 故 / 由于 / 由…可知 / 为方便 / 不难验证.

**Terms:** give the English original at first occurrence, then use one form consistently throughout. Terminology consistency outranks elegance: do not call the same object 紧集 in one place and 致密集 in another.

**Common Chinese-specific defects:** translationese, long modifier chains ("…的…的…的"), inconsistent terminology.

**Note on 不难验证:** it occupies the same structural slot as English "it is easy to see," and appears unflagged in observed Chinese proof writing. That is a **soft conflict** with W5, not an endorsement.
