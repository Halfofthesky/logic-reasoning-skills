# Logic & Reasoning Skills

Three Claude skills for logical analysis, built from open-access logic textbooks.

## Skills

### argument-analyst

Full six-phase logical analysis of argumentative text: argument detection and mapping, reconstruction in standard form (with implicit premises and the principle of charity), validity and soundness assessment, fallacy detection, explanation quality evaluation via the seven explanatory virtues, and an overall verdict with repair suggestions.

### fallacy-detector

Focused scan for 28 named fallacies across five families (Distraction, Weak Induction, Illicit Presumption, Linguistic Emphasis, Probabilistic/Statistical). Each entry includes detection heuristics, explanation of why the pattern fails, "NOT a fallacy when" guards to prevent over-flagging, and fix suggestions.

### formal-logic-solver

Formal logic problem-solver: English-to-symbolic translation, truth table construction and validity testing, natural deduction proofs (8 inference rules, 10 replacement rules, conditional proof, reductio ad absurdum), categorical syllogism evaluation (Venn diagrams and syllogistic rules), and first-order logic (predicate logic with quantifier rules).

## Installation

Copy any skill directory into your Claude skills folder:

```
~/.claude/skills/argument-analyst/
~/.claude/skills/fallacy-detector/
~/.claude/skills/formal-logic-solver/
```

Each skill is a self-contained `SKILL.md` file with no external dependencies.

## Sources and Attribution

These skills synthesize methods from four open-access textbooks. No prose is reproduced verbatim; the skills distill frameworks, taxonomies, and procedures into operational instructions.

- **Dowden, Bradley H.** *Logical Reasoning.* Sacramento: California State University Sacramento, 2023 (updated). Licensed CC BY-NC-SA.
  [https://open.umn.edu/opentextbooks/textbooks/logical-reasoning](https://open.umn.edu/opentextbooks/textbooks/logical-reasoning)

- **Van Cleave, Matthew J.** *Introduction to Logic and Critical Thinking.* Version 2.0, 2016. Licensed CC BY 4.0.
  [https://open.umn.edu/opentextbooks/textbooks/introduction-to-logic-and-critical-thinking](https://open.umn.edu/opentextbooks/textbooks/introduction-to-logic-and-critical-thinking)

- **Knachel, Matthew.** *Fundamental Methods of Logic.* Milwaukee: UWM Libraries, 2017. Licensed CC BY 4.0.
  [https://dc.uwm.edu/phil_facbooks/1](https://dc.uwm.edu/phil_facbooks/1)

- **DeLancey, Craig.** *A Concise Introduction to Logic.* Open SUNY Textbooks, 2017. Licensed CC BY-NC-SA 4.0.
  [https://open.umn.edu/opentextbooks/textbooks/a-concise-introduction-to-logic](https://open.umn.edu/opentextbooks/textbooks/a-concise-introduction-to-logic)

## License

This work is licensed under [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0)](https://creativecommons.org/licenses/by-nc-sa/4.0/).

This license is required by the ShareAlike clause of the Dowden and DeLancey source texts. You are free to share and adapt this material for non-commercial purposes, provided you give appropriate credit and distribute any derivative works under the same license.
