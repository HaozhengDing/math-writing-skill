# Bad → Good pairs

**The highest-leverage file in this skill.** Models routinely agree with abstract rules and then fail to apply them; paired examples execute far more reliably.

Read before writing. When unsure how a passage should read, find the closest pair here.

When you learn something new, **add a pair here rather than another abstract clause** to `style-rules.md`.

---

## 0. Over-encapsulation ← start here

The LLM signature failure. See `slop-blacklist.md` S16.

### ✗ Bad
> We introduce a two-layer localization framework. In the first layer we establish a local boundedness principle for the family; the second layer globalizes it via a finite reduction argument. Applying the framework to our setting yields the desired uniform bound.

### ✓ Good
> The function is locally bounded: every point has a neighbourhood on which it is bounded. Since the domain is compact, finitely many such neighbourhoods already cover it, and the largest of their bounds works everywhere. So the bound is uniform.

**Gap**: four invented nouns ("framework", "layer", "principle", "reduction argument") wrapped around one compactness argument. The good version is longer and much better. Run the four tests (S16) — standard name for this meaning? used more than once? does deleting it break a proof? standard in this field, in this sense? The framework fails all four.

### ✗ Bad
> **Definition 2.1.** A pair $(X,Y)$ is called *admissible* if every point of $X$ admits a neighbourhood whose image under $f$ lies in $Y$. We say $X$ is *$Y$-compatible* if such an admissible pair exists.
>
> **Lemma 2.2.** If $(X,Y)$ is admissible, then $X$ is $Y$-compatible.
> **Proof.** Immediate from Definition 2.1. ∎

### ✓ Good
> Every point of $X$ has a neighbourhood mapped into $Y$.

**Gap**: two definitions and a lemma to say one sentence. "Immediate from Definition 2.1" is the tell — a lemma whose proof is the definition was never a lemma. **This is the shape over-encapsulation usually takes.**

### ✗ Bad
> We say a set is *tame* if each of its points has a neighbourhood meeting it in only finitely many members.

### ✓ Good
> A family of sets is *locally finite* if each point has a neighbourhood meeting only finitely many of its members.

**Gap**: "tame" already means several other things in mathematics, and the concept already has a name. Renaming a standard notion makes the text untranslatable back into the field's literature.

### ⚠️ Counter-example — when abstraction is right
> A **filter** on a set $X$ is a non-empty family $\mathcal{F} \subseteq \mathcal{P}(X)$ closed under supersets and finite intersections.

This is genuine abstraction: it is used throughout, it unifies limits, convergence, and ultrafilters, and it carries real content. **The rule is not "never abstract" — it is "abstract when the mathematics demands it, not when the prose wants a noun."**

### Worked illustrations

Three techniques that the abstractions above do not convey on their own. All examples are constructed from standard mathematics.

**Naming a case instead of stating the condition.** The definition is right there — and then the name replaces it everywhere:

### ✗ Bad
> $	ext{deep regime: } n \ge N;\qquad 	ext{shallow regime: } n < N.$
>
> … **Theorem** (simplicity in the deep regime). …

### ✓ Good
> … **Theorem.** For $n \ge N$ and $\lambda 
e 0$, the module $Q$ is simple.

**Gap**: the reader must carry a lookup to follow every later argument. "Deep" and "shallow" are a **spatial metaphor for two ranges of one parameter** — the metaphor does no mathematical work and suggests a structure that is not present. Either write the inequality, or use a label that restates it.

**A mnemonic replacing a formula.** A macro is declared and then used:

### ✗ Bad
> $\depth_T((h-z)v)=\depth_T(v)+1$.

### ✓ Good
> $n_T((h-z)v) = n_T(v) + 1$, where $n_T(w) = \min\{m : T^m w = 0\}$ is the nilpotency order.

**Gap**: the name is smoother to write and loses precisely what needs checking. The macro declaration is a **commitment to the coinage at the tooling level** — greppable, and a strong signal (S16 §Detection).

**A standard word carrying a private meaning** — the most insidious case:

### ✗ Bad
> Throughout, **regular** means satisfying condition (H); the regular case is treated in §4.

### ✓ Good
> Throughout, **regular** means satisfying condition (H). *(Acceptable **only** if bound this way at first use — see `terminology-audit.md` §3.)*

**Gap**: `regular` is standard mathematical English with several established senses, so it **passes the standard-name test superficially** and no reader flags it — while every reader imports the wrong association. A coined new word announces itself as unfamiliar and gets questioned; a hijacked standard word does not, and so escapes review entirely.

**A summary that cannot be false:**

### ✗ Bad
> The reduced theory exhibits a controlled obstruction in the asymptotic profile, and the framework measures that obstruction through the stratification and the residual pairing.

### ✓ Good
> For $\lambda 
e 0$ the quotient is simple; for $\lambda = 0$ it has a unique maximal submodule. The two cases differ by whether a certain integrality condition holds.

**Gap**: in the bad version every content word is invented, so the sentence **contains no checkable content** — it cannot be right or wrong, which is exactly the failure. Test: *can this sentence be false?* If not, it says nothing.

**If you can draw the diagram but cannot state a theorem it encodes, the diagram is packaging.**

---

## 1. Openings

### ✗ Bad
> Throughout the rich history of mathematical analysis, continuity has occupied a central and enduring place. With the continued development of modern mathematics, our understanding has deepened considerably. This section explores these ideas.

### ✓ Good
> We want to capture the idea that a function does not jump. Intuitively: when $x$ is near $a$, $f(x)$ should be near $f(a)$. But "near" needs to be quantified on the real line — how near counts as near? The $\varepsilon$-$\delta$ language is one precise answer to that question.

**Gap**: the bad version contains no mathematical object in three sentences. The good one names the problem in its first sentence and says why new language is needed.

---

## 2. Definitions

### ✗ Bad
> **Definition 1.1.** Let $X$ be a topological space. If every open cover of $X$ has a finite subcover, then $X$ is called compact.

### ✓ Good
> We often need to extract something finite from infinitely many conditions. To show a continuous function attains its maximum on a closed bounded interval, for instance, we want to compress "near every point $f$ is bounded" — a local statement — into finitely many statements. General topological spaces do not allow this: on $(0,1)$ every point has a bounded neighbourhood, yet $f(x) = 1/x$ is unbounded. So we name the property that makes the compression possible:
>
> **Definition 1.1.** Let $X$ be a topological space. If every open cover of $X$ has a finite subcover, then $X$ is called compact.

**Gap**: the good version supplies the difficulty, a counterexample, and why the concept deserves a name. The reader now knows what compactness is *for*.

---

## 3. Openings of proofs

### ✗ Bad
> **Proof.** Let $\varepsilon > 0$. Take $\delta = \varepsilon/2$. If $|x-a| < \delta$, then $|f(x)-f(a)| = |2x-2a| = 2|x-a| < 2\delta = \varepsilon$. ∎

(Mathematically fine, but the reader cannot see where $\delta = \varepsilon/2$ came from, and cannot transfer the trick.)

### ✓ Good
> **Proof.** We need to force $|f(x)-f(a)|$ below $\varepsilon$. Since $f(x)-f(a) = 2(x-a)$, it is enough to make $|x-a|$ smaller than $\varepsilon/2$. So take $\delta = \varepsilon/2$:
>
> Let $\varepsilon > 0$. If $|x-a| < \delta$, then
> $$|f(x)-f(a)| = 2|x-a| < 2\delta = \varepsilon.$$
> This proves continuity.

**Gap**: the good version says what is being controlled and why that $\delta$ suffices. The choice of $\delta$ is now transparent rather than magic.

---

## 4. Strategy paragraph in a long proof

### ✗ Bad
> **Proof.** Let $\{U_\alpha\}$ be an open cover of $X \times Y$. For each $(x,y) \in X \times Y$ there is $\alpha$ with $(x,y) \in U_\alpha$. By definition of the product topology there are open neighbourhoods $V$ of $x$ and $W$ of $y$ with $V \times W \subseteq U_\alpha$. … *(straight into detail)*

### ✓ Good
> **Proof.** Three steps. First, use that a basis for the product topology consists of rectangles, to refine the cover to a cover by rectangles. Second, fix $x$ and use compactness of $Y$ to compress the vertical direction to finitely many pieces. Third, let $x$ vary and use compactness of $X$ to do the same horizontally. Compactness is used exactly twice, once in each direction.
>
> Now the details. Let $\{U_\alpha\}$ be an open cover of $X \times Y$. …

**Gap**: the good version tells the reader how many steps there are and what each uses, before any technique appears. This is the single largest readability difference between human and model mathematical prose.

---

## 5. Formulas must be answerable to prose

### ✗ Bad
> From the above we obtain:
> \[ \sum_{k=1}^{n} \frac{1}{k(k+1)} = \sum_{k=1}^{n}\left(\frac{1}{k} - \frac{1}{k+1}\right) = 1 - \frac{1}{n+1}. \]
> Letting $n \to \infty$, \[ \sum_{k=1}^{\infty} \frac{1}{k(k+1)} = 1. \]

### ✓ Good
> The terms telescope once written in partial fractions:
> \[ \frac{1}{k(k+1)} = \frac{1}{k} - \frac{1}{k+1}. \]
> This form is useful precisely because consecutive terms cancel — the $-\frac{1}{k+1}$ of one term against the $+\frac{1}{k+1}$ of the next — leaving only the first and last:
> \[ \sum_{k=1}^{n} \frac{1}{k(k+1)} = 1 - \frac{1}{n+1}. \]
> As $n \to \infty$ the right-hand side tends to $1$, so the series converges with sum $1$.

**Gap**: the good version says why the decomposition helps and what cancels. The reader can verify the algebra; the *purpose* must not be left to be guessed.

---

## 6. "Clearly"

### ✗ Bad
> Since $f$ is continuous on a compact set, clearly $f$ is uniformly continuous, so there is $\delta > 0$ such that …

### ✓ Good
> Here we use that a continuous function on a compact set is uniformly continuous (Theorem 4.3). That theorem gives $\delta > 0$ such that …

**Gap**: the bad version hides a non-trivial theorem behind one word. A reader who has not met Theorem 4.3 is stuck with no idea what is missing; one who has gets no pointer.

### Counter-example — a legal "obviously"
> If $|x-a| < \delta$ then $2|x-a| < 2\delta$; with $\delta = \varepsilon/2$ this is obviously $\varepsilon$.

**Legal**: what is omitted is pure substitution. **The test is whether the reader is stuck for more than ten seconds, not the word itself.**

---

## 7. Lists vs prose

### ✗ Bad
> The proof is as follows:
> - First, $A$ is open.
> - Second, since $A$ is open, $A^c$ is closed.
> - Finally, $A^c$ closed gives the result.

### ✓ Good
> We argue in two steps. First, $A$ is open: … . With that in hand, $A^c$ is closed immediately. But $A^c$ closed is exactly the claim, so we are done.

**Gap**: the bad version chops a **sequential** chain into **parallel** bullets, and the logical connectives ("since", "hence") are eaten by the formatting. Lists suit cases, not chains.

---

## 8. Empty evaluations

### ✗ Bad
> This is a profound and beautiful theorem, revealing deep connections between algebra and geometry.

### ✓ Good
> The theorem links two objects that appear unrelated: the left side depends only on the topology of $X$, the right side only on the group structure. That is what lets topological information be converted into algebraic computation, and it is the basis of every application that follows.

**Gap**: the good version never says "profound" — it **says what is profound**. Evaluations carry no information; reasons do.

---

## 9. Nominalization

### ✗ Bad
> The carrying out of an analysis of the behaviour of $f$ at infinity is achieved by means of a consideration of the growth of the sequence.

### ✓ Good
> We analyse how $f$ behaves at infinity by looking at how fast the sequence grows.

**Gap**: `-tion of` chains where verbs would do. See `style-rules.md` W3.

---

## 10. Introducing notation

### ✗ Bad
> For convenience we fix the following notation: $X$ a topological space, $Y$ a set, $f : X \to Y$ a map, $\mathcal{U}$ an open cover of $X$, $\mathcal{V}$ a finite subcover, $\mathcal{W}$ a family of open subsets of $Y$, $\varepsilon > 0$, $\delta > 0$, $n \in \mathbb{N}$, …
> *(three of these are used in the next thirty pages)*

### ✓ Good
> Fix a topological space $X$. To discuss compactness we need a name for a cover: a family $\mathcal{U}$ of open sets is an **open cover** of $X$ if $X = \bigcup \mathcal{U}$.
> *(further symbols are introduced when first needed)*

**Gap**: a notation table is a reference tool, not reading material. Introduce each symbol at its first genuine use.

---

## 11. Metadiscourse

### ✗ Bad
> We now turn to the three main aspects of this topic. Let us begin by considering the first of these.

### ✓ Good
> We first define compactness, then show it is preserved by continuous maps — which is where every application in this section comes from.

**Gap**: an informative preview says what will be proved and why it matters. A roll-call says nothing.

---

## 12. Uncertainty

### ✗ Bad (presenting the unproved as proved)
> Hence the estimate holds in the general nonlinear case as well.

### ✓ Good
> Hence the estimate holds in the linear case. We conjecture it also holds nonlinearly, but the argument above uses linearity in line 3 and does not extend directly; that would need an extra hypothesis or a new idea.

**Gap**: **this is the most dangerous anti-pattern of all.** Over-assertion is far more harmful than empty phrasing, because it lets an open problem be read as settled.

---

## 13. Sentence-initial symbols and symbols as verbs

### ✗ Bad
> $f'' - a$ has $n$ distinct zeroes. Also, $x \in \mathbb{Q}$.

### ✓ Good
> The polynomial $f'' - a$ has $n$ distinct zeroes. Also, $x$ is rational.

**Gap**: Knuth rule 2, and Serre's rule about verbs. In the second bad sentence **the only verb is `∈`**.

---

## 14. Logical symbols in running prose

### ✗ Bad
> Hence $\forall \varepsilon > 0,\ \exists \delta > 0$ such that $\forall x,\ |x - x_0| < \delta \Rightarrow |f(x) - f(x_0)| < \varepsilon$.

### ✓ Good
> Hence for every $\varepsilon > 0$ there exists $\delta > 0$ such that whenever $|x - x_0| < \delta$ we have $|f(x) - f(x_0)| < \varepsilon$.

**Gap**: Knuth rule 3. Quantifiers inside a **displayed** formula are fine; as connectives inside a sentence they destroy the grammar.

---

## 15. The blah test

### ✗ Bad
> Consider $S_n$, $q < p$. From $n \to \infty$ we get $a_n \to a$; $\varepsilon$ arbitrary, hence the claim.

### ✓ Good
> Consider $S_n$, where $q < p$. Since $n \to \infty$ gives $a_n \to a$, and $\varepsilon$ was arbitrary, the claim follows.

**Gap**: replace the formulas with "blah" and the bad version reads *"Consider blah, blah. From blah we get blah; blah arbitrary, hence the claim."* — unreadable. The good version still reads. This is Knuth rule 13 and the fastest test for whether formulas sit inside sentences.

---

## 16. Construct first, assert after

### ✗ Bad
> **Theorem 1.** There exists an isomorphism $f : A \to B$.
> **Theorem 2.** $f$ preserves multiplication.
>
> *(Reader: which $f$? Why "the map $f$" all of a sudden?)*

### ✓ Good
> We construct a map $f : A \to B$ explicitly, by setting … *(construction)*. We then check that this $f$ is a bijection and preserves multiplication; hence it is an isomorphism.

**Gap**: Serre's point — the two-part form slides the reader from the indefinite to the definite article, and "because you have switched from the indefinite article to the definite one, you are able to say things that you have really not proven at all." **Build the animal first, then describe it.**

---

## 17. The last step is not optional

### ✗ Bad
> … from the estimate above together with Lemma 2, and compactness of $A$, the theorem follows. ∎
>
> *(One step is missing: compactness gives a finite subcover, and one must say that this subcover does cover $A$.)*

### ✓ Good
> … from the estimate above together with Lemma 2 we obtain a finite subfamily $\{U_{i_1},\dots,U_{i_k}\}$. Since $A \subseteq \bigcup_j U_{i_j}$ and each $U_{i_j}$ is open, this is precisely what compactness of $A$ asserts. The theorem follows. ∎

**Gap**: Serre — "very often, mistakes in proofs are in the non-written part, the implicit part." **Proof errors hide in the step you did not write down.**

---

## How to use this file

- To fix a passage, **first locate which bad example it most resembles**, then rewrite to that structure. Do not polish sentence by sentence.
- When the user says "this still reads wrong", **add the case here**. This file should grow with use.
