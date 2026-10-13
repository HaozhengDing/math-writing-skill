# Genre skeletons

Different genres make different **contracts with the reader**. The skeleton follows from the contract.

Fix the genre before writing. If it is unclear, ask.

---

## The universal micro-structure

Every "piece of mathematics" that gets fully developed has three parts:

```
motivation (why we need it) → content (definition / theorem / proof) → digestion (examples, counterexamples, uses)
```

Models routinely supply only the middle. **Adding the first and third is the fastest available readability gain.**

---

# G0 — Organizing existing material

**The most common and most painful job.** The user has notes, drafts, fragmentary proofs, several sources, and wants one coherent document.

**Reader contract**: the reader never sees the sources. The finished text must stand alone. But the mathematics must be *the same mathematics*.

**The real risk here is not prose. It is structure and fidelity.**

```
0. Fix reader and genre     (which skeleton below will the output follow?)
1. Inventory                what mathematical items does the material actually contain?
2. Dependency analysis      what depends on what? produce a partial order
3. Conflict detection       notation collisions, contradictions, duplicates, register drift
4. Gap marking              which arguments are incomplete? MARK them — do not fill them
5. Structure design         reorder to the target skeleton respecting the partial order
6. Write                    applying the discourse moves
7. Deliver                  notation-change table + gap list + suspected-error list
```

**Hard constraints**
- The mathematics does not change.
- Gaps are **marked**, not filled with generated content.
- Suspected errors are **listed**, not silently corrected.
- Unifying notation requires a mapping table.

**Why step 4 matters most**: a fabricated proof inside an otherwise finished-looking document is far worse than a visible gap. The gap is honest; the fabrication is not, and it will be trusted.

---

# G1 — Textbook section

**Reader contract**: starts from nothing, willing to follow, free to look back. **No step may require outside knowledge.**

```
1. Introduction      start from a concrete problem; name the inadequacy of existing tools
2. Definition        the concept, with an example and a non-example
3. Basic properties  simple propositions that build familiarity (the "feel" stage)
4. Main theorem      statement + why we want it + proof
5. Examples          at least two: a typical one and a boundary one
6. Connections       where this sits in the course
7. Exercises         increasing difficulty
```

- Cross-section citations must be **restated in place** (M12).
- The main theorem needs a "why do we want this" before it.
- The key idea in the proof must be flagged explicitly (M11).
- Notation on demand (M6), never dumped at the head of a chapter.

---

# G2 — Lecture note

**Reader contract**: just attended the lecture, needs to reconstruct it. **May be more informal and faster than a textbook; may not be vaguer.**

```
1. The problem this lecture addresses (1–2 sentences)
2. The route we take today
3. Content (as G1, more compactly)
4. Key points to remember
5. Common misconceptions (optional, but very valuable)
```

- Lecture notes may say "last time we saw …"; a textbook may not (it must be self-contained).
- The **common misconceptions** section is something only lecture notes can do well — write it directly: "Many people expect X; in fact Y."

---

# G3 — Paper

**Reader contract**: a specialist with limited time, who will read selectively. **May cite prior results; may not be vague.**

```
1. Abstract          problem + result + method, one sentence each
2. Introduction
   - what the problem is, and why it matters (really, not "is important")
   - what was known, and where it got stuck
   - what this paper does — contributions stated so they can be checked
   - outline of the method (the core idea; key constructions allowed here)
   - relation to existing work
3. Preliminaries     definitions and notation (centralizing these is legitimate — they are tools)
4. Main results      statements, grouped or dispersed as the structure dictates
5. Proofs            strategy paragraph first (M3)
6. Examples          verify non-emptiness; demonstrate sharpness
7. Discussion        limitations, open problems
```

- The **Introduction is the most important part**. A referee decides there.
- Contributions must be **decidable**: "we prove X", not "we study X".
- Characterization of prior work must be specific and fair — avoid the sales register ("however, they all overlooked …").
- Hypotheses must be **complete**, not revealed mid-proof.
- Papers cite rather than restate (opposite of G1).

---

# G4 — Survey

**Reader contract**: wants a map quickly, does not intend to read every detail. **Must have a point of view; may not be a list.**

```
1. Why a survey now — where is the turning point in the field
2. The map: divide the area into strands, and say on what basis
3. Strand by strand: core question → main results → technical character → key references
4. Comparison and connections between strands
5. Open problems — real ones, not courtesies
6. Reading paths for readers of different backgrounds
```

- **Chronological listing of references is not a survey.** The choice of dividing dimension *is* the contribution.
- Every claim needs representative references.
- The author's judgement (which strand looks more promising) must be given, with reasons.

---

# G5 — Solution write-up

**Reader contract**: has thought about the problem, possibly got stuck; wants the *idea*, not just the answer.

```
1. The answer         first — the reader wants to know immediately
2. Where the idea comes from    the core value of the write-up
3. Full argument      rigorous, step by step
4. Check              verify plausibility: special cases, limiting behaviour, dimensions
5. Commentary         what general technique was used; whether it generalizes
```

- **Never just the answer.** "How one would think of this" is the difference between a solution and an answer.
- Step 4 is the most frequently omitted and catches a large share of errors.
- If several methods work, compare their applicability rather than listing them side by side.

---

# Genre quick reference

| User says | Genre | Primary risk |
|---|---|---|
| "write up these notes" / "整理成文" | **G0** | Changing the mathematics; filling gaps |
| "write it like a textbook / lecture note" | G1 / G2 | Skipped steps, missing motivation |
| "write me a paper" | G3 | Empty introduction; undecidable contributions |
| "summarize this area" | G4 | Degenerates into a reference list |
| "how do I solve this" | G5 | Answer without method |
| "this proof is unclear" | local rewrite (A) | Fixing wording instead of structure |
