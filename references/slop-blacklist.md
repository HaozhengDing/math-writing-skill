# Anti-slop blacklist

Failure modes of LLM mathematical writing. Each entry gives a **detection signal** and a **treatment**.

Run the greppable word lists (Part 4–5) mechanically. A hit is not automatically wrong, but **every hit must be consciously kept or fixed** — none may pass unnoticed.

---

# Part 1 — The LLM signature failure

> **There are three, not one.** S16 below is the first and largest. Its two siblings — **S17 process narration** and **S18 disciplinary register leakage** — sit in Part 3 with the other register material. Read all three together; they are surface symptoms of a single habit: **describing a process where a relation should be stated.**
>
> | | Wrong | Example |
> |---|---|---|
> | **S16** | the **vocabulary** | an invented name for a standard condition |
> | **S17** | the **subject** | "the early experiments were not in vain" |
> | **S18** | the **register** | "the **input** weights … the **output** weights" |

## S16 Over-encapsulation

**Inventing abstractions the mathematics does not need, and failing to use the field's own language.**

This is the failure mode LLMs fall into most often, and it is the hardest to see, because the result *sounds* more sophisticated rather than less.

Sections 7–10 below come from a real corpus of technical research notes in which this pattern was pervasive — see `terminology-audit.md`.

### What it looks like

1. **Naming things that already have names.** Calling a compactness argument "the localization principle"; calling a locally finite family "tame"; renaming a standard object with your own term.
2. **Naming things that need no name.** "Property (P)", "Condition (C)", "an admissible pair (X, Y)" — introduced for a one-line observation, then referenced once.
3. **Framework register imported from ML/CS papers.** "We propose a framework", "our pipeline", "the approach consists of three modules", "we introduce a novel paradigm".
4. **Avoiding the field's verbs.** Not "by compactness", but "through a controlled finitization procedure". Not "this is finitely generated", but "this structure admits a finite spanning set".
5. **Abstraction as hedging.** Stating a result at a higher level of generality than needed, so the claim becomes vaguer and harder to falsify.
6. **Bookkeeping inflation.** A definition that exists only so it can be cited once, adding a tracking burden with no mathematical content.
7. **Naming a case instead of stating the condition.** Calling the range $n \ge N$ "the asymptotic regime" and $n < N$ "the finite regime" — defining the two by explicit inequalities, then using the names everywhere, so the reader must carry a lookup table to follow any argument. **The condition is the content; the name is a detour to it.**
8. **A mnemonic replacing a formula.** Writing `depth` for $\min\{m : T^m v = 0\}$ — smoother to write, and it loses exactly what needs checking. Note the tell: the document declares `\DeclareMathOperator{\depth}{depth}` — **committing the coinage at the tooling level**, which also makes it much harder to remove later.
9. **A standard word carrying a private meaning.** `regular` used throughout a project to mean "satisfying condition (H)", when the field already uses the word in three other senses. This is the most insidious form: the word **passes the standard-name test superficially**, so no reader flags it — while every reader silently imports their own, wrong, associations. The test must be applied to the **meaning**, not to the word.
10. **Rhetorical packaging of a summary.** When every content word in a summary is a coinage, the summary degenerates into pure syntax. A real example from the corpus:

> ✗ "The reduced theory exhibits a controlled obstruction in the asymptotic profile, and the framework measures that obstruction through the stratification and the residual pairing."

Every content word here is invented, so the sentence **contains no checkable content at all** — it cannot be right or wrong. The same corpus also contains boxed, arrow-linked "concept diagrams" built entirely from such terms. **A summary you cannot falsify is not a summary.**

### Why it happens

- Training pressure toward sounding sophisticated; the "we propose a novel framework" register is heavily represented in the data.
- **A vague wrapper is harder to falsify than a concrete claim.** This is the deep reason. Over-encapsulation is often not stylistic decoration but a way of not committing.
- Uncertainty about the field's specific terminology is resolved by inventing a generic one, which feels safer than using a term you might get wrong.
- A memorable name makes the *writing* easier — and it is easy to mistake that for making the *reader's* job easier. It does the opposite.

### Why it is harmful

- The reader cannot map your text onto what they already know. Reading becomes translation.
- It **hides whether you actually have a proof.** This is the serious harm.
- It makes the mathematics appear deeper than it is.
- **It is self-reinforcing.** Once the invented term is a section title, every later mention inherits its authority; the coinage acquires a life of its own and stops being examined.

### The four tests

| Test | Question | Fail means |
|---|---|---|
| **Standard-name** | Does the field already have a name for **this meaning**? | Use that name instead. |
| **Removal** | Delete the definition. Does any proof break? | It was packaging. |
| **Reuse** | Is it used more than once? | A one-use name is bookkeeping. |
| **Context** | Is this word standard *in this field, in this sense*? | A standard word with a private meaning is worse than a new word. |

A named concept should pass at least one. Preferably all three of the first three — and it must pass the context test outright.

### The metaphor rule

The corpus shows the decisive distinction:

- **A metaphor** ("the deep regime", "the outer layer") must be decoded. It requires a lookup, and it imports spatial intuition that may be *wrong* — "deep" versus "shallow" is just two ranges of one parameter; the metaphor does no mathematical work and quietly suggests a structure that is not there.
- **A transparent label** (`the range c ≤ −a−1`, `nilpotency order`, `the segment G^{≥ν}`) can be read without a lookup, because it says what it is.

**Prefer names that announce their content over names that evoke it.**

This is also the answer to the overcorrection worry: you do **not** have to write the inequality out forty times. You have to stop naming it with a metaphor. Either write the condition, or use a label that restates it.

### Detection: the macro signal

A declared macro for a **non-standard** operator is a strong, mechanically greppable sign that a coinage has taken root:

```latex
\DeclareMathOperator{\depth}{depth}   % ← non-standard: red flag
\DeclareMathOperator{\Hom}{Hom}       % ← standard: fine
\newcommand{\deepregion}{...}         % ← red flag
```

Grep `\DeclareMathOperator` and `\newcommand` for names that are not standard operators (`\Hom`, `\Ext`, `\Tor`, `\rank`, `\soc`, `\rad` …). Each hit is a coinage the author has committed to, and each one must pass the four tests.

### ✗ / ✓

> ✗ We introduce a two-layer localization framework. In the first layer we establish a local boundedness principle; the second layer globalizes it via a finite reduction argument.

> ✓ The function is locally bounded: each point has a neighbourhood on which it is bounded. Since the domain is compact, finitely many of these neighbourhoods cover it, so the bound is uniform.

The second is longer and considerably better. The first is three invented nouns wrapped around one compactness argument.

> ✗ We say that a pair (X, Y) is admissible if every point of X has a neighbourhood whose image lies in Y. Let (X, Y) be admissible. …

> ✓ (just say it) Each point of X has a neighbourhood mapped into Y.

> ✗ **Theorem** (simplicity in the deep regime). *(Reader must go back and find what "shallow" meant.)*

> ✓ **Theorem.** For $n \ge N$ and $\lambda 
e 0$, the module $Q$ is simple.

> ✗ Let $\depth_T(v)$ be the depth of $v$. *(A name standing where a computation should be.)*

> ✓ Let $n_T(v) = \min\{m : T^m v = 0\}$ be the nilpotency order of $v$ with respect to $T$.

### ⚠️ Do not overcorrect

**This is not "never abstract."** Abstraction *is* mathematics — group theory is abstraction, and a paper that refuses to name anything is unreadable for the opposite reason.

The rule is: **abstract when the mathematics demands it, not when the prose wants a noun.**

The test is whether the abstraction carries mathematical content and gets used. A framework that organizes three genuinely different arguments is doing work. A framework wrapped around one argument is decoration.

**And note which words in the corpus are *not* anti-patterns** — the distinction is per-occurrence, not per-word:
- `spectral sequence` — standard. Keep.
- `head`, `socle`, `radical` — standard module-theoretic vocabulary. Keep.
- `regular` — standard in at least four senses; a *fifth*, private sense is the anti-pattern. Judge each occurrence.
- `rank-one` — near-standard in differential-operator module theory (Bavula). Borderline.
- `研究缺口` / "research gap" — ordinary language. Not an anti-pattern.

**The lesson: this problem cannot be solved with a banned-word list.** The same word is correct in one sentence and a coinage in the next. That is why the tests exist and why they must be applied to meanings.

---

# Part 2 — Structural anti-patterns

### S1 Empty openings
- **Looks like**: grand context that never reaches the mathematics. `Throughout the rich history of analysis, continuity has occupied a central place. With the continued development of modern mathematics, …`
- **Treatment**: delete. Start from the specific problem. The first paragraph should already contain a mathematical object.

### S2 Invented motivation
- **Looks like**: fabricated applications or importance used to justify a concept. `The notion of compactness is of great practical importance in engineering.`
- **Treatment**: replace with the real mathematical motivation — which theorem it makes true, which counterexample it rules out. **If you cannot find a real motivation, you do not yet understand the concept. Go and find out. Do not invent one.**

### S3 Answer before question
- **Looks like**: conclusion or definition first, with motivation reduced to a single "this is important".
- **Treatment**: swap the order. See M1.

### S4 The proof that restates
- **Looks like**: the proof rephrases the theorem, or is just "by definition".
- **Treatment**: this is a **mathematical** defect, not a style problem. Supply the substance, or mark the proof as incomplete. Do not paper over it.

### S5 Skipped steps hidden by "clearly"
- **Looks like**: a decisive step carried by "clearly / obviously / it is easy to see".
- **Treatment**: expand it, or cite the specific lemma. This is one of the most damaging habits a model has — **it makes errors undetectable**.

### S6 Formula dumping
- **Looks like**: consecutive displays with no prose between them.
- **Treatment**: a sentence after each; or merge the routine computation, or move it out.

### S7 Proof chains turned into bullet lists
- **Looks like**: steps with real dependencies presented as bullets.
- **Treatment**: back into connected paragraphs. Lists are for **parallel** items ("three cases"), not **sequential** ones.

### S8 Notation explosion
- **Looks like**: many symbols introduced and never used; one object under two symbols; confused symbol levels (ε as both an error and an index).
- **Treatment**: delete unused symbols; unify collisions; check against a symbol table.

### S9 Metadiscourse
- **Looks like**: `We now turn to the three main aspects of this section.` / `In summary, we can see that` / `It is worth noting that`.
- **Treatment**: delete. The reader is reading a text, not attending a talk.

### S10 Endings that do not advance
- **Looks like**: the closing repeats what was already said.
- **Treatment**: point to what comes next, what the limits are, what is open.

### S11 Mechanically applied templates
- **Looks like**: every definition gets a forced motivation paragraph; the text becomes an assembly line.
- **Treatment**: add motivation only where the reader would genuinely ask why. **Rules are for judgement, not for filling in blanks.**

---

# Part 3 — Tone and register

### S12 Over-hedging
- `It might perhaps be possible, in some sense, to suggest that …`
- **Treatment**: say what is certain as certain, and say explicitly what is not.

### S13 Over-assertion
- Stating unproved things in a confident voice.
- **Treatment**: downgrade to "we conjecture / it appears". **This is more dangerous than over-hedging**, because it lets the reader treat an open problem as settled.

### S14 Emotional salesmanship
- `This beautiful result!` / `Remarkably, …` when it is not remarkable.
- **Treatment**: cut the emotion; say what is unexpected and why.

### S15 False empathy
- `The reader may find this confusing, which is normal …`
- **Treatment**: explain the hard part properly instead.

### S17 Process narration

**Writing about the research instead of the mathematics.**

Found in the same corpus as S16, concentrated in a note genre that interleaves statement, explanation, and proof. This is the second signature failure, and it is distinct from over-encapsulation: the vocabulary is fine, the *subject* is wrong. The text narrates how the work went — what was tried, what was surprising, what the author intends — rather than stating mathematics.

**Diagnosis**: ask of each paragraph, *does this state a mathematical fact, or does it narrate the process of finding one?* In a private notebook, process narration is appropriate. In a document meant to be read as mathematics, it is noise.

#### S17.1 Document meta-commentary
Reading guides, maintenance instructions, self-description.

> ✗ `\begin{remark}[living note 规则] 后续每次有新的证明进展、符号约定或合作者建议，本文件应更新`
> ✗ `\section*{阅读指南}`
> ✗ `这份 note 的主旨可以先用一句话概括`

**Treatment**: delete. Version-control metadata belongs in a commit message; a reading guide belongs in a file header, not in the mathematics.

#### S17.2 Self-justification
Arguing that the work was worthwhile, or defending a choice.

> ✗ `早期计算的启发是：继续无目标地增大 Γ 并不可靠。`
> ✗ `换句话说，早期实验不是白做的。`
> ✗ `我们不是为了局部化本身而局部化，而是希望把局部化 quotient 识别成另一类标准诱导模`

**Treatment**: delete. A reader judges the mathematics; they are not auditing your process. If a choice needs justification, justify it mathematically (what breaks otherwise), not biographically.

#### S17.3 Promotional register
Dramatic labels for ordinary results.

> ✗ `\section{The completion step (the harvest)}` / `\section{Where the method stops (the frontier)}`
> ✗ `The engine is one lemma`
> ✗ `第二步：$B_2$ 和 $G_2$ 暴露出真正的模式`

**Treatment**: name the section after its content. "The harvest" and "the frontier" are marketing; `Simplicity for $c<b$` and `Where the method fails` are not.

#### S17.4 Numbered revelation framing
Presenting findings as a sequence of insights or steps.

> ✗ `这一步给出的第一个启示是：…` / `这一步给出的第二个启示是：…`
> ✗ `\section{目前的整体逻辑链}` + a boxed arrow diagram

**Treatment**: state the results. If there really are three cases, number the *cases*, not the *revelations*.

#### S17.5 Confessional scope packaging
⚠️ **The most delicate entry — read the whole thing.**

Repeated disclaimers about what the document does not claim:

> ✗ `this note is not a claim of independent peer review or formal verification` (near-identical text closing the abstract in four separate files)
> ✗ `\begin{remark}[What is not asserted]` (a six-line non-assertion block)

**The content of these caveats is often necessary** — they mark real gaps, and removing them would be dishonest. **The problem is register, not content.**

- **Keep**: "Theorem 4.2 is proved only for $\mu \notin \mathbb{Z}$."
- **Cut**: "This note is not a claim of independent peer review or formal verification."

State the mathematical boundary of what is proved as a mathematical fact about the theorem. Do not add a legal disclaimer about your own document. A repeated, boilerplate disclaimer trains the reader to skip it — including the one time it matters.

**The model answer exists, in the exemplars.** One audited report has the same problem to solve — it is not peer-reviewed — and solves it two ways, neither of which is a disclaimer:

1. **A titled remark listing the limitations as precise facts** (`exemplar.md` P14): each obstruction gets an explicit witness, then *"Only under (3.2) is \(G_c\) known here to contain every proper submodule. In particular, at the critical level \(G_c\) may vanish when \(\mu\notin\Z\) although \(Q_c\) is still reducible. The criterion concerns unreduced modules; simplicity after a central reduction is a separate question."* Three sentences, each stating exactly which statement is limited and how — all usable by the reader.
2. **A dedicated open-problems section** (P9), and **verification cited as evidence with counts** (P10): *"Independent audit of 2026-09-22, … (154 exact checks); counterexamples reproduced in … (24 checks)."*

**Rule: when tempted to disclaim, cite instead.** If verification exists, point at it with numbers and a path. If it does not, say precisely which results are unverified — as facts about those results.

#### S17.6 Unfalsifiable slogans
A sentence that sounds like a conclusion but cannot be false.

> ✗ `The applicability boundary of the present method coincides with the onset of that no-go.`
> ✗ `The reduced theory exhibits a controlled obstruction in the asymptotic profile.` (see S16.10)

**Treatment**: apply the falsifiability test — *can this sentence be false?* If not, replace it with the theorem or the counterexample it is gesturing at. See rubric G4 Step 3.

#### S17.7 The "understanding layer" template

A recurring structural pattern: a paragraph named 理解 / 定位 / 启示 / 直观上 (or "Understanding", "Where this sits") inserted between the statement and the proof. It appears in several files as a reusable template.

This is a **good instinct executed in the wrong register.** The instinct is right — M1 says motivate before formalising. The failure is that these paragraphs usually contain a *restatement* of the statement plus homiletic framing, rather than the actual reason the definition is shaped that way.

**Test**: does the paragraph tell the reader something they could not have got from the statement itself? If it only reframes the statement in plainer words, either cut it or replace it with the real motivation — which usually means: what goes wrong without this hypothesis, or which earlier attempt this repairs.

**Treatment**: keep the slot, change the content. A genuine "why this definition" paragraph is one of the highest-value things in mathematical writing. A homiletic restatement is not.

#### Counter-note: these markers are genre-dependent

This register is **normal and useful in a working notebook** — "early experiments were not in vain" is a reasonable thing to write to yourself on a Tuesday. It becomes a defect when the note is promoted to something a reader will read as mathematics.

**So the first question is not "how do I fix this sentence" but "what is this document for?"** If it is a private notebook, leave it alone. If it is being read by anyone else — an advisor, a collaborator, a referee — the process narration goes.

### S18 Disciplinary register leakage

**Ordinary English words borrowed from computer science and engineering — correct in that discipline, and simply not what a mathematician writes.**

This is the third signature failure, and distinct from the other two:

| | What is wrong | Example |
|---|---|---|
| **S16** | The **vocabulary** — invented abstractions | an invented name for a standard condition |
| **S17** | The **subject** — narrating the research | "the early experiments were not in vain" |
| **S18** | The **register** — describing a computation instead of mathematics | "the **input** weights … the **output** weights" |

#### Root cause: describing data flow instead of mathematical relations

This is what makes S18 diagnosable rather than a word list. The borrowed vocabulary nearly always appears where the text is describing **what goes into a process and what comes out**, rather than **what the objects are and how they relate**.

> ✗ (real instance) "…at most the sum of the **input weights**: for \([h,e]\), \([e,f]\), \([h,f]\), \([h,h]\) the **output weights** are at most \(2,1,0,0\) against **input sums** \(3,2,1,2\)."

The mathematics being stated is: *the weight of a bracket is at most the sum of the weights of its factors.* The sentence instead describes a pipe with an inlet and an outlet.

> ✓ "For each of \([h,e]\), \([e,f]\), \([h,f]\), \([h,h]\), the weight of the bracket is at most the sum of the weights of its factors: \(2\le3\), \(1\le2\), \(0\le1\), \(0\le2\)."

**The fix is a restructure, not a synonym.** "input weight" has no one-word mathematical replacement — the repair is to **name the mathematical objects** (the bracket, its factors, their weights) and state the relation between them.

#### Why it is invisible

These words pass the **standard-name test** (S16) trivially: `input`, `output`, `data`, `setup` are all standard English. They are not jargon a mathematician would call *wrong*. They are just **not what we say** — which is exactly why they survive review and why they need their own rule.

#### Evidence — measured, not guessed

Searched across the 1776-line body of a technical paper:

| Term | Real hits | Verdict |
|---|---:|---|
| `input` / `output` | 2 | ❌ L222–223 — the clearest instance |
| `data` | 2 | ❌ L875, L893 — "the polynomial **data** \(\eta=2\)" → **the parameters** |
| `channel` | 2 | ❌ L1681, L1747 — "the lowering **channel**", "the three **channels**" → **maps**, **transitions** |
| `setup` | 2 (body) | ❌ `\section{Setup and notation}` (L67), "assume only the **setup**" (L1225) → **Notation and conventions** |
| `mechanism` | 2 | ⚠️ borderline — L680, L1211; "argument" or "phenomenon" reads more mathematical |

**False positives found in the same sweep — do not flag these:**

| Match | Reality |
|---|---|
| `efficien` ×26 | all **co**efficient |
| `string` ×7 | all `\texorpdfstring` (a LaTeX macro) |
| `script` ×2 | all de**script**ion |
| `array` ×2 | `\begin{array}` |
| `tool` ×1 | the `mathtools` package |
| `report` ×2 | "We report recent progress" — normal mathematical English |

**Note the scale**: five genuine instances in 1776 lines. S18 is a **polish-level** defect, not a structural one — unlike S16, which ran to ~50 occurrences per document. Do not let an S18 hunt turn into a rewrite.

#### Word table — with mathematical alternatives

| CS / engineering | Mathematicians write |
|---|---|
| input, output | *(restructure — name the objects and the relation)* |
| data | parameters, hypotheses, the given values |
| setup | notation and conventions, preliminaries |
| channel | map, transition, arrow |
| mechanism | argument, phenomenon *(borderline)* |
| implement | construct, realise |
| handle (a case) | treat, dispose of |
| feature | property |
| tool, toolkit | method, technique |
| store, record into | *(state the relation instead)* |
| default | unless stated otherwise |
| robust | stable under perturbation |
| test | check, verify |
| valid | well-defined, legitimate |
| process (as a noun) | construction, procedure, argument |
| performance | *(usually nothing — cut it)* |

**Judgement rules**
- **`process` as a verb is usually fine** ("we process the relation") — as a noun it is CS ("the processing pipeline").
- **`valid` / `test` / `check`** have legitimate mathematical uses; flag only when they describe software behaviour rather than mathematical correctness.
- **`robust`** is a real red flag: mathematics says *stable*, *independent of*, or names the perturbation.
- **`default`** is acceptable in the fixed phrase "by default" if rare; as a noun ("the default value") it is CS.

#### Relationship to the other failures

S18 often appears **alongside** S16 in the same document, and the two interact badly: a coined term plus CS register makes the text read as neither mathematics nor computer science. When cleaning, handle S16 first (structural), then S18 (polish) — and do not mix the passes, or a terminology fix will damage good prose (see `exemplar.md`).

---

# Part 4 — Greppable word lists

Not banned words — **words that require a reason**. Judge each hit.

```
it is well known that        obviously              clearly
it is easy to see            trivially              of course
it is worth noting that      it should be noted     note that
profound                     elegant                beautiful
powerful                     remarkable             fascinating
in this paper we will        let us now turn to     in conclusion
plays a crucial role         of great importance
framework                    paradigm               pipeline
we propose                   we introduce a novel
```

### ⚠️ `trivial` is overloaded — the commonest false positive

`trivial` has a **legitimate technical meaning** and must not be flagged in that sense:

- **trivial module** (the zero module), **trivial representation**, **trivial character**
- **meets trivially** = the intersection is zero
- **nontrivial submodule** = a nonzero proper submodule

Only the **epistemic** sense is the anti-pattern — "trivially, this follows", "it is trivial that".

**Evidence**: in the 1777-line exemplar (`exemplar.md`), `trivial` occurs 5 times and **every one is the technical sense** — *"the module is trivial"* (L438), *"the span meets \(F^{m+t}M\) trivially"* (L571), *"a nontrivial…"* (L869), *"act nontrivially"* (L1078), *"meets \(V\) nontrivially"* (L1109). A blanket ban on the word would produce five false positives in a document with no real problem.

**Same caution applies to**: `immediate` (a *degenerate case* may genuinely be immediate), `similarly` (acceptable when listing an analogous one-line computation), `normal`/`regular`/`simple`/`free` (all overloaded with technical meanings).

**Rule**: grep the word, then judge the **sense**. Never ban a word that has a technical use without stating which sense is meant.

**Judgement rules**
- **Evaluations** (profound / elegant / powerful): allowed, **but must be followed immediately by the specific reason.** `This is a profound theorem` ✗ → `What is profound here is that it links a local property of X to a global property of Y` ✓
- **"Clearly / obviously"**: allowed, but the omitted step must be genuinely mechanical. Spot-check three; if you hesitate, rewrite.
- **Metadiscourse** (`in conclusion`, `let us now turn to`): delete by default.
- **"It is worth noting that"**: allowed only if what follows is genuinely counterintuitive or easy to miss.
- **Framework vocabulary** (`framework`, `paradigm`, `pipeline`, `we propose`): see S16. Usually a sign of imported register, not mathematics.

**Chinese equivalents** — load only when writing in Chinese:
```
众所周知  在数学的广阔天地  随着…的不断发展  具有重要意义
极其重要  至关重要  不可或缺  扮演着重要角色
值得注意的是  需要指出的是  不难发现  显而易见  易知  显然
深刻  优美  优雅  美妙  令人惊叹  精妙  巧妙  强大
综上所述  总而言之  我们可以看到  本文将…展开论述
接下来我们将  下面进入  进行…的讨论  作出证明
```

### Register markers (S17) — greppable phrases

These are the surface forms of process narration. **Chinese and English notes use two distinct dialects of the same register** — worth grepping separately.

**Chinese notes lean on:**

```
这不是…而是…        这正是…的来源        换句话说
一句话概括          本文的定位           阅读指南
第一个启示          第二个启示           早期实验不是白做的
值得注意            启发是               未独立审稿或形式化验证
```

**English notes lean on:**

```
the crucial point is        it is worth noting        first and foremost
the engine is               state honestly            the harvest / the frontier
not a claim of              what is not asserted      this note does not claim
```

**Judgement rules**
- `这不是…而是…` / "not X but Y": allowed only when there is a **real** alternative being excluded that the text considers. Otherwise it flattens a derivation into rhetorical balance — a very common tic.
- `第一个启示 / 第二个启示`: **default delete.** If there are three cases, number the cases, not the revelations.
- `一句话概括` / "in one sentence this note says": allowed only if the sentence is checkable. Otherwise see S16.10.
- Scope disclaimers (`未独立审稿或形式化验证`, "not a claim of independent peer review"): **keep the mathematical caveat, cut the legal-register disclaimer.** See S17.5.

### Disciplinary leakage markers (S18) — greppable

```
input        output       data         setup        channel
mechanism    implement    handle       feature      tool / toolkit
store        default      robust       process (noun)
performance  valid        test
```

**Judge the word, not the substring.** Known false positives in a LaTeX mathematics corpus: `efficient` (contains `efficien`), `description` (contains `script`), `\texorpdfstring` (contains `string`), `mathtools` (contains `tool`), `\begin{array}` (contains `array`).

**Expected yield is low** — five genuine instances in 1776 lines. If a sweep is returning dozens of hits, the pattern is matching substrings, not words. Full treatment and rewrite table: S18.

---

# Part 5 — Verbosity substitutions

From Merry, *Communication in Mathematics* §4.1.1–4.1.2. **The most directly machine-checkable material in this skill** — deterministic mappings, no judgement required.

### 5A — Verbose substitutes for "because" (all → `because`)

```
due to the fact that            → because
in view of the fact that        → because
owing to the fact that          → because
for the reason that             → because
on account of                   → because
on the grounds that             → because
the reason is because           → because
accounted for by the fact that  → because
based on the fact that          → because
because of the fact that        → because
```

### 5B — Phrases reducible to one word

```
in order to            → to
by means of            → by
for the purpose of     → for
during the course of   → during / while
as to whether          → whether
the question as to whether → whether
connected together     → connected
alternative choice     → choice
equal to one another   → equal
fewer in number        → fewer
assemble together      → assemble
collaborate together   → collaborate
eliminate altogether   → eliminate
```

### 5C — More verbose phrases

```
a number of                    → some
a small number of              → a few
despite the fact that          → although
in connection with             → about / concerning
in the event that              → if
take into consideration        → consider
in the vast majority of cases  → usually
make an assumption that        → assume
an example of this is the fact that → for example
```

### 5D — Emphatic words to delete mechanically

`very` / `most` / `least` / `actually` / `really` — Merry: "they can almost always be deleted… the words we have removed usually indicate the adjectives that are themselves questionable."

**That is: after deleting the emphasis, if the remaining adjective looks doubtful, that is exactly what needs attention.**

### 5E — Two mechanical searches

1. **Search `-ly`** — catches stray adverbs. (Misses very/most/least/never/often; over-matches imply/rely/reply. Review by hand.)
2. **Search `there is` / `there are` / `this is` / `it is`** — catches redundancy and unclear reference.

Both are cheap and belong in the pre-delivery self-check.

### 5F — Mathematical redundancy

Merry's example: `The smallest odd prime is a well-defined, unique number.` — **`unique` is redundant**; the definition already implies it.

**Consequence**: after writing a mathematical sentence, ask "if I delete this word, is the statement still true?" If yes, the word was filler.

### 5G — Misused symbols

- ✗ `=` for "the next step is" or "implies" (UC Davis). Arrows are slightly better, still not good.
- ✗ `∴ ∵ ∀ ∃ ⇒` in running prose (Knuth rule 3; works on logic excepted).
- ✗ Sentences starting with a symbol; symbols used as verbs (H1/H2 in `style-rules.md`).
