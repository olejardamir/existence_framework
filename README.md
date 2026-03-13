# existence_framework
The existence framework that can be used to explore different models and their mindsets


# Existence Frameworks, Verifiers, and Non-Contradiction

In simple terms, it is possible to define something as **existent** in more than one mathematically coherent way, and those meanings do not have to agree. Because of that, before arguing against someone’s claim about existence, it helps to understand **which framework of existence** they are using and then reason inside that framework.

This also applies to **game semantics**. You can construct a mathematically valid framework in which your chosen notion of existence does **not** match the condition “Verifier has a winning strategy,” and the two can even assign opposite truth values to some statements.

---

## Table of Contents

- [Core Idea](#core-idea)
- [Game Semantics and a Different Existence Policy](#game-semantics-and-a-different-existence-policy)
  - [1. Game Semantics Validates a Specific Existential Rule](#1-game-semantics-validates-a-specific-existential-rule)
  - [2. Define a Different but Coherent Notion of Existence](#2-define-a-different-but-coherent-notion-of-existence)
  - [3. Why It Can Disagree with Game Semantics](#3-why-it-can-disagree-with-game-semantics)
- [The Master Schema](#the-master-schema)
- [How to Build Any Existence Meaning](#how-to-build-any-existence-meaning)
  - [Step 1 — Write the Target Meaning](#step-1--write-the-target-meaning)
  - [Step 2 — Choose the Inhabitant Kind](#step-2--choose-the-inhabitant-kind)
  - [Step 3 — Choose the Scope](#step-3--choose-the-scope)
  - [Step 4 — Choose the Evidence Requirement](#step-4--choose-the-evidence-requirement)
  - [Step 5 — Add Admissibility Constraints](#step-5--add-admissibility-constraints)
  - [Step 6 — Assemble `θ`](#step-6--assemble-θ)
  - [Step 7 — Define `V_θ(e, X)` as a Checklist](#step-7--define-v_θe-x-as-a-checklist)
  - [Step 8 — State the Final Existence Meaning](#step-8--state-the-final-existence-meaning)
- [Worked Mini-Examples](#worked-mini-examples)
  - [Example A: Classical Non-Emptiness](#example-a-classical-non-emptiness)
  - [Example B: Computable Inhabitance](#example-b-computable-inhabitance)
  - [Example C: Global Point](#example-c-global-point)
  - [Example D: Local Existence](#example-d-local-existence)
  - [Example E: Modal Actualist Existence](#example-e-modal-actualist-existence)
- [When Two Existence Meanings Do Not Contradict Each Other](#when-two-existence-meanings-do-not-contradict-each-other)
  - [Condition 1: Same Base Universe and Scope](#condition-1-same-base-universe-and-scope)
  - [Condition 2: Comparable Evidence and Constraints](#condition-2-comparable-evidence-and-constraints)
  - [Condition 3: Do Not Claim Equivalence Without Equivalence](#condition-3-do-not-claim-equivalence-without-equivalence)
  - [Condition 4: Avoid Complementary Constraints](#condition-4-avoid-complementary-constraints)
- [Practical Fast Test](#practical-fast-test)
- [Conclusion](#conclusion)

---

## Core Idea

An “existence meaning” can be treated as a formally defined rule for what counts as an admissible witness.

That means two people can both be using mathematically valid systems, while still disagreeing about whether something “exists,” simply because their systems use different witness policies, different scopes, or different admissibility conditions.

This is not necessarily inconsistency. It may simply mean they are **not using the same existential operator**.

---

## Game Semantics and a Different Existence Policy

### 1. Game Semantics Validates a Specific Existential Rule

In standard game semantics for first-order logic,

\[
\exists x\,P(x)
\]

is true exactly when the **Verifier** can choose a value of \(x\) that makes \(P(x)\) true. In other words, truth is tied to the Verifier having a winning move or winning strategy at that stage.

So, in the usual game-theoretic reading of the ordinary existential quantifier:

- existence means there is some admissible witness,
- and the Verifier can select it successfully.

---

### 2. Define a Different but Coherent Notion of Existence

Now define a different existential quantifier:

\[
\exists_{\mathrm{def}} x\,P(x)
\]

to mean:

> there exists a **definable** element satisfying \(P(x)\)

with semantics:

\[
M \models \exists_{\mathrm{def}} x\,P(x)
\iff
\text{there is } a \in D_M \text{ definable in } M \text{ such that } M \models P(a).
\]

This is mathematically coherent. The only thing that changed is the rule for what counts as an admissible witness.

The system is still well-defined, but its notion of existence is now stricter than the ordinary one.

---

### 3. Why It Can Disagree with Game Semantics

Game semantics for the ordinary existential quantifier \(\exists\) does **not** require the witness to be definable.

So there can be structures in which:

- some \(a\) satisfies \(P(a)\), so the Verifier has a winning move in the usual \(\exists\)-game,
- but no such satisfying \(a\) is definable, so \(\exists_{\mathrm{def}} x\,P(x)\) is false.

Therefore, the two notions of existence can assign opposite truth values to the same formula.

### Important nuance

This does **not** mean the framework is inconsistent.

It means only that the new framework is **not using the same existential quantifier** that ordinary game semantics is designed to interpret.

---

# The Master Schema

Use the following schema for any chosen notion of existence:

\[
\boxed{
\exists_{\theta}(X)
\;:\Longleftrightarrow\;
\exists e\;V_{\theta}(e,X)
}
\]

Where:

- \(X\): the thing you want to say “has something”  
  (set, type, object, sheaf, structure, and so on)
- \(e\): a candidate **inhabitant package**  
  (witness + context + certificate)
- \(\theta\): the parameter bundle that defines your chosen meaning of existence
- \(V_{\theta}\): the verifier determined by \(\theta\)

This is the general template.

---

# How to Build Any Existence Meaning

## Step 1 — Write the Target Meaning

State the intended meaning in one sentence, without mentioning predicates.

Examples:

- “Exists means: there is an element.”
- “Exists means: there is a computable element.”
- “Exists means: there is a global point.”
- “Exists means: there is a local section on some cover.”
- “Exists means: there is an element in some possible world.”

---

## Step 2 — Choose the Inhabitant Kind

Choose exactly one witness type.

Options:

- **Element**: \(a \in X\)  
  set/domain style
- **Term**: \(t : X\)  
  type theory
- **Morphism / point**: \(1 \to X\)  
  category/topos
- **Section**: \(s \in X(U)\)  
  sheaf semantics
- **Strategy**: \(\sigma\)  
  game semantics
- **Assignment update / choice function**: \(F\)  
  team or dependence semantics

This determines the shape of the **witness component** of \(e\).

---

## Step 3 — Choose the Scope

Choose where the witness must exist.

Options:

- **Here / absolute**: in the current domain or context
- **At world \(w\)**: world-relative domain \(D(w)\)
- **In some world**: \(\exists w\)
- **In all worlds**: \(\forall w\)
- **In some model**: \(\exists M \models F\)
- **In all models of a class \(\mathcal{K}\)**: \(\forall M \in \mathcal{K}\)
- **Locally on a cover**: \(\exists \{U_i\}\) with local witnesses

This determines the **context component** of \(e\).

---

## Step 4 — Choose the Evidence Requirement

Choose one certificate mode.

Options:

- **None**  
  truth-conditional only
- **Proof object**  
  derivation tree, proof term
- **Program**  
  algorithm producing a witness
- **Trace**  
  verification transcript, reduction trace, or computation log
- **Section data**  
  cover plus compatible local data
- **Strategy certificate**  
  proof object for a winning strategy

This determines the **certificate component** of \(e\).

---

## Step 5 — Add Admissibility Constraints

Choose zero or more additional constraints.

Options:

- **Computability**  
  witness must be computable
- **Resource bound**  
  time \(\le k\), space \(\le k\), description length \(\le k\), proof length \(\le k\)
- **Definability**  
  witness must be definable, with or without parameters
- **Canonicity**  
  witness must be canonical or in normal form
- **Uniqueness**  
  uniqueness, or uniqueness up to isomorphism
- **Stability**  
  witness persists under allowed extensions or refinements

These become fields inside \(\theta\).

---

## Step 6 — Assemble `θ`

Use the standard shape:

\[
\theta =
(\mathsf{Kind},\ \mathsf{Scope},\ \mathsf{Evidence},\ \mathsf{Constraints})
\]

Where:

- \(\mathsf{Kind}\in\{\textsf{element, term, morphism, section, strategy, function}\}\)
- \(\mathsf{Scope}\in\{\textsf{here, world }w, \exists w, \forall w, \exists M, \forall M\in\mathcal{K}, \textsf{local cover}\}\)
- \(\mathsf{Evidence}\in\{\textsf{none, proof, program, trace, section-data, strategy}\}\)
- \(\mathsf{Constraints}\) is a possibly empty list such as:
  \([\textsf{computable}, \textsf{time}\le k, \textsf{definable}, \dots]\)

---

## Step 7 — Define `V_θ(e, X)` as a Checklist

Always define the verifier as a conjunction of mechanical checks:

\[
V_{\theta}(e,X)\equiv
\mathsf{ScopeOK}
\wedge
\mathsf{KindOK}
\wedge
\mathsf{EvidenceOK}
\wedge
\mathsf{ConstraintsOK}
\]

Each part is interpreted as follows.

### 7A) `KindOK`

- **element**: witness \(a\) is in \(X\)
- **term**: witness \(t\) typechecks as \(X\)
- **morphism**: certificate contains a morphism \(1 \to X\)
- **section**: certificate contains a section \(s \in X(U)\)
- **strategy**: certificate is a winning strategy for \(X\)
- **function**: certificate contains a function \(F\) of the required form

### 7B) `ScopeOK`

- **here**: no extra context
- **world \(w\)**: witness lives in \(X(w)\)
- **some world**: certificate includes \(w\) and witness in \(X(w)\)
- **all worlds**: evidence must be uniform across worlds
- **some model**: certificate includes \(M\) and witness in \(X^M\)
- **all models**: evidence must be uniform across the model class
- **local cover**: certificate includes cover \(\{U_i\}\) and local witnesses, plus compatibility if required

### 7C) `EvidenceOK`

- **none**: nothing further required
- **proof**: certificate is a derivation that witness is valid
- **program**: certificate is code, plus proof or argument that it halts and outputs a witness
- **trace**: certificate is an accepted verifier transcript
- **section-data**: cover plus gluing or compatibility data
- **strategy**: proof that the strategy wins

### 7D) `ConstraintsOK`

Apply each chosen constraint:

- **computable**: witness or program is computable
- **time \(\le k\)**: execution halts within \(k\)
- **definable**: witness is definable by some formula \(\varphi\), with uniqueness if required
- **canonical**: witness equals the canonical representative
- **stability**: property survives allowed extensions or refinements

---

## Step 8 — State the Final Existence Meaning

Once \(\theta\) and \(V_{\theta}\) are fixed, the meaning is simply:

\[
\exists_{\theta}(X)
\text{ holds iff }
\exists e\;V_{\theta}(e,X).
\]

That is the selected interpretation of the bare phrase “there exists.”

---

# Worked Mini-Examples

## Example A: Classical Non-Emptiness

- Target: “something exists in \(X\)”
- \(\theta=(\textsf{element},\textsf{here},\textsf{none},[])\)
- \(V_{\theta}(e,X)\): witness \(a \in X\)
- Result:

\[
\exists_{\theta}(X)\iff X\neq\varnothing
\]

---

## Example B: Computable Inhabitance

- Target: “a computable inhabitant exists”
- \(\theta=(\textsf{element},\textsf{here},\textsf{program},[\textsf{computable}])\)
- \(V\): program outputs \(a\in X\) and halts
- Result: \(X\) has a computable element

---

## Example C: Global Point

- Target: “\(X\) has a global element”
- \(\theta=(\textsf{morphism},\textsf{here},\textsf{none},[])\)
- \(V\): certificate contains a morphism \(1\to X\)
- Result: \(X\) is globally inhabited

---

## Example D: Local Existence

- Target: “\(X\) has a local section somewhere”
- \(\theta=(\textsf{section},\textsf{local cover},\textsf{section-data},[])\)
- \(V\): there is a cover \(\{U_i\}\) and sections \(s_i \in X(U_i)\)
- Result: \(X\) is locally inhabited, even if it has no global point

---

## Example E: Modal Actualist Existence

- Target: “something exists at world \(w\)”
- \(\theta=(\textsf{element},\textsf{world }w,\textsf{none},[])\)
- \(V\): witness \(a \in X(w)\)
- Result: \(X\) is inhabited at \(w\)

---

This procedure gives a mechanical method for generating any existence interpretation you want:

1. choose **kind**
2. choose **scope**
3. choose **evidence**
4. choose **constraints**
5. encode them into \(\theta\)
6. define \(V_{\theta}\) as the resulting checklist

---

# When Two Existence Meanings Do Not Contradict Each Other

Let an existence meaning be generated by the schema:

\[
\exists_{\theta}(X)
\;:\Longleftrightarrow\;
\exists e\;V_{\theta}(e,X).
\]

Suppose two meanings \(A\) and \(B\) are defined by \(\theta_A\) and \(\theta_B\).

The question is:

> When do these two meanings avoid contradiction?

The answer is: they must be related in a way that prevents one from saying “true” and the other from saying “false” while still pretending both are the same claim.

## Condition 1: Same Base Universe and Scope

They must quantify over the same underlying type of inhabitant and the same contextual domain.

That means:

- same inhabitant kind  
  (element vs term vs morphism vs section vs strategy)
- same scope policy  
  (here vs world \(w\) vs some world vs local cover vs some model vs all models in a class)

If these differ, disagreement may happen simply because the two frameworks are talking about different kinds of existence.

A classic example is **global** versus **local** existence.

---

## Condition 2: Comparable Evidence and Constraints

Their verifiers should be related by implication over the same candidate evidence space:

\[
\forall e,X\;
\big(V_A(e,X)\Rightarrow V_B(e,X)\big)
\quad\text{or}\quad
\forall e,X\;
\big(V_B(e,X)\Rightarrow V_A(e,X)\big).
\]

This means one notion is a **refinement** of the other rather than an unrelated competitor.

### Consequences

If

\[
V_A(e,X)\Rightarrow V_B(e,X),
\]

then

\[
\exists_A(X)\Rightarrow \exists_B(X)
\]

for all \(X\).

So the two meanings may differ in strength, but they are not incompatible.

---

## Condition 3: Do Not Claim Equivalence Without Equivalence

If you want to treat two meanings as literally the same existence notion, implication is not enough. You need equivalence:

\[
\forall e,X\;
\big(V_A(e,X)\Leftrightarrow V_B(e,X)\big)
\quad\Rightarrow\quad
\forall X\;
\big(\exists_A(X)\Leftrightarrow \exists_B(X)\big).
\]

If you only have one-way implication and still claim the meanings are identical, then the problem is not mathematical inconsistency but conceptual misidentification.

---

## Condition 4: Avoid Complementary Constraints

A common source of contradiction is using complementary witness requirements, such as:

- \(A\): there exists an inhabitant with property \(C\)
- \(B\): there exists an inhabitant with property \(\neg C\)

and then applying both to an \(X\) designed so only one side can hold.

To avoid this, constraints should be:

- **compatible**, meaning their intersection is not systematically empty, or
- **nested**, meaning one implies the other

---

# Practical Fast Test

Given \(\theta_A\) and \(\theta_B\), the two meanings are non-contradictory if:

1. **Same what / where**  
   same inhabitant kind and same scope domain or class
2. **Same candidate space**  
   evidence objects \(e\) live in the same format
3. **Verifier nesting**  
   either \(V_A \Rightarrow V_B\) or \(V_B \Rightarrow V_A\)
4. **No forced equivalence**  
   only claim equivalence if you actually have \(V_A \Leftrightarrow V_B\)

These conditions prevent situations in which one framework says \(A(X)\) is true and the other says \(B(X)\) is false, while still pretending both statements express the same notion of existence.

---

# Conclusion

Different existence claims can be mathematically valid while still disagreeing, because existence is not a single fixed notion once you allow the witness policy, scope, evidence, or admissibility constraints to change.

The right way to handle such disagreements is:

1. identify the framework,
2. identify the existential policy,
3. compare the verifier structure,
4. check whether the two meanings are refinements, equivalents, or genuinely different quantifiers.

That is the key distinction:

- **different truth values do not automatically imply inconsistency**
- they may simply reflect **different meanings of existence**
