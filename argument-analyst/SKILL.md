---
name: argument-analyst
description: >
  Systematically analyze arguments in text: reconstruct them in standard form, identify premises
  (explicit and implicit), evaluate validity and soundness, detect fallacies, assess inductive strength,
  and grade explanation quality. Use this skill whenever the user asks to "analyze this argument,"
  "check my reasoning," "find the fallacies," "evaluate this claim," "is this a good argument,"
  "what's wrong with this logic," "stress-test this reasoning," "steelman/steelman this," or
  presents any text (essay, article, debate transcript, op-ed, social media post, academic paper,
  policy proposal) and asks for logical evaluation. Also trigger when the user submits a passage
  and asks "is this valid," "is this sound," "does this follow," "what are the assumptions here,"
  or "what's the weakest point." Trigger proactively when reviewing any argumentative text,
  even if the user says only "review this" or "what do you think of this" and the text contains
  claims supported by reasons.
---

# Argument Analyst

Analyze argumentative text using a systematic, multi-phase procedure grounded in three
complementary frameworks from formal and informal logic. The goal is to produce analysis
that is both rigorous and useful: not a pedantic logic exercise, but a practical assessment
of whether the reasoning actually works and where it breaks down.

## Source Frameworks

This skill synthesizes methods from three open-access logic textbooks:

- **Dowden, Bradley H.** *Logical Reasoning* (2023 ed.) -- richest treatment of informal
  reasoning, fallacy detection in real-world contexts, and practical decision-making. Provides
  the 23 Principles of Logical Reasoning and the four-question authority checklist.
- **Van Cleave, Matthew J.** *Introduction to Logic and Critical Thinking* v2.0 -- strongest
  framework for argument reconstruction (standard form, the informal test of validity,
  the principle of charity, supplying missing premises) and the seven explanatory virtues
  for inference-to-best-explanation arguments.
- **Knachel, Matthew.** *Fundamental Methods of Logic* (2017) -- best-organized fallacy
  taxonomy (four families, 20 named fallacies) and clearest treatment of the formal/informal
  fallacy boundary, plus manipulative framing and implicature.

Do not cite these books in output unless the user asks for sources. The frameworks are
internalized, not attributed.


## Analysis Procedure

Work through these phases in order. Each phase builds on the previous one. If the text is
short (a single argument), some phases collapse. If long (an essay, article), apply per-argument
where possible and then synthesize.

### Phase 1: Argument Detection and Mapping

**Is there an argument present?** Ask: does the text contain a statement someone is trying
to establish as true (or explain why it is true) by basing it on some other statement? If the
answer is yes, an argument is present. If no reasons are given for any claim, the text is
assertion, description, explanation, or rhetoric -- not argument. Say so and stop (or note
which parts are argumentative and which are not).

**Distinguish arguments from explanations.** Arguments try to convince you *that* something
is true. Explanations assume the conclusion is already accepted and show *why* it is true.
The same passage can contain both. Flag which is which -- the evaluation criteria differ.

**Identify all arguments in the text.** For each:
1. Locate the conclusion (the claim being supported).
2. Locate the premises (the reasons given).
3. Use indicator words as aids but not as proof:
   - Premise indicators: because, since, for, as, given that, seeing that, for the reason that
   - Conclusion indicators: therefore, so, hence, thus, consequently, it follows that, we may conclude
   - Discount indicators: even though, while it may be true that, although, despite
4. Identify argument structure: simple (premises -> conclusion), chain (subarguments feeding
   intermediate conclusions), or convergent (independent premises supporting one conclusion).
5. Note which arguments are main arguments and which are subarguments.

### Phase 2: Reconstruction in Standard Form

For each argument identified, reconstruct it in numbered standard form:

```
1. [Premise 1]
2. [Premise 2]
...
N. Therefore, [Conclusion] (from 1, 2, ...)
```

**Recognize rhetorical moves that are not premises:**
- *Assuring*: "experts agree that...", "studies have shown..." -- signals that further reasons
  exist but aren't being given now. Not a premise; evaluate the implied authority separately.
- *Guarding*: "probably," "it is likely that," "tends to" -- weakens a claim to make it harder
  to refute. Note the degree of hedging; it affects what the arguer is actually committed to.
- *Discounting*: "even though X, still Y" -- acknowledges a potential objection and dismisses
  it. The discounted material (X) is NOT a premise for the conclusion; it's a concession.

**Rules for reconstruction:**
- Remove extraneous sentences, discount phrases, indicator words.
- Replace pronouns with their antecedents.
- Paraphrase for clarity where needed, but preserve the arguer's intent.
- For chain arguments, mark intermediate conclusions: "Therefore, [X] (from 1-2)" then
  use X as a premise in the next step.
- Note which premises support which conclusions (from 1-2, from 3, independently).

**Supply missing premises** using the principle of charity: add the most plausible statement
needed to make the argument valid (for deductive arguments) or inductively strong (for
inductive arguments). Mark supplied premises explicitly as [IMPLICIT]. Two constraints:
(a) the implicit premise must be needed for the argument to work, and (b) it must be
something the arguer would plausibly believe.

**Watch for the is-ought gap.** If the conclusion is normative (contains "should," "ought,"
"good," "bad," "right," "wrong") but all explicit premises are descriptive, there is a
missing normative premise. Make it explicit.

### Phase 3: Validity and Soundness Assessment

**For deductive arguments:**

Apply the informal test of validity: can you imagine a scenario in which all the premises
are true and yet the conclusion is false? If yes, the argument is invalid -- describe the
counterexample. If you cannot imagine such a scenario, the argument is valid.

Then assess soundness: is the argument valid AND are all premises actually true? If any
premise is false or doubtful, the argument is unsound even if valid. Note which premises
are contested or require evidence not provided.

**For inductive arguments:**

Assess inductive strength: do the premises make the conclusion probable? An inductively
strong argument is one where, given the truth of the premises, the conclusion is likely
(but not guaranteed). Note that inductive arguments are defeasible -- additional information
could overturn them.

Types of inductive arguments to recognize:
- **Statistical generalization**: from sample to population. Check: sample size, representativeness, margin of error.
- **Inference to the best explanation (IBE)**: the conclusion is the hypothesis that best explains observed facts.
  Evaluate using the seven explanatory virtues (see Phase 5).
- **Analogical argument**: X and Y share properties A, B, C; X also has property D; therefore Y probably has D.
  Check: relevance of shared properties, number of shared properties, presence of relevant disanalogies.
- **Causal argument**: X caused Y. Check: correlation vs. causation, alternative explanations, temporal order,
  mechanism, confounding variables.

### Phase 4: Fallacy Detection

Scan the argument for fallacies. Organized into four families:

#### Family 1: Fallacies of Distraction (Relevance)

The reasons given are irrelevant to the conclusion. The arguer sidesteps the real issue.

- **Appeal to Emotion (ad Populum)**: playing on fear, pity, patriotism, desire to fit in
  (bandwagon), or any other emotion instead of providing relevant evidence. Includes appeals
  to pity in courtroom-style contexts, fear-mongering, and "everybody's doing it."
- **Appeal to Force (ad Baculum)**: threatening consequences for disagreement rather than
  giving reasons. Includes subtle forms: physically intimidating debate style, implicit
  professional threats.
- **Straw Man**: misrepresenting an opponent's position -- exaggerating, distorting, or
  fabricating a weaker version -- then attacking the distortion. The rebuttal is irrelevant
  because it addresses a position no one holds.
- **Red Herring**: changing the subject to a related but irrelevant issue, then making strong
  points on the new topic and pretending to have addressed the original. Includes evasive
  non-answers to direct questions.
- **Ad Hominem**: attacking the person making the argument rather than the argument itself.
  Two forms: (a) *Abusive* -- name-calling, character attacks, unflattering language.
  (b) *Circumstantial* -- arguing that the person's circumstances (interests, associations)
  invalidate their argument.
  **Important exception**: attacking credibility IS legitimate when evaluating testimony
  (witness on a stand), because testimony is a claim, not an argument. When evaluating
  an argument, the arguer's character is irrelevant -- the argument stands on its own.
- **Tu Quoque**: deflecting criticism by pointing out the critic does the same thing, instead
  of answering the criticism. Exception: if the criticism applies equally to ALL positions
  (including the critic's), pointing this out is legitimate, not fallacious.

#### Family 2: Fallacies of Weak Induction

The premises provide some evidence but far too little to support the conclusion.

- **Argument from Ignorance (ad Ignorantiam)**: concluding X is true because it hasn't
  been proven false (or vice versa). Forms: "You can't prove me wrong, so I'm right";
  setting an unreasonably high standard of proof then concluding failure to meet it means
  the opposite; "I can't imagine how X could be true, therefore X is false."
  **Note**: absence of evidence CAN sometimes be evidence of absence, when searches
  have been thorough and would be expected to find evidence if it existed. Assess the
  thoroughness of the search.
- **Appeal to Inappropriate Authority**: citing someone who lacks relevant expertise on the
  topic at hand. Apply Dowden's four-question checklist: (1) Is the authority an expert on
  *this* subject? (2) Do authorities in the field agree (barring occasional outliers)? (3) Is
  the citation accurate -- is the authority being quoted correctly? (4) Can the authority be
  trusted to tell the truth on this topic (no disqualifying bias)?
  Only accept the appeal if all four answers are yes.
- **Post Hoc Ergo Propter Hoc**: inferring causation from mere temporal sequence. X happened
  before Y, therefore X caused Y. Temporal precedence is necessary but not sufficient for
  causation.
- **Slippery Slope**: claiming an action will trigger an unstoppable causal chain to disaster,
  without sufficient justification that the chain is inevitable. Key insight: even if each link
  in the chain is individually probable, the conjunction of all links may be improbable.
  If each of 8 links has .9 probability, the chain probability is only .43. Distinguish from
  valid hypothetical syllogism (where each link is certain, not merely probable).
- **Hasty Generalization**: inferring a general conclusion from too few particular instances.
  Includes reliance on anecdotal evidence and formation of stereotypes from limited
  experience.

#### Family 3: Fallacies of Illicit Presumption

A hidden premise is assumed that is controversial, unsupported, or false.

- **Accident**: applying a general rule to an exceptional case without acknowledging that
  exceptions exist. The reverse of hasty generalization: instead of going from too few
  particulars to a generalization, here we go from a generalization to a particular case
  where the generalization doesn't apply.
- **Begging the Question (Petitio Principii)**: the conclusion is assumed (explicitly or
  implicitly) in one of the premises. The argument is circular. Note: formally, question-begging
  arguments ARE valid (if the premise is true, the conclusion must be true, because they're
  the same claim). The problem is not formal but pragmatic: the argument provides no
  independent reason to accept the conclusion.
- **False Dichotomy (False Dilemma)**: presenting only two options when more exist, then
  eliminating one to force the other. Often appears as a disjunctive syllogism with a false
  first premise. The fix is to "escape between the horns" by identifying overlooked alternatives.
- **Complex Question**: asking a question that presupposes something controversial. "Have
  you stopped cheating?" presupposes that you were cheating.
- **Suppressed Evidence**: selectively presenting only evidence that supports one's conclusion
  while omitting evidence that undermines it.
- **Composition**: inferring that the whole has a property because all its parts have that
  property. Sometimes valid (every part is plastic -> the whole is plastic) but often not
  (every player is mediocre -> the team is mediocre). Identifying the fallacy requires
  understanding which properties transfer from parts to wholes and which do not.
- **Division**: the reverse -- inferring that a part has a property because the whole has it.
  Same content-dependence as composition.

#### Family 4: Fallacies of Linguistic Emphasis

Exploiting ambiguity, framing, or selective emphasis in language.

- **Equivocation**: using the same word in two different senses within an argument. Includes
  exploitation of homonymy (unrelated meanings: bank/bank), polysemy (related meanings:
  law-as-statute vs. law-of-nature), and false implicature (saying something literally true
  that communicates a false implication).
- **Accent**: emphasizing favorable content and de-emphasizing unfavorable content through
  typographic manipulation, fine print, fast-talking disclaimers, or selective stress.
- **Quoting Out of Context**: selectively quoting so that the meaning changes from the
  original. The quoted words are accurate but the context that gives them their real meaning
  is omitted.
- **Manipulative Framing**: choosing loaded or slanted language to bias the audience's
  perception. "Estate tax" vs. "death tax"; "enhanced interrogation" vs. "torture." The framing
  carries an implicit argument that bypasses rational evaluation.

#### Probabilistic and Statistical Fallacies

These are formal rather than informal -- identifiable from structure alone:

- **Conjunction Fallacy**: judging a conjunction of events as more probable than either
  event alone. P(A and B) cannot exceed P(A) or P(B).
- **Base Rate Fallacy**: ignoring prior probabilities when evaluating conditional evidence.
- **Small Numbers Fallacy**: drawing conclusions from samples too small to be reliable.
- **Regression to the Mean Fallacy**: attributing a causal explanation to what is merely
  statistical regression toward the average.
- **Gambler's Fallacy**: believing that past random outcomes affect future probabilities
  in independent events.

### Phase 5: Explanation Quality (for IBE arguments)

When the argument is an inference to the best explanation, evaluate using the seven
explanatory virtues:

1. **Explanatoriness**: Does the hypothesis explain ALL the observed facts?
2. **Depth**: Does it raise more questions than it answers?
3. **Power**: Does it apply in a range of similar contexts, not just this one case?
4. **Falsifiability**: Is it possible for evidence to show the explanation is wrong?
   Unfalsifiable hypotheses are defective.
5. **Modesty**: Does it claim more than needed to explain the facts? Unnecessary
   specificity is a flaw.
6. **Simplicity (Ockham's Razor)**: Does it posit fewer entities or processes than
   alternatives? Prefer the simpler explanation, all else being equal.
7. **Conservativeness**: Does it require abandoning fewer well-established beliefs
   than alternatives?

Compare the proposed explanation against competing explanations on all seven virtues.
The explanation that scores best overall is the best explanation.

### Phase 6: Overall Assessment and Verdict

Synthesize findings into a final assessment:

1. **Argument map**: how many arguments were found, their structure (main vs. sub),
   and logical relationships.
2. **Strongest elements**: which premises are well-supported, which inferences are valid
   or inductively strong.
3. **Weakest elements**: which premises are false or unsupported, which inferences fail,
   which fallacies are present.
4. **Missing pieces**: what evidence or premises would be needed to make the argument
   work. What questions remain unanswered.
5. **Verdict**: an overall assessment of argument quality on a scale:
   - **Sound/Cogent**: Valid/strong with true premises. The argument works.
   - **Formally valid but unsound**: The logic works but at least one premise is false or
     doubtful.
   - **Inductively strong but defeasible**: Probably correct given current evidence, but
     vulnerable to new information.
   - **Weak**: Significant logical flaws, unsupported premises, or fallacies that undermine
     the conclusion.
   - **Fallacious**: One or more clear fallacies render the argument unreliable.
6. **Repair suggestions**: how the argument could be fixed -- what premises need evidence,
   what structural changes would make it valid, what fallacies need to be excised.


## Output Format

Adapt output length and detail to the complexity of the input:

**For a short passage (1-3 sentences):** A concise analysis -- reconstruction in standard form,
validity check, any fallacies, and verdict. A few paragraphs.

**For a medium passage (a paragraph or two):** Full six-phase analysis, but keep each phase
to a paragraph or two. Use the phase headings.

**For a long text (article, essay, chapter):** Full analysis with argument map. May need to
select the most important 3-5 arguments for deep analysis rather than analyzing every claim.
Note which arguments were not analyzed in depth.

**General principles:**
- Lead with the 