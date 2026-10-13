# Provenance and evidence grading

## Read this first — evidence levels

This file distinguishes three levels. **Do not mix them.**

| Level | Meaning | Mark |
|---|---|---|
| **A** | The skill author **verified the quotation verbatim** in the retained extracted text | ✅ verified |
| **B** | Retrieved and reported by an automated research pass, with a URL, but **not page-checked by the author** | ⚠️ single-source report |
| **C** | Not verifiable from retained material, or blocked by a paywall / bot protection | ❌ unverified |

**Where the A-level evidence lives**: `.mathstyle/` in the workspace holds 32 extracted texts and PDFs — Knuth *Mathematical Writing* in full, Merry *Communication in Mathematics* (~150 pp.), the Serre transcript, Halmos, Lombardo, Bertsekas, Friesecke, the UC Davis notes, and Best & Peres 2024. Every ✅ quote below can be found there by searching.

> **Why grade at all**: in one automated research report, several quotations attributed to Tao's blog **could not be found anywhere in the retained text**. Without evidence levels, such items acquire unearned authority and stop being examined — which is worse than citing nothing.

---

## 1. Verified primary sources (level A)

All quotations below were checked verbatim.

### Knuth, Larrabee, Roberts — *Mathematical Writing* (Stanford CS-TR-88-1193)
[PDF](http://infolab.stanford.edu/pub/cstr/reports/cs/tr/88/1193/CS-TR-88-1193.pdf) · retained: `.mathstyle/knuth-mathwriting.txt` (includes Halmos's guest lecture §42)

- ✅ **Rule 2**: "Don't start a sentence with a symbol." Example: `Bad: f'' - a has n distinct zeroes.` / `Good: The polynomial f'' - a has n distinct zeroes.`
- ✅ **Rule 3**: "Don't use the symbols ∴, ∋, ∀, ∃, ⇒; replace them by the corresponding words. (Except in works on logic, of course.)"
- ✅ **Rule 10**: "Don't use the style of homework papers, in which a sequence of formulas is merely listed. Tie the concepts together with a running commentary."
- ✅ **Rule 23**: colons before displayed equations are wrong — "and those colons are wrong."
- ✅ **Rule 24**: "The opening paragraph should be your best paragraph, and its first sentence should be your best sentence." — "Probably the worst way to start is with a sentence of the form 'An X is a Y.'" Example: `Bad: An important method for internal sorting is quicksort.` / `Good: Quicksort is an important method for internal sorting, because…`
- ✅ **Rule 26** (relevant to S16, but see the caveat in §4): "Resist the temptation to use long strings of nouns as adjectives… In general, don't use jargon unnecessarily. Even specialists in a field get more pleasure from papers that use a nonspecialist's vocabulary."
- ✅ **§42, Halmos on "we"**: "Paul says that even better is to avoid both passive voice and the use of 'we' through judicial use of imperative and indicative moods", proposing `We can now prove the following result:` → `Replace z by 7 throughout.` He also agrees that "we" carries a lighter tone and that "he isn't sure he wants that tone in his writing"; the first person singular "should be avoided in formal technical writing."

### Serre — *How to Write Mathematics Badly*
[transcript](https://metaphor.ethz.ch/x/2025/hs/401-3005-00L/texts/serre_how_to_write_mathematics_badly_transcript.pdf) · retained: `.mathstyle/serre.txt`

- ✅ "But you had to see, in the long list of symbols, which one was a verb! So please don't use, if possible, symbols for verbs." His example: a paper whose only verb was `∈`.
- ✅ On construct-before-assert: "because you have switched from the indefinite article to the definite one, you are able to say things that you have really not proven at all."
- ✅ On implicit final steps: "very often, mistakes in proofs are in the non-written part, the implicit part."
- ✅ On detail: "I prefer a more detailed proof on paper. Because on paper, if you find it too long you just go to the next page. But if it is too short and if something is missing you may spend a lot of time trying to reconstruct it."
- ✅ On "the map of Theorem 1" and the definite article presupposing an unproven construction.

### Merry — *Communication in Mathematics* (ETH, 2020)
[PDF](https://www2.math.ethz.ch/will-merry/files/Merry%20-%20Communication%20in%20Mathematics%20(2020).pdf) · retained: `.mathstyle/merry.txt`

- ✅ **"Clearly / obviously"**: such phrases "may come across either as condescending or as displaying a lack of willingness (or ability!) to work out the details", with the audit: "If the statement is obvious, do I need to make the statement at all? / If I do need to make the statement, then is it actually obvious? / Should I perhaps be giving a proof after all?"
- ✅ **Tense**: "Mathematical statements should be universal truths, and are traditionally stated in the present tense."
- ✅ **Verbosity tables** §4.1.1–4.1.2 — the source for `slop-blacklist.md` Part 5.
- ✅ **Confusable pairs** §4.2: its/it's, discreet/discrete, device/devise, compliment/complement, and others.

### Other retained sources (level B — text present, not checked line by line)

| Source | Link | Retained |
|---|---|---|
| Halmos, *How to Write Mathematics* | [PDF](http://www.mat.uc.pt/~pedro/lectivos/LaTeX/how-to-write-mathematics.pdf) | `.mathstyle/halmos-hwm.txt` |
| Bertsekas, *Ten Simple Rules for Mathematical Writing* | [MIT](https://www.mit.edu/~dimitrib/Ten_Rules.html) · [slides](https://www.mit.edu/~dimitrib/Ten_Rules.pdf) | `.mathstyle/ten_rules.txt` |
| Friesecke, *Comments on mathematics writing* | [TUM](https://www.math.cit.tum.de/fileadmin/w00ccg/math/personen/analysis/MathematicsWriting.pdf) | `.mathstyle/tum.txt` |
| Lombardo, *Some tips for writing mathematics* | [Pisa](http://people.dm.unipi.it/lombardo/files/Style.pdf) | `.mathstyle/lombardo.txt` |
| Lee, *A Guide to Writing Mathematics* | [UC Davis](http://web.cs.ucdavis.edu/~amenta/w10/writingman.pdf) | `.mathstyle/ucdavis.txt` |
| UiO MAT2000, *Writing mathematics* | [UiO](https://www.uio.no/studier/emner/matnat/math/MAT2000/v26/lecturenotes/2026-writing.pdf) | `.mathstyle/uio2.txt` |
| Best & Peres, *Mathematical Communication: Remarks from Tao on Writing Papers* (2024) | [PDF](https://bimsa.net/activity/MathematicalCommunication/files/Lec2,3%20--%20Advice%20from%20Tao%20on%20Writing.pdf) | `.mathstyle/tao-advice.txt` |
| Higham, *Handbook of Writing for the Mathematical Sciences*, 3rd ed. | table of contents only | `.mathstyle/higham-toc.txt` |

---

## 2. Not verified (level C) — **do not cite**

| Item | Status |
|---|---|
| **Tao's blog, "introduce notation used three or more times"** | ❌ The retained text contains **no occurrence of the word "notation"**. Could not be verified. **Not included in `style-rules.md`** — only the weaker principle "introduce notation by reuse" is kept, uncredited. |
| **Tao's blog, "27 English renderings of P ∧ Q"** | ❌ Not found in retained text. **Not included.** |
| **Higham's actual text** | ❌ SIAM (403), Manchester (503) and others blocked; only the table of contents was obtained. Anything attributed to Higham is **inferred from section titles** and must not be quoted. |
| **AMS Author Handbook / the Steenrod collection** | ❌ Cloudflare-blocked. |
| **Halmos's full essay** | ⚠️ Only the abridged Indiana 5-page version plus a secondary summary. "Write in spirals" and the sections on language and honesty are known only through those summaries. |
| **Serre's original video / French text** | ❌ Not obtained. |
| **Chinese standards and textbooks on mathematical writing** | ❌ Search hits resolved to library catalogue records or paywalled scans. |

> **Note on the Tao provenance chain**: `.mathstyle/tao-advice.txt` is actually the **Best & Peres 2024 compilation**, not Tao's blog. Quotations labelled "Tao's blog [5]–[10]" therefore rest on a secondary compilation — and in two cases not even on that. Return to terrytao.wordpress.com to check before citing.

---

## 3. Authoritative disagreements

**This section matters more than the rules.** Treating any of these as settled will mislead.

### 3.1 Teachable vs not — a challenge to this entire skill

Halmos: there is "no usable recipe for good writing"; "effective exposition is not a teachable art."
Bertsekas **explicitly disagrees**, advocating a structured style: "Very hard to teach to others… Controversial… Instead we will advocate a **structured style** — Offers specific verifiable rules that students can follow."

**This skill's position**: with Bertsekas — while conceding that **Halmos is right that no rule set can be sufficient.** Rules remove defects; they do not generate insight.

### 3.2 "We" — **this corrected one of this skill's rules**

The original rule ("use we, avoid passive throughout") was oversimplified. There are three positions:

| Position | Source |
|---|---|
| Use "we", meaning *you and me together*, not a formal "I" | Knuth rule 6 ✅ |
| **Better to avoid both the passive and "we"**, using imperative / indicative | Halmos (Knuth §42) ✅ |
| Use "we" unconditionally in formal technical mathematics | Merry ⚠️ |

**`style-rules.md` §Person was rewritten accordingly** — three options, chosen by what reads most naturally.

### 3.3 Over-encapsulation vs "avoid jargon" — a genuine tension

The user's observation (LLMs over-encapsulate and fail to use the field's basic language) and **Knuth rule 26** ("don't use jargon unnecessarily… even specialists get more pleasure from papers that use a nonspecialist's vocabulary") **pull in opposite directions** at first sight.

They are reconcilable once three cases are separated:

| Case | Verdict |
|---|---|
| `ε-δ argument`, `compactness`, `finitely generated` — the field's standard terms | ✅ **Use them.** This is the vocabulary the user wants. |
| `the two-layer localization framework`, `Property (P)`, `tame` for locally finite — invented wrappers | ❌ **Over-encapsulation.** S16. |
| `due to the fact that` instead of `because` — needless formality | ❌ **Knuth's target.** Verbosity, Part 5. |

**Knuth's rule and S16 are about different failure modes and both stand.** Knuth objects to unnecessary jargon where a plain word exists; S16 objects to invented abstractions where the field's established word exists.

### 3.4 Writing in Chinese: whether "我们" is acceptable

- One side: it means author + reader, not the author, and it closes the distance to the reader.
- The other: **forcing a subject where Chinese would omit it is Europeanised Chinese**; in most cases omitting it is more concise.
- Also raised: some journals and universities forbid subjective phrasing including 我们; the older formal register is 笔者.

**Conclusion: there is no unified norm.** The target venue's requirements must be checked. This skill's default use of 我们 is a choice, not a standard.

### 3.5 How much detail a proof needs

Serre wants more detail; Tao's line is that standard lemmas need not be reproved. **Reconcilable only by audience**: Serre means the paper's own new steps, Tao means textbook-standard results.

### 3.6 Other disagreements

- **Proof by contradiction**: Halmos — do not use it when a direct proof is available. ✅ verified
- **Lemma splitting**: Tao folds one-use sub-arguments into the parent proof; **Peres explicitly disagrees**, arguing for modularity so a reader can check part of an argument, forget it, and return. Halmos records his advisors contradicting each other on the same question.
- **Appendices**: Peres says don't; Bertsekas recommends them.
- **Whether motivation is even desirable**: Serre — "I'm not sure I really believe in motivation." Almost everyone else disagrees.
- **Humour**: Knuth permits it under conditions; *Monthly* readers wrote in to protest the informal style.
- **First person singular**: Knuth, Halmos and Merry against; Herb Wilf for.

---

## 4. Rule → source mapping

| Rule | Evidence |
|---|---|
| M1 motivation before definition | ✅ Knuth rule 12 (a definition "motivated only by decree" is "somewhat riskier") ⚠️ reported; B: Friesecke, Best & Peres |
| M3 strategy paragraph | ✅ Knuth rule 10 (prose + running commentary); B: Atiyah rule 10 |
| M5 every formula answerable to prose | ✅ Knuth rules 1, 10; B: Friesecke |
| M7 special case first | B: Best & Peres, Atiyah |
| M13 construct before assert | ✅ Serre |
| M14 no implicit final step | ✅ Serre |
| M16 prove it checkably | ✅ Serre |
| H1 no sentence-initial symbol | ✅ **Knuth rule 2** |
| H2 no symbols as verbs | ✅ **Serre** |
| H3 no logical symbols in prose | ✅ **Knuth rule 3** |
| H4 no colon before a display | ✅ **Knuth rule 23** |
| H9 opening paragraph is the best paragraph | ✅ **Knuth rule 24** |
| H10 proofs are prose | ✅ **Knuth rule 10** |
| W1 use the field's standard vocabulary | ⚠️ **Synthesised** from the user's observation plus Knuth rule 26; see §3.3 for the tension. **No single source states it in this form.** |
| W5 "clearly" audit | ✅ **Merry** |
| Tense | ✅ **Merry** |
| Person | ✅ Knuth rule 6 + **Halmos's counter-position** (§3.2) |
| Verbosity tables | B: Merry §4.1.1–4.1.2 |
| Chinese section | ⚠️ One forum discussion (chaoli.club); **no formal standard** |
| Formalisation of M1–M16, H1–H10, W1–W8; rubric G0–G7 | **This skill's own construction**, no source |

---

## 5. How to extend this file

1. Priority gaps: **Higham's text** (blocked) and **Chinese normative literature** (entirely absent).
2. Return to terrytao.wordpress.com and check the items marked ❌ before including them.
3. **Grade every new citation A/B/C. Level C must never enter the rule files.**
4. On disagreement: **record it, do not unilaterally adopt.** The disagreement is itself information — see §3.2, where a source corrected a rule of this skill.
