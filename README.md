# Logic & Reasoning Skills

Three skills for Claude that bring formal and informal logic into your workflow. Built by synthesizing four open-access logic textbooks into operational instructions Claude can follow.

Each skill is a self-contained `SKILL.md` file — no scripts, no dependencies, no external references. Claude reads the file and gains the relevant analytical capability.

## The three skills

### argument-analyst

Systematic six-phase analysis of any argumentative text.

**What it does:**

1. **Argument detection** — identifies which parts of a text are arguments (reasons given for a conclusion) vs. explanations, descriptions, or bare assertions.
2. **Reconstruction in standard form** — extracts premises and conclusions, numbers them, marks their logical relationships, and resolves enthymemes (arguments with an unstated premise) through a five-step procedure: detect the gap, identify the addressee, generate competing candidate premises rather than one, tag each supplied premise by provenance (`TEXTUAL` / `CONVENTIONAL` / `ANALYST`), and stop at the charity ceiling rather than repairing an argument into one the arguer never made. The is-ought gap is handled as one case of this procedure.
3. **Validity and soundness assessment** — applies the informal test of validity (can you imagine a scenario where the premises are true and the conclusion false?) for deductive arguments; assesses inductive strength for statistical generalizations, analogies, causal claims, and inferences to the best explanation.
4. **Fallacy detection** — scans for 24+ named fallacies organized in four families.
5. **Explanation quality** — evaluates inference-to-best-explanation arguments against seven explanatory virtues (explanatoriness, depth, power, falsifiability, modesty, simplicity, conservativeness).
6. **Verdict** — overall assessment on a six-point scale from Sound/Cogent to Fallacious, plus *Incomplete as stated* for arguments that cannot be judged without a premise the text never supplies. Includes repair suggestions and a rule requiring the verdict to name which grade depends on which supplied premise.

**Example prompts:**

- "Analyze the argument in this op-ed."
- "Put this argument in standard form and tell me if it's valid."
- "What are the hidden assumptions in this policy proposal?"
- "This is an enthymeme — what premise is the speaker expecting me to supply?"
- "Steelman this, then find its weakest point."
- "Is this a good argument? Be specific about what works and what doesn't."

**Best for:** thorough evaluation of essays, articles, debate transcripts, academic papers, policy proposals — anything where you want the full picture, not just a quick flag.

---

### fallacy-detector

Fast-scan for logical fallacies with structured findings.

**What it does:**

Scans text for 28 named fallacies across five families and reports each finding in a consistent format: fallacy name, the offending passage, why it fails, and what a non-fallacious version would look like.

**Fallacy families:**

- **Distraction (Relevance):** Appeal to Emotion, Appeal to Force, Straw Man, Red Herring, Ad Hominem (abusive and circumstantial), Tu Quoque
- **Weak Induction:** Argument from Ignorance, Appeal to Inappropriate Authority (with a four-question checklist), Post Hoc, False Cause, Slippery Slope, Hasty Generalization
- **Illicit Presumption:** Begging the Question, False Dichotomy, Complex Question, Suppressed Evidence, Accident, Composition, Division
- **Linguistic Emphasis:** Equivocation, Accent/Selective Emphasis, Quoting Out of Context, Manipulative Framing
- **Probabilistic/Statistical:** Conjunction Fallacy, Base Rate Fallacy, Small Numbers, Regression to the Mean, Gambler's Fallacy

Each fallacy entry includes "NOT a fallacy when..." guidance to prevent over-flagging. The skill also distinguishes between fallacies (patterns of reasoning that fail) and mere factual errors or bad style.

**Example prompts:**

- "Find the fallacies in this." (paste any text)
- "What rhetorical tricks are being used in this ad?"
- "Is this politician's argument fallacious? Name the specific fallacies."
- "Red-flag this email for me — what reasoning errors does it contain?"
- "Is there anything wrong with this reasoning, or is it actually fine?"

**Best for:** quick "what's wrong here" scans of op-eds, social media posts, political speeches, ad copy, comment threads, emails, proposals. Lighter and faster than argument-analyst — it skips reconstruction and goes straight to pattern-matching.

---

### formal-logic-solver

Solve formal logic problems step by step.

**What it does:**

- **Symbolization** — translates English sentences into propositional or predicate logic notation, with a guide for tricky constructions ("unless," "only if," "if and only if").
- **Truth tables** — builds complete truth tables and applies the validity test (is there any row where all premises are true and the conclusion is false?). Includes the indirect (short-cut) method for complex arguments.
- **Natural deduction proofs** — constructs proofs using 8 basic inference rules (Modus Ponens, Modus Tollens, Hypothetical Syllogism, Disjunctive Syllogism, Constructive Dilemma, Simplification, Conjunction, Addition) plus 10 replacement rules (De Morgan's, Transposition, Material Implication, Distribution, etc.) and two proof strategies (Conditional Proof and Reductio ad Absurdum). Includes a strategy guide for working forward vs. backward.
- **Categorical syllogisms** — evaluates syllogisms using Venn diagrams (two-circle and three-circle) and the five syllogistic rules with distribution checks. Includes the Square of Opposition (traditional and Boolean interpretations).
- **First-order logic** — translates quantified English into predicate logic (with the critical "All uses →, Some uses ∧" pattern) and applies four quantifier rules (Universal Instantiation, Existential Generalization, Existential Instantiation, Universal Derivation).

**Example prompts:**

- "Prove this argument is valid: if P then Q, if Q then R, P, therefore R."
- "Build a truth table for (P → Q) ∧ (Q → R) → (P → R)."
- "Is this syllogism valid? All mammals are warm-blooded. All whales are mammals. Therefore all whales are warm-blooded."
- "Translate into predicate logic: Every student who studies hard passes the exam."
- "What inference rule justifies going from 'P → Q' and '¬Q' to '¬P'?"
- "Show me why affirming the consequent is invalid."

**Best for:** logic homework, exam prep, checking formal validity of arguments, learning inference rules, working through proofs.

---

## Which skill to use

| You want to... | Use |
|---|---|
| Thoroughly evaluate an essay, article, or speech | `argument-analyst` |
| Quickly find what's wrong with a piece of reasoning | `fallacy-detector` |
| Check formal validity with a truth table or proof | `formal-logic-solver` |
| Reconstruct an argument in standard form | `argument-analyst` |
| Know if a specific fallacy is present | `fallacy-detector` |
| Translate English into logical notation | `formal-logic-solver` |
| Evaluate a categorical syllogism | `formal-logic-solver` |
| Grade the quality of an explanation | `argument-analyst` |
| Identify manipulative framing or rhetorical tricks | `fallacy-detector` |

The skills are complementary. For a deep analysis, you might use `argument-analyst` for the overall evaluation and then `formal-logic-solver` to check a specific inference formally.

## Installation

### Method 1: Copy into Claude Code skills directory

Clone or download the repo and copy the skill directories into your Claude Code user skills folder:

```bash
git clone https://github.com/Halfofthesky/logic-reasoning-skills.git
cp -r logic-reasoning-skills/argument-analyst ~/.claude/skills/
cp -r logic-reasoning-skills/fallacy-detector ~/.claude/skills/
cp -r logic-reasoning-skills/formal-logic-solver ~/.claude/skills/
```

Or to install into a specific project rather than globally:

```bash
cp -r logic-reasoning-skills/argument-analyst .claude/skills/
cp -r logic-reasoning-skills/fallacy-detector .claude/skills/
cp -r logic-reasoning-skills/formal-logic-solver .claude/skills/
```

### Method 2: Download individual skills

Each skill is a single file (`SKILL.md`) inside its own directory. You can download just the ones you want:

```
argument-analyst/SKILL.md
fallacy-detector/SKILL.md
formal-logic-solver/SKILL.md
```

Place each in a directory of the same name under your skills folder.

### Method 3: Use in Cowork (Claude desktop app)

In a Cowork session, connect a folder that contains the skill directories. Claude will detect and use them automatically when relevant prompts are given. You can also package each skill as a `.skill` file (a zip archive containing the directory with `SKILL.md`) for one-click installation via Cowork's "Save skill" button.

### Requirements

- Claude Code, Claude desktop app (Cowork mode), or any Claude-based tool that supports the skills protocol.
- No external dependencies — each skill is pure Markdown instructions.
- No scripts, no API keys, no runtime requirements.

## Sources and Attribution

These skills synthesize methods from four open-access logic textbooks. No prose is reproduced verbatim; the skills distill frameworks, taxonomies, and analytical procedures into operational instructions.

**Primary sources:**

- **Dowden, Bradley H.** *Logical Reasoning.* Sacramento: California State University Sacramento, 2023 (updated). Licensed [CC BY-NC-SA](https://creativecommons.org/licenses/by-nc-sa/4.0/).
  [https://open.umn.edu/opentextbooks/textbooks/logical-reasoning](https://open.umn.edu/opentextbooks/textbooks/logical-reasoning)
  Contributions: 23 Principles of Logical Reasoning, four-question authority checklist, counterexample method for validity testing, practical decision-making framework, criteria for good explanations.

- **Van Cleave, Matthew J.** *Introduction to Logic and Critical Thinking.* Version 2.0, 2016. Licensed [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).
  [https://open.umn.edu/opentextbooks/textbooks/introduction-to-logic-and-critical-thinking](https://open.umn.edu/opentextbooks/textbooks/introduction-to-logic-and-critical-thinking)
  Contributions: principle of charity, informal test of validity, standard form reconstruction method, seven explanatory virtues, assuring/guarding/discounting framework, 8 valid inference forms for proofs, categorical logic with Venn diagrams.

- **Knachel, Matthew.** *Fundamental Methods of Logic.* Milwaukee: UWM Libraries, 2017. Licensed [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).
  [https://dc.uwm.edu/phil_facbooks/1](https://dc.uwm.edu/phil_facbooks/1)
  Contributions: four-family fallacy taxonomy (20 named fallacies), manipulative framing as a fallacy category, implicature and equivocation treatment, Aristotelian and sentential logic methods.

- **DeLancey, Craig.** *A Concise Introduction to Logic.* Open SUNY Textbooks, 2017. Licensed [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/).
  [https://open.umn.edu/opentextbooks/textbooks/a-concise-introduction-to-logic](https://open.umn.edu/opentextbooks/textbooks/a-concise-introduction-to-logic)
  Contributions: propositional and first-order logic proof systems, conditional derivation and reductio ad absurdum methods, quantifier rules (universal instantiation, existential generalization, existential instantiation, universal derivation).

## License

This work is licensed under [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0)](https://creativecommons.org/licenses/by-nc-sa/4.0/).

This license is required by the ShareAlike clause of the Dowden and DeLancey source texts. You are free to share and adapt this material for non-commercial purposes, provided you give appropriate credit and distribute any derivative works under the same license.
