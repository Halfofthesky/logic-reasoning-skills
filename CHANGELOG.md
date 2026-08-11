# Changelog

All notable changes to the skills in this repository.

## [v2.0] — 2026-08-11

### argument-analyst — enthymeme resolution rewrite

Phase 2 previously supplied unstated premises in a single paragraph: add the most
plausible statement needed to make the argument valid, mark it `[IMPLICIT]`, subject to
two constraints — that it be needed for the argument to work, and that the arguer would
plausibly believe it.

**Why that was inadequate.** The first constraint is syntactic and does no filtering.
Infinitely many propositions restore validity, and the cheapest is always the bare
material conditional "if [premises] then [conclusion]." That completion satisfies the
constraint in every case and carries no content, so the constraint cannot discriminate
between readings. The entire load therefore fell on the second constraint, which was
stated as a plausibility gesture with no procedure behind it.

The deeper problem is that an enthymeme's missing premise is not concealed in the text.
Aristotle placed the enthymeme in the *Rhetoric* rather than the *Analytics* precisely
because the omitted premise is held by the audience as shared *endoxa* — the speaker
omits it because omitting it signals membership in a discourse community. Recovering it
therefore requires modelling the addressee, not parsing the sentence. The previous version
treated the passage as a closed object and had no step for this.

This release does not claim to automate that judgment. It makes the point at which
judgment was exercised explicit and auditable by a human reader.

**Added — five-step enthymeme procedure (Phase 2).**

1. *Detect the gap.* Six named signals: missing middle term, normative conclusion from
   descriptive premises, causal conclusion from correlational premises, evaluative
   conclusion from factual premises, modal jump, and unbridged general/particular shift.
2. *Identify the addressee.* Name in one line the discourse community for whom the
   argument would read as complete as written. This is what licenses a CONVENTIONAL tag.
3. *Generate candidates, not a completion.* Two to four propositions spanning
   weakest-sufficient, most-likely-held, and strongest-defensible. The bare material
   conditional is explicitly prohibited as a candidate. The spread between the weakest
   and the most-likely-held completion is reported as a finding in its own right.
4. *Tag provenance.* `[IMPLICIT-TEXTUAL]` (arguer commits to it elsewhere — cite where),
   `[IMPLICIT-CONVENTIONAL: <audience>]` (audience common ground — name the audience),
   `[IMPLICIT-ANALYST]` (analyst's construction; the arguer may reject it). No supplied
   premise may be left untagged.
5. *Charity ceiling.* Stop repairing when the supplied premise is more contestable than
   the conclusion, when the arguer visibly rejects it, or when an ANALYST-tagged premise
   is doing all the inferential work. Report the gap instead of a repaired argument.

**Added — cross-check.** Scan the remainder of the text for the same premise doing work
in other arguments. Recurrence upgrades ANALYST to TEXTUAL; conspicuous absence counts
as evidence against the candidate.

**Added — degraded mode.** For anonymous, fragmentary, translated, or decontextualized
text, the CONVENTIONAL tag is unavailable. Falling back on a generic "reasonable person"
is explicitly forbidden: it imports the analyst's own common ground under a neutral label,
which is the failure the tags exist to prevent.

**Changed — is-ought gap** demoted from a standalone rule to one detection signal in
Step 1, and routed through Steps 3–5 like any other missing premise.

**Changed — verdict scale (Phase 6)** extended from five grades to six. New grade
**Incomplete as stated** covers arguments that reached the charity ceiling: the reasoning
may be fine, but the text does not supply enough to judge it. This is distinct from
**Weak**, where something has actually been shown to be wrong. The verdict must now also
name which grade depends on which supplied premise; an argument whose validity rests on
an `[IMPLICIT-ANALYST]` premise may not be graded Sound/Cogent without stating that
dependence.

**Changed — skill description** now triggers on unstated-premise phrasing ("what is this
argument assuming," "what's the hidden premise," "resolve this enthymeme," "what does the
speaker take for granted").

**Changed — README** updated for the new Phase 2 and the six-grade scale.

### Known limitation

Degraded mode currently refuses rather than degrades. For anonymous online argument — a
common case — the audience is real but unidentified, so every tag collapses to ANALYST
and the provenance scheme stops doing work exactly where it is most needed. Two candidate
fixes, neither yet adopted: infer the addressee from stylistic and lexical markers and tag
CONVENTIONAL with a confidence note; or treat "audience unrecoverable" as a reportable
property of the text rather than a defect in the analysis. Both need testing against real
cases first.

## [v1.0] — initial release

Three skills: `argument-analyst`, `fallacy-detector`, `formal-logic-solver`. Synthesized
from four open-access logic textbooks (Dowden, Van Cleave, Knachel, DeLancey). See README
for per-source attribution.
