# Positive checklist — what good looks like

Everything else in this skill describes **what to avoid**. This file is the other direction: twenty-three named techniques that make mathematical prose readable, with the anti-pattern each one answers.

The patterns were extracted by line-anchored analysis of well-written research notes in a technical genre (progress reports written for specialist readers), then detached from their source material. They are **a** good style for **that** genre, not a universal one.

---

## The clarity-adverb audit — why the rest of this file is believable

Before the patterns, the single most useful data point.

A 1777-line research paper was audited for hedging adverbs. Body text only:

| phrase | hits |
|---|---:|
| `clearly` | **0** |
| `obviously` | **0** |
| `it is easy` / `easy to see` | **0** |
| `well known` | **0** |
| `straightforward` | **0** |
| `routine` | **0** |
| `of course` | **0** |
| `note that` | **0** |
| `it follows` | **0** |
| `immediate` | 1 |
| `similarly` | 1 |

**Four hits in total, and every one defensible.** The single `immediate` sits on a genuinely degenerate case and is followed at once by the general argument. The single `similarly` skips a one-line bracket computation.

**Why this matters more than any rule here**: it is direct evidence that the guidance in `slop-blacklist.md` (S5) is **achievable at scale**. This was a paper with cross-references, inductions, and case analyses — exactly the conditions under which "clearly" is most tempting — and it contains none. The discipline is not an aspiration; it is what a careful author writes.

**And it exposes a false positive.** The same sweep found several occurrences of `trivial` — *all* of them the mathematical term (*trivial module*, *meets trivially*, *nontrivial*), none the epistemic "trivially, this follows". See `slop-blacklist.md` Part 4: never blanket-ban a word that has a technical use.

---

## P1. Caveats state what the mathematics does **not** assert

Where a notation could be misread, say so immediately — and make the caveat a fact about the mathematics, not a disclaimer about the document.

> ✓ "The expression $F^{-m}u + M$ denotes a coset of a vector in the localization; **it does not assert that $F^{-1}$ acts on the quotient**."
> ✓ "This is a vector-space filtration; **its terms need not be $U$-submodules**."
> ✓ "**No inequality $j + r > b$ is needed.**"

**Contrast with S17.5** — the confessional register ("this note is not a claim of independent peer review"). Both are negative statements, but:

- P1 tells the reader something **about the mathematics** that they would otherwise get wrong.
- S17.5 tells the reader something **about the document's status** that they never assumed.

**Rule**: before stating a caveat, ask *does this prevent a mathematical misreading, or am I managing my own liability?* Keep the first, cut the second.

**This is a technique, not a reflex.** In the audited document it appears nine times.

---

## P2. Account for the hypotheses before the theorem

> ✓ "**The isomorphism requires $\lambda_1 \ne 0$; the level $c$ is arbitrary. The additional condition $c \ne -2$ is used only for simplicity.**"

Three sentences that tell the reader what to watch for — which hypothesis is essential, which is free, which is a convenience. A reader meeting $\lambda_1 \ne 0$ in the theorem already knows why it is there.

This is M15 ("say where each hypothesis is used") executed **in advance** rather than during the proof. Two sentences; removes the commonest source of confusion in hypothesis-heavy mathematics.

---

## P3. Name the method, not the step

The right answer to "how much detail". Dense but never hand-waving: **state the operation and the identity, then the conclusion**, without expanding the algebra.

> ✓ "The localization has basis $\{F^rXu\}$: **common denominators give spanning**, and **multiplying a finite relation on the left by a sufficiently large power of $F$ reduces independence to PBW in $M$**."
> ✓ "For $m = 1$, **multiply the right-hand side on the right by $F$ and use $D^j(x)F = FD^j(x) - D^{j+1}(x)$; the sum telescopes to $x$**."
> ✓ "**Indeed, move sufficiently high modes past a fixed finite PBW word; all resulting noncentral modes still have sufficiently high indices and annihilate the inducing vector.**"

Note what these are **not**:
- Not "it is easy to see" (S5) — the reader is told **what to do**.
- Not a full expansion — the routine algebra is left to the reader.
- Not "clearly".

**This resolves the tension between W5 and M16.** The choice is not "expand everything" vs. "hand-wave". There is a third option: **name the method and the identity, and let the reader execute it.** A reader who can run the step will; one who cannot now knows exactly what is missing.

---

## P4. Descriptive titles, zero metaphor

Titles say what is in the section: "Definitions, notation, and assumptions"; "The basic isomorphism"; "Bases and commutation with negative powers"; "Smoothness, simplicity, and the assumptions".

**Contrast with S17.3** ("the harvest", "the frontier") and **S16.7** (naming a case instead of stating it). No title requires decoding; none narrates a discovery.

---

## P5. Sharpness — show each hypothesis is necessary

> ✓ "If $\lambda_1 = 0$, the homomorphism still exists, but $\Phi(e_0v) = e_0w_1 = 0$, whereas $e_0v \ne 0$ by the source PBW basis. **Thus the specified map is not an isomorphism.**"

The hypothesis is not merely assumed — its failure is exhibited with an explicit witness. This is the difference between a theorem and an understanding of a theorem.

**Contrast with S16**: no invented object is needed. The witness is in the existing notation.

---

## P6. Bind a private label to an explicit symbol at first use

> ✓ "For **the local case $|x| < 1$**, let $D$ be the open unit disc; equivalently, throughout we work on the open unit disc."

The single most useful finding, because it resolves the largest terminology problem. A private label is tolerable **if its first use is bound to an explicit object**.

After the binding, every later "the boundary case" resolves to something the reader can see. The word has become an **abbreviation for something stated**, not a **label for something implied**.

**Rule**: a private label is acceptable when bound at first use; not acceptable when the reader must infer the referent from context. Full treatment in `terminology-audit.md` §3.

---

## P7. Anchor to the literature precisely

> ✓ "These conventions agree with [FGXZ, §2.3]."
> ✓ "By [FGXZ, Theorem 1.1], for $a + b \ge 0$, …"
> ✓ the bibliography gives arXiv ID **with version** (`arXiv:2404.03855v2`) and the sections relied on.

Conventions are declared compatible with a cited source rather than left for the reader to reconcile — the notation-compatibility rule in `style-rules.md` §Notation, done well. The version number matters: a citation that still resolves to the same theorem in five years.

---

## P8. Say which part of a proof needed which hypothesis

> ✓ "The isomorphism remains valid at the critical level $c = -2$; **its injectivity was proved without using simplicity**."

A precise statement about the *structure of the argument*, letting the reader see which conclusions survive when a hypothesis is dropped. This is the constructive form of the scope remark — the kind that should survive any cleanup, as opposed to what S17.5 targets.

---

## P9. Open problems get their own section, precisely stated

Not a disclaimer scattered through the text — a dedicated section at the end, which **states what is settled first**:

> ✓ "**Theorem 4.8 settles simplicity … for all parameters, in both regions. The following questions remain.**"

Each item is a well-posed question, and the **difficulty itself is made mathematical**:

> ✓ "determine whether $G_c$ is simple, compute $\operatorname{soc}(G_c)$, and decide whether $Q_c$ has finite composition length; **a correct analysis must track the three maps $P_\nu \to P_{\nu+2}, P_\nu, P_{\nu-2}$ simultaneously** (Propositions 3.4 and 3.5)."

A reader learns what is open, why it is hard, and where the machinery is. Nothing is apologised for.

---

## P10. Evidence, not disclaimer

Verification status belongs in the bibliography as a citable artifact with counts — not in the abstract as an apology:

> ✓ "Independent audit of 2026-09-22 — report and `tools/verify_claims.py` (**154 exact checks**); counterexamples reproduced in `tools/check_regressions.py` (**24 checks**)."

**This is the direct inversion of S17.5.** That anti-pattern writes *"this note is not a claim of independent peer review or formal verification"* into the abstract. This says *here is the audit, with 154 checks, and here is its path*. Same underlying fact; one of them is useful.

**Rule: when tempted to disclaim, cite instead.** If verification exists, point at it with numbers. If it does not, say precisely which results are unverified — as facts about those results.

---

## P11. A section title may be the statement itself

> ✓ `\subsection{The basic case $\mathcal{T}_{f_1}M_{-1,1}(\varphi) \cong M_{0,0}(\psi)$}`

The title *is* the theorem. Extreme, and effective in a technical report where the reader scans for a specific result.

---

## P12. Declare the local convention at the top of the section

> ✓ "**Throughout this section $c < b$.**"

One line; removes the need to repeat the hypothesis in every statement that follows.

---

## P13. Composite results get a proof map

> ✓ "Propositions 3.9 and 4.7 **prove necessity of the first two conditions**. In the deep case, Proposition 3.4 **proves necessity of the third**. **Sufficiency** is given by the containment argument of Theorem 4.8 … and the slice argument of Theorem 5.4 …"

Four sentences, and the reader can verify nothing is missing. For a criterion with three conditions proved in five places, this is the difference between a result and a *checkable* result. Note it names the **argument** ("the containment argument", "the slice argument"), not just the label.

---

## P14. Limitations as precise mathematical facts, in a titled remark

The best single technique in either source. A titled remark gives each obstruction an **explicit witness**:

> ✓ "If $\lambda_L = 0$, the extra relation $f_bu = 0$ **produces the proper submodule** $U(f_bw_1)$. If $\kappa = -2$ …, the central operator $T(L-1) - \theta$ **produces a proper image**; the $h_{-1}$-degree calculation **proves that this image neither vanishes nor fills** the quotient. … one may take $0 \ne f_b^kw_1 \in G_c \subsetneq Q_c$ with $k \ge \max(1, \mu+2)$."

Then the limitations — **every one a statement about the mathematics, with a scope**:

> ✓ "**Only under (3.2) is $G_c$ known here** to contain every proper submodule. **In particular**, at the critical level $G_c$ may vanish when $\mu \notin \mathbb{Z}$ although $Q_c$ is still reducible. **The criterion concerns unreduced modules; simplicity after a central reduction is a separate question.**"

Compare S17.5. Both say "here is what I have and have not shown". This one does it in three sentences a reader can **use** — each states exactly which statement is limited, and how.

---

## P15. Key a table by the condition, not by the label

> ✓ `regime | conditions for simplicity` … the row keys are $n \ge N$ and $n < N$ — **the inequalities**, not words like "the deep regime" and "the shallow regime".

The same document uses those words in prose, but its **structure** is keyed by the condition. This is the S16.7 rewrite already applied.

**And the section titles do it too**:

> ✓ `\section{The case $c \le -a-1$: simplicity and the unique maximal submodule}`
> ✓ `\section{The case $-a \le c < b$: simplicity}`

**This is the strongest evidence that the S16.7 rewrite works in practice**: the same author, on the same material, names sections and table rows by the inequality, and the result reads well. The task for the prose is to follow the structure.

---

## P16. Negative hypothesis accounting — say what is **not** needed

The most frequently repeated technique in the audited document (≈8 instances). State a hypothesis, then immediately state that the other parameters are free — or that a condition can be dropped.

> ✓ "If $\lambda_1 \ne 0$, then $\Phi$ is the unique isomorphism sending $v$ to $w_1$. **This holds for every $\kappa \in \mathbb{C}$.**"
> ✓ "**This assertion uses $\eta_N \ne 0$ and $r \ge 1$, but not $\kappa \ne -2$.**"
> ✓ "**Only commutation with $E, H, F$ is needed; $C$ need not be central in $A$.**"
> ✓ "**This does not require $E$ to be locally nilpotent on $D$, or $C$ to act semisimply.**"

**Why it is worth the words**: a reader who does not know which hypotheses are essential will either over-constrain their own reuse of the result, or waste time trying to remove a condition that is load-bearing. Both are expensive. Section-level versions occur too: *"neither $\lambda_L \ne 0$ nor $\kappa \ne -2$ is imposed unless stated"*.

This extends **P1** from notation to hypotheses — the same move: state the boundary of what is claimed.

---

## P17. Fix out-of-range conventions at the point of definition

> ✓ "A character $\chi : S_{a,b} \to \mathbb{C}$ is given by $\kappa = \chi(K)$ and $\lambda_i = \chi(h_i)$, $0 \le i \le L$, **with $\lambda_i := 0$ for $i > L$** and $\chi = 0$ on all root vectors."

One convention, declared once, removes a case split from every later statement mentioning $\lambda_i$. Companion habit — degenerate cases defined where the object is defined:

- `($T_{\le q} = 0$ for $q < 0$)`
- `including the empty sequence` with `$x(\varnothing) = 1$`
- `with $A_0 = 1$`

**Rule**: when a definition has a boundary, define the boundary case in the same breath. One clause; the cheapest available reduction in reader effort.

---

## P18. Discharge a finite check by tabulating — never by asserting

The document's operational substitute for "clearly":

> ✓ "for $[h,e]$, $[e,f]$, $[h,f]$, $[h,h]$ **the weight of the bracket is at most the sum of the weights of its factors: $2 \le 3$, $1 \le 2$, $0 \le 1$, $0 \le 2$**."

Four numbers, and the check is done. Compare *"this is straightforward to verify"*: conveys less and cannot be audited.

For larger mechanical work: **name the type of computation, list its ingredients, and point at a machine-checked artifact**:

> ✓ "The assertions about $Z$ are **direct bracket computations** ($[E,Z] = [F,Z] = [H,Z] = 0$; the displayed values are **verified in `tools/check_regressions.py`**)."

And when it is short enough, write it out — one sentence can carry a whole check: *"commuting $e_i$ past $F^{-1}$ produces the Cartan index $i + b \ge L + 1$ and the central $\delta$-term, which vanish on $u$, and the remaining correction vanishes because $i + 2b > b$, so $f_{i+2b}u = 0$."*

**Three legitimate registers, in order of preference**: write it out → tabulate the finitely many cases → name the computation type and cite the artifact. **"Clearly" is not among them.**

> ⚠️ **Note on the first example**: the technique is right, the original wording was not — the source said "input weights" and "output weights", which is **computer-science register** (see `slop-blacklist.md` S18). The mathematics is a relation between objects, not a flow through a pipe. **Copy the tabulation, not the vocabulary.**

---

## P19. Skip a repetition by naming what changes

> ✓ "In (2.4)–(2.6) **replace $n+1, n+2$ by $n+N, n+2N$.**"
> ✓ "**For $x = e_r$ the same computation uses** …"
> ✓ "**The same strong induction** proves surjectivity …"

The pattern is *"the same X, with Y in place of Z"* — the invariant that changed is named, and the steps that carry over are identified.

**Contrast**: "similarly" alone, or "by the same argument", leaves the reader to work out which substitution and whether anything else changes. Bare "similarly" is acceptable only for a genuinely one-line computation.

---

## P20. Retractions and corrections: flat register, provenance, witness

The register is the same every time — **claim → status → witness**, with no apology:

> ✓ "**An earlier draft claimed** that the subspaces $G^{\ge\nu}$ are submodules and deduced that $G_c$ is never simple… **These claims are withdrawn. A counterexample is given by** the basic model …"
> ✓ "The following **replaces the incorrect formula of an earlier draft**; it was **corrected after the independent audit of 2026-09-22, whose counterexamples are reproduced in** `tools/check_regressions.py`."
> ✓ "The earlier description by the single condition $A_0^{\nu+1}x_{\nu+1} = 0$ **is false in general**. **For an explicit counterexample**, specialize to … **The nonzero assertion uses $e_{-1}u \ne 0$ in this basic model; it is not asserted for every** normalized pair."
> ✓ "These examples **disprove** general tail-stability; **they do not classify** the stable subspaces for every parameter. … **but the value of this socle, the simplicity of $G_c$, and the composition length of $Q_c$ are open.**"

**This is the strongest form of P14.** A withdrawn claim, stated plainly with its witness, is worth more than a silent deletion — the reader learns what was tried and why it fails. Note also that each correction is *scoped in the same sentence*: what survives is stated alongside what does not.

---

## P21. When you do abstract, declare it intentional

> ✓ "**We isolate the abstract mechanism.** Let $\mathfrak{a}$ be a complex Lie algebra containing elements $E, H, F$ with …"

One sentence converts a chapter of computation into a general theorem — by **saying out loud that the abstraction is deliberate**.

**This is the exact counterpart to S16.** S16 objects to abstractions introduced silently, where the reader cannot tell whether the generality does work or hides something. Here the author announces it, and the abstraction is thereby licensed.

**Rule**: the problem with abstraction is not generality — it is *unannounced* generality. If you are abstracting, say so and say why.

---

## P22. Remarks carry mechanisms and are numbered

`\newtheorem{remark}[theorem]{Remark}`: remarks **share the theorem counter and take titles**, which makes them citable and correctable objects rather than asides. All three substantive remarks in the audited document are load-bearing:

- `[Scalar coefficients and inverse powers]` — exposes a naive argument, refutes the trap, forwards to the theorem that repairs it.
- `[A concrete coprimality calculation]` — instantiates an abstract choice of $r$ with actual numbers, ending in a concrete vector.
- `[Three obstructions, with different origins]` — **P14**; gives the criterion's three conditions separate mechanisms.

**Rule**: a remark should carry a mechanism, a concrete instance, or a retraction. If it carries none of the three, it is decoration — cut it.

---

## P23. Parentheses carry the reason, not an aside

> `(all negative powers simultaneously)`
> `(the $\delta$-term vanishes because $b - c \ge 1$)`
> `(the terms with $j \ge 1$ land in $M$)`
> `($F$ is invertible on $D$)`

Every parenthesis in the document does work. A cheap, high-frequency habit worth copying directly.

---

## Summary table

| Positive pattern | Anti-pattern it answers |
|---|---|
| P1 Caveats about what notation does **not** assert | S17.5 confessional scope disclaimers |
| P2 Hypothesis accounting before the theorem | M15 left implicit until the proof |
| P3 Name the method, not the step | S5 "clearly"; and over-expansion |
| P4 Descriptive titles — may be the statement itself | S17.3 promotional labels; S16.7 metaphor titles |
| P5 Sharpness with an explicit witness | S13 over-assertion |
| P6 Bind private labels to explicit symbols | S16.9 standard word, private meaning |
| P7 Precise literature anchoring | S16.4 vague appeal to "the literature" |
| P8 Which proof step used which hypothesis | S17.5 boilerplate disclaimers |
| P9 Open problems: own section, precisely stated | S17.5; S17.6 unfalsifiable slogans |
| P10 Evidence (cited, with counts), not disclaimer | S17.5 disclaimers in abstracts |
| P11 Section title as the statement | S17.3 |
| P12 Local convention declared at section top | repetitive hypotheses |
| P13 Proof map for composite results | S4 / M15 |
| P14 Limitations as precise facts with witnesses | **S17.5 — the model answer** |
| P15 Table keyed by condition, not label | S16.7 case-naming |
| P16 Say which hypotheses are **not** needed | over-constrained reuse; S12 over-hedging |
| P17 Fix out-of-range conventions at the definition | case splits scattered through the text |
| P18 Tabulate the finite check; name the artifact | **S5 "clearly" — the operational substitute** |
| P19 "The same X with Y in place of Z" | "similarly"; S5 |
| P20 Retract flatly: claim → withdrawn → witness | silent deletion; S17.5 |
| P21 Declare an abstraction intentional | **S16 — the licensed form of abstraction** |
| P22 Remarks carry mechanisms; number them | decorative remarks |
| P23 Parentheses carry the reason | padding |

---

## What the two audited documents establish

1. **S5 is achievable at scale.** Zero clarity adverbs in 1777 lines (verified). Whatever else is uncertain about this skill, that target is real.
2. **P1 is a technique, not a reflex** — nine instances in one document.
3. **The S16.7 rewrite is already applied — in the structure, not the prose.** Section titles and table rows key on inequalities; the prose still used the metaphor. The fix is to bring the prose in line with the structure.
4. **Style and vocabulary are separable.** A document can be well written *and* carry dozens of unwanted term occurrences. **Fix them in separate passes**, or a terminology fix will damage good prose.

---

## How to use

This file is the **positive checklist** to `slop-blacklist.md`'s negative one. A document satisfying most of P1–P23 is very unlikely to be suffering from S16, S17, or S18.

**Start with P3, P16, and P18.** They are the highest-frequency habits here, each costs a sentence or less, and none requires restructuring anything.

To extend: add further exemplars, but keep the provenance explicit (genre, reader, date) — a pattern that works in a progress report may not work in a textbook or a referee response.
