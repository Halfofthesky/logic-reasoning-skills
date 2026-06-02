---
name: formal-logic-solver
description: >
  Solve formal logic problems: symbolize English arguments, build truth tables, construct
  proofs using natural deduction, evaluate categorical syllogisms, and test validity in
  propositional and first-order logic. Use this skill whenever the user asks to "prove this
  is valid," "build a truth table," "symbolize this argument," "is this a valid syllogism,"
  "construct a proof," "translate into logical notation," "check this inference," or presents
  a formal logic problem from a textbook, exam, or their own reasoning. Also trigger when
  the user asks about specific inference rules (modus ponens, modus tollens, etc.),
  logical equivalences (De Morgan's, contraposition, etc.), or categorical logic (Venn
  diagrams, the square of opposition, syllogistic forms). This skill handles the formal/
  mechanical side of logic — symbolization, truth tables, proofs, and syllogism testing.
  For informal argument evaluation, use argument-analyst. For fallacy detection, use
  fallacy-detector.
---

# Formal Logic Solver

Solve formal logic problems using standard methods from propositional logic, categorical
logic, and first-order logic. This skill synthesizes methods from DeLancey (*A Concise
Introduction to Logic*), Van Cleave (*Introduction to Logic and Critical Thinking* Ch. 2),
and Knachel (*Fundamental Methods of Logic* Ch. 3-4).


## Task Router

Determine what the user needs and go to the appropriate section:

- **"Symbolize / translate this"** → Section 1: Symbolization
- **"Is this valid?" (short argument)** → Section 2: Truth Tables
- **"Prove this" / "construct a proof"** → Section 3: Natural Deduction Proofs
- **"Is this syllogism valid?"** → Section 4: Categorical Logic
- **"Translate into predicate logic"** → Section 5: First-Order Logic
- **"What rule is this?"** → Section 6: Quick Reference


## Section 1: Symbolization (English → Formal Notation)

### Connectives

| English | Symbol | Name | Type |
|---------|--------|------|------|
| and, but, yet, moreover, although, while | `∧` (or `·`) | Conjunction | Both conjuncts must be true |
| or, either...or, unless | `∨` | Disjunction | At least one disjunct true (inclusive or) |
| not, it is not the case that, fails to | `¬` (or `~`) | Negation | Reverses truth value |
| if...then, implies, only if, sufficient for | `→` (or `⊃`) | Conditional | False only when antecedent true and consequent false |
| if and only if, just in case, necessary and sufficient | `↔` (or `≡`) | Biconditional | Both same truth value |

### Translation Rules

**Step 1:** Identify atomic propositions (simple declarative sentences that are
either true or false). Assign each a capital letter.

**Step 2:** Identify the logical connectives in the English. Watch for:
- "unless P, Q" = "if not P then Q" = `¬P → Q` = `P ∨ Q`
- "P only if Q" = "if P then Q" = `P → Q` (NOT "if Q then P")
- "P if Q" = "if Q then P" = `Q → P`
- "neither P nor Q" = `¬P ∧ ¬Q` = `¬(P ∨ Q)`
- "not both P and Q" = `¬(P ∧ Q)` = `¬P ∨ ¬Q`
- "but" and "although" are logically just conjunction despite their rhetorical force

**Step 3:** Determine the main connective (the one with widest scope). Use
parentheses to eliminate ambiguity. Operator precedence (tightest to widest):
`¬`, `∧`, `∨`, `→`, `↔`

**Common pitfalls:**
- "Only if" is NOT the same as "if." "P only if Q" means P → Q.
- English "or" is usually inclusive. Only use exclusive or if context demands it.
- "If" in the consequent position: "Q if P" means P → Q (the "if" attaches to the antecedent).
- Nested conditionals need careful parenthesization.


## Section 2: Truth Tables

### Procedure

**Step 1:** Count the distinct atomic propositions (n). The table will have 2^n rows.

**Step 2:** Set up reference columns for each atomic proposition. Fill in
systematically: first column alternates T/F in blocks of 2^(n-1), second in
blocks of 2^(n-2), etc. Last column alternates every row.

**Step 3:** Add a column for each premise and one for the conclusion. Compute
truth values row by row, working from innermost connectives outward.

**Truth value rules:**

| p | q | p ∧ q | p ∨ q | p → q | p ↔ q | ¬p |
|---|---|-------|-------|-------|-------|----|
| T | T |   T   |   T   |   T   |   T   | F  |
| T | F |   F   |   T   |   F   |   F   | F  |
| F | T |   F   |   T   |   T   |   F   | T  |
| F | F |   F   |   F   |   T   |   T   | T  |

The critical one: **a conditional is false ONLY when the antecedent is true
and the consequent is false.** In all other cases it is true.

### Validity Test

An argument is **valid** if and only if there is NO row where all premises are
true and the conclusion is false.

- If such a row exists: **INVALID**. That row is a counterexample (a formal
  counterexample, not just an informal one).
- If no such row exists: **VALID**.

### Other Truth Table Tests

- **Tautology**: true on every row (e.g., `P ∨ ¬P`).
- **Contradiction**: false on every row (e.g., `P ∧ ¬P`).
- **Contingent**: true on some rows, false on others.
- **Logical equivalence**: two formulas have identical truth values on every row.

### Short-Cut: Indirect Truth Table Method

For complex arguments, instead of building the full table:
1. Assume the argument is invalid (all premises true, conclusion false).
2. Assign T to all premises and F to the conclusion.
3. Work backwards to determine what truth values the atoms must have.
4. If you reach a contradiction, the argument is valid.
5. If you find a consistent assignment, the argument is invalid (and that
   assignment is your counterexample).


## Section 3: Natural Deduction Proofs

### The 8 Basic Inference Rules

These rules can only be applied to WHOLE lines (main connective), not to
components within a line.

**Rules using the conditional (→):**

```
MODUS PONENS (MP)          MODUS TOLLENS (MT)
1. p → q                   1. p → q
2. p                       2. ¬q
∴  q                       ∴  ¬p
```

```
HYPOTHETICAL SYLLOGISM (HS)
1. p → q
2. q → r
∴  p → r
```

**Rules using conjunction (∧):**

```
SIMPLIFICATION (Simp)      CONJUNCTION (Conj)
1. p ∧ q                   1. p
∴  p   (or q)              2. q
                            ∴  p ∧ q
```

**Rules using disjunction (∨):**

```
DISJUNCTIVE SYLLOGISM (DS)    ADDITION (Add)
1. p ∨ q                      1. p
2. ¬p                         ∴  p ∨ q
∴  q                          (q can be anything)
```

```
CONSTRUCTIVE DILEMMA (CD)
1. p ∨ q
2. p → r
3. q → s
∴  r ∨ s
```

### 10 Replacement Rules (Logical Equivalences)

These CAN be applied to components within a line (unlike inference rules).
Both directions are valid.

```
Double Negation (DN):        ¬¬p  ⟺  p
Commutation (Com):           p ∧ q  ⟺  q ∧ p
                             p ∨ q  ⟺  q ∨ p
Association (Assoc):         (p ∧ q) ∧ r  ⟺  p ∧ (q ∧ r)
                             (p ∨ q) ∨ r  ⟺  p ∨ (q ∨ r)
Distribution (Dist):        p ∧ (q ∨ r)  ⟺  (p ∧ q) ∨ (p ∧ r)
                             p ∨ (q ∧ r)  ⟺  (p ∨ q) ∧ (p ∨ r)
De Morgan's (DM):            ¬(p ∧ q)  ⟺  ¬p ∨ ¬q
                             ¬(p ∨ q)  ⟺  ¬p ∧ ¬q
Transposition (Trans):       p → q  ⟺  ¬q → ¬p
Material Implication (MI):   p → q  ⟺  ¬p ∨ q
Material Equivalence (ME):   p ↔ q  ⟺  (p → q) ∧ (q → p)
                             p ↔ q  ⟺  (p ∧ q) ∨ (¬p ∧ ¬q)
Exportation (Exp):           (p ∧ q) → r  ⟺  p → (q → r)
Tautology (Taut):            p  ⟺  p ∨ p
                             p  ⟺  p ∧ p
```

### Conditional Proof (CP)

To derive a conditional `p → q`:
1. Assume `p` (open a subproof).
2. Derive `q` within the subproof using any available rules.
3. Close the subproof and conclude `p → q`.
4. **Critical**: once the subproof is closed, its internal lines cannot be cited again.

### Indirect Proof / Reductio ad Absurdum (RAA)

To derive `p`:
1. Assume `¬p` (open a subproof).
2. Derive a contradiction (`q` and `¬q` for any `q`) within the subproof.
3. Close the subproof and conclude `p`.

### Proof Strategy

**Working forward:** Look at the premises. What rules can you apply right now?
Apply them and see what new lines you generate.

**Working backward (usually more effective):** Look at the conclusion.
- Conclusion is a conditional `p → q`? → Try conditional proof (assume p, derive q).
- Conclusion is a negation `¬p`? → Try indirect proof (assume p, derive contradiction).
- Conclusion is a conjunction `p ∧ q`? → Derive p and q separately, then use Conjunction.
- Conclusion is a disjunction `p ∨ q`? → Derive either p or q, then use Addition.
  Or look for Constructive Dilemma.
- Conclusion matches a consequent in a premise? → Try Modus Ponens.
- Conclusion matches the negation of an antecedent? → Try Modus Tollens.
- Conclusion links two conditionals? → Try Hypothetical Syllogism.

**When stuck:**
- Apply De Morgan's to negated conjunctions/disjunctions.
- Use Material Implication to convert conditionals to disjunctions (or vice versa).
- Try Transposition (contrapositive).
- Consider Conditional Proof or Indirect Proof for any goal.

### Proof Format

```
1. [Premise 1]                          Premise
2. [Premise 2]                          Premise
3. [Derived line]                       [Rule, line numbers]
4. | [Assumption for CP/RAA]            Assume (CP) or Assume (RAA)
5. | [Derived within subproof]          [Rule, line numbers]
6. | [Derived within subproof]          [Rule, line numbers]
7. [Conditional or conclusion]          CP 4-6 or RAA 4-6
```

Use indentation or Fitch bars to delimit subproofs. Every line must cite either
"Premise," "Assume," or a rule + the line numbers it applies to.


## Section 4: Categorical Logic

### The Four Categorical Forms

| Form | Name | Notation | Meaning |
|------|------|----------|---------|
| All S are P | Universal Affirmative (A) | SaP | Everything in S is in P |
| No S are P | Universal Negative (E) | SeP | Nothing is in both S and P |
| Some S are P | Particular Affirmative (I) | SiP | At least one thing is in both S and P |
| Some S are not P | Particular Negative (O) | SoP | At least one thing in S is not in P |

### Venn Diagram Method

**Two-circle Venn (for immediate inferences):**
- Shading a region = that region is EMPTY (nothing exists there).
- Placing an X in a region = at least one thing exists there.
- "All S are P": shade the part of S that does NOT overlap with P.
- "No S are P": shade the overlap (intersection) of S and P.
- "Some S are P": place X in the overlap of S and P.
- "Some S are not P": place X in the part of S that does NOT overlap with P.

**Three-circle Venn (for categorical syllogisms):**
1. Draw three overlapping circles for S (subject of conclusion), P (predicate
   of conclusion), and M (middle term — appears in both premises but not
   the conclusion).
2. Diagram the universal premise(s) FIRST (shading). Then diagram particular
   premise(s) (placing X). If an X could go in either of two regions, place it
   on the boundary.
3. Read off whether the conclusion is already represented in the diagram.
   If yes: **VALID**. If not: **INVALID**.

### Syllogistic Rules (alternative to Venn method)

A categorical syllogism is valid if and only if ALL of the following hold:
1. The middle term is distributed in at least one premise.
2. If a term is distributed in the conclusion, it must be distributed in its premise.
3. At least one premise is affirmative (not both negative).
4. If one premise is negative, the conclusion must be negative.
5. If both premises are universal, the conclusion cannot be particular
   (existential fallacy, under Boolean interpretation).

**Distribution rules:**
- A (All S are P): S is distributed, P is not.
- E (No S are P): both S and P are distributed.
- I (Some S are P): neither is distributed.
- O (Some S are not P): P is distributed, S is not.

### The Square of Opposition (Traditional)

```
        A (All S are P) ←――contraries――→ E (No S are P)
        |                                    |
   subalterns                           subalterns
        |                                    |
        I (Some S are P) ←subcontraries→ O (Some S are not P)

   A ←→ O : contradictories (exactly one is true)
   E ←→ I : contradictories (exactly one is true)
```

**Traditional interpretation** (assumes S is non-empty):
- Contraries: cannot both be true, can both be false.
- Subcontraries: cannot both be false, can both be true.
- Subalterns: truth flows down (A implies I, E implies O).
- Contradictories: exactly one true, one false.

**Boolean (modern) interpretation**: only the contradictory relations hold.
Universal statements do NOT imply their particular counterparts (no existential
import assumed).


## Section 5: First-Order Logic (Predicate Logic)

### Notation

- **Constants** (named individuals): a, b, c, ... (lowercase)
- **Variables**: x, y, z (lowercase)
- **Predicates**: F, G, H, ... (uppercase) — Fx means "x has property F"
- **Universal quantifier**: ∀x ("for all x")
- **Existential quantifier**: ∃x ("there exists an x such that")

### Translation Patterns

| English | FOL |
|---------|-----|
| All dogs bark | ∀x(Dx → Bx) |
| Some dogs bark | ∃x(Dx ∧ Bx) |
| No dogs bark | ¬∃x(Dx ∧ Bx)  or  ∀x(Dx → ¬Bx) |
| Some dogs don't bark | ∃x(Dx ∧ ¬Bx) |
| Fido barks | Bf |

**Critical pattern**: "All" uses → inside the quantifier; "Some" uses ∧.
This is the most common translation error.

### Quantifier Rules for Proofs

```
UNIVERSAL INSTANTIATION (UI)       EXISTENTIAL GENERALIZATION (EG)
∀x Φ(x)                           Φ(a)
―――――――                            ―――――――
Φ(a)     [a is any constant]       ∃x Φ(x)
```

```
EXISTENTIAL INSTANTIATION (EI)     UNIVERSAL DERIVATION (UD)
∃x Φ(x)                           [Assume arbitrary a]
―――――――                            ...derive Φ(a)...
Φ(c)     [c is a NEW constant      ―――――――
          not appearing earlier]    ∀x Φ(x)
```

**Order matters**: always do EI before UI when both are needed (to ensure
the constant introduced by EI is genuinely new).

**UD restriction**: the constant `a` used in the subproof must be arbitrary —
it cannot appear in any premise or undischarged assumption.


## Section 6: Quick Reference Tables

### Formal Fallacies (Invalid Argument Forms)

These LOOK like valid forms but are not:

```
AFFIRMING THE CONSEQUENT       DENYING THE ANTECEDENT
1. p → q                      1. p → q
2. q                           2. ¬p
∴  p   ✗ INVALID              ∴  ¬q  ✗ INVALID
```

Contrast with their valid counterparts:
- Affirming the consequent ≠ Modus Ponens (MP affirms the antecedent)
- Denying the antecedent ≠ Modus Tollens (MT denies the consequent)

### Key Logical Equivalences (for quick reference)

```
Contrapositive:   p → q  ≡  ¬q → ¬p          (ALWAYS valid)
Converse:         p → q  ≢  q → p             (NOT generally valid)
Inverse:          p → q  ≢  ¬p → ¬q           (NOT generally valid)
De Morgan's:      ¬(p ∧ q)  ≡  ¬p ∨ ¬q
                  ¬(p ∨ q)  ≡  ¬p ∧ ¬q
Conditional:      p → q  ≡  ¬p ∨ q
Biconditional:    p ↔ q  ≡  (p → q) ∧ (q → p)
```


## Output Format

**For truth tables:** Display the complete table with clear column headers.
Mark the validity-determining rows. State the verdict: VALID or INVALID.

**For proofs:** Number each line. Show the justification (rule + line numbers)
to the right. Use indentation for subproofs. End with the conclusion and
state what was proven.

**For categorical syllogisms:** Name the form, identify the terms (S, P, M),
describe the Venn diagram, and state VALID or INVALID.

**For symbolization:** Show the translation key (letter assignments), the
symbolic formula, and read it back in English to verify accuracy.

**Always show your work.** The point of formal logic is that every step is
explicit and checkable.
