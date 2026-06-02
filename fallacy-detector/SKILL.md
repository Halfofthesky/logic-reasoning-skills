---
name: fallacy-detector
description: >
  Scan text for logical fallacies and reasoning errors. Use this skill whenever the user asks
  to "find the fallacies," "what's wrong with this reasoning," "check this for logical errors,"
  "spot the bad arguments," "is this fallacious," "debunk this," "red-flag this," or submits
  any argumentative text (op-ed, tweet, political speech, ad copy, debate transcript, comment
  thread, article, email, proposal) and wants to know what reasoning errors it contains.
  Also trigger when the user asks "why is this argument bad," "what tricks are being used here,"
  "is this manipulative," or "what rhetorical tricks are in this." This skill is faster and more
  focused than the argument-analyst skill: it skips full argument reconstruction and goes straight
  to identifying fallacious patterns, naming them, explaining why they fail, and showing what
  a corrected version would look like. Use argument-analyst for full logical evaluation;
  use fallacy-detector for quick "what's wrong here" scans.
---

# Fallacy Detector

Scan argumentative text for logical fallacies and reasoning errors. For each fallacy found,
report: (1) the fallacy name, (2) the specific passage that commits it, (3) why it's
fallacious, and (4) what a non-fallacious version of the point would look like.

This skill synthesizes fallacy taxonomies from Dowden (*Logical Reasoning*), Van Cleave
(*Introduction to Logic and Critical Thinking*), and Knachel (*Fundamental Methods of Logic*).

## How to Use This Skill

1. Read the submitted text.
2. Scan for fallacy signatures using the detection guide below.
3. For each fallacy found, output a finding in the format specified.
4. After all findings, give a brief overall assessment.
5. If no fallacies are found, say so — not every text is fallacious.

**Critical rule: avoid over-flagging.** A fallacy diagnosis requires that the reasoning
*actually fails* in the way described. Many patterns that superficially resemble fallacies
are legitimate. Each entry below includes "NOT a fallacy when..." guidance. Read it
before flagging.


## Output Format

For each fallacy found:

> **[Fallacy Name]**
> *Passage:* "[quote or close paraphrase of the offending passage]"
> *Problem:* [1-3 sentences: why this reasoning fails]
> *Fix:* [What the arguer would need to say/show instead]

After all findings, a brief **Overall Assessment**: how many fallacies, how severely they
damage the argument, and whether the core point could survive if the fallacies were fixed.


## Fallacy Detection Guide

### I. Distraction Fallacies (Relevance)

Common signature: the "reason" given has nothing to do with the conclusion. The arguer
sidesteps the real issue.

---

**APPEAL TO EMOTION (ad Populum)**

*Detection signs:* Emotional language disproportionate to the evidence offered. Fear-mongering
("imagine if..."), pity plays (graphic suffering descriptions when the question is about policy
or fact), patriotic/nationalistic appeals substituting for evidence, bandwagon pressure
("everyone agrees," "#1 in the ratings," "millions of people can't be wrong").

*Why it fails:* Emotional responses are not evidence. Feeling strongly that X is true
provides no reason to believe X is true.

*NOT a fallacy when:* Emotions are genuinely relevant to the conclusion (e.g., arguing that
a policy causes suffering, where the suffering IS the point). Also not a fallacy when emotion
accompanies a substantive argument rather than replacing it.

---

**APPEAL TO FORCE (ad Baculum)**

*Detection signs:* Explicit threats ("agree or face consequences"), implicit professional
threats ("those who don't support X will be remembered"), intimidating debate style used
as a substitute for argument. Subtle form: physically imposing behavior, shouting down
opponents, combative body language that flusters the interlocutor.

*Why it fails:* Threats give you a reason to SAY you believe X, not a reason to actually
believe X.

*NOT a fallacy when:* The "threat" is actually a factual prediction relevant to the argument
("if we don't evacuate, people will die" is evidence, not a threat).

---

**STRAW MAN**

*Detection signs:* The rebuttal attacks a position more extreme, absolute, or absurd than
what was actually stated. Look for: exaggeration ("so you're saying we should just..."),
insertion of words the opponent never used, fabricated implications ("that's basically
saying..."), attacking the most extreme version of a position rather than the stated one.

*Why it fails:* Defeating a position no one holds proves nothing about the real position.

*NOT a fallacy when:* The characterization is accurate, or when making explicit what is
logically implied by the opponent's stated position (even if they didn't say it outright).

---

**RED HERRING**

*Detection signs:* The response starts on-topic but gradually drifts to a different subject.
The arguer scores points on the new topic and acts as if the original question has been
addressed. Especially common: evasive non-answers to direct questions (the question is
about X, the response is about Y). Watch for "the real issue is..." followed by a topic change.

*Why it fails:* Strong points about topic Y are irrelevant to the question about topic X.

*NOT a fallacy when:* The arguer explicitly argues that a different question must be settled
first and explains why, or when the "tangent" is actually relevant context.

---

**AD HOMINEM**

*Detection signs:* The response targets the person rather than their argument: name-calling,
character attacks, bringing up the arguer's past, questioning their motives or associations.

Two forms:
- *Abusive:* Direct attacks on character, intelligence, appearance, labels.
- *Circumstantial:* "Of course you'd say that, you're a [group member / have a financial
  interest / stand to benefit]."

*Why it fails:* An argument's quality is independent of who makes it. A hypocrite can give
a valid argument; a saint can give a terrible one.

*NOT a fallacy when:* (a) Evaluating testimony rather than argument — a witness's
credibility IS relevant to whether their claims are true. (b) The person's expertise or
conflict of interest is directly relevant to an appeal-to-authority claim they're making.
(c) Pointing out that someone's behavior contradicts their stated principles, when that
contradiction is itself the topic of discussion.

---

**TU QUOQUE ("You Too")**

*Detection signs:* Responding to criticism by pointing out the critic does the same thing,
without addressing the substance of the criticism. "How can you criticize X when you
do X yourself?"

*Why it fails:* The critic's hypocrisy doesn't make the criticism wrong.

*NOT a fallacy when:* The point is that the criticism applies equally to everyone (including
the critic), making it a non-discriminating objection rather than a targeted one. In that
case, "you too" is a legitimate rebuttal showing the criticism proves too much.

---

### II. Weak Induction Fallacies

Common signature: some evidence is offered, but it is far too weak to support the conclusion.

---

**ARGUMENT FROM IGNORANCE (ad Ignorantiam)**

*Detection signs:* Four patterns to watch for:
1. "No one has proven X false, therefore X is true" (or vice versa).
2. Setting an unreasonably high standard of proof, then concluding failure to meet it
   proves the opposite.
3. "I can't understand/imagine how X could be true, therefore X is false."
4. "No evidence has been found for X, therefore X is false."

*Why it fails:* Lack of proof is not proof of lack — unless the search has been thorough
enough that evidence would have been found if it existed.

*NOT a fallacy when:* Extensive, well-designed searches have failed to find evidence.
Absence of evidence after thorough investigation CAN be evidence of absence. Assess
the thoroughness of the search.

---

**APPEAL TO INAPPROPRIATE AUTHORITY**

*Detection signs:* A claim is supported by citing someone famous, credentialed, or
impressive — but whose expertise is not in the relevant field. Celebrity endorsements,
citing a PhD in an unrelated discipline, "doctors say..." about a non-medical question.

*Four-question checklist (all must be yes for the appeal to be legitimate):*
1. Is the authority an expert on THIS subject specifically?
2. Do authorities in the field broadly agree (not just one outlier)?
3. Is the authority being quoted accurately and in context?
4. Can the authority be trusted on this topic (no disqualifying conflict of interest)?

*Why it fails:* Expertise in one domain does not transfer to another.

*NOT a fallacy when:* The authority is genuinely expert in the relevant field, their
view represents professional consensus, and they have no disqualifying bias.

---

**POST HOC ERGO PROPTER HOC**

*Detection signs:* "After X happened, Y happened, therefore X caused Y." Temporal
sequence presented as the sole or primary evidence of causation. Especially common
in evaluating leaders/presidents ("crime fell under President Z, therefore Z's policies
reduced crime") and in personal anecdotes ("I took supplement X and felt better").

*Why it fails:* Temporal precedence is necessary but nowhere near sufficient for
causation. The world is full of coincidences and confounding variables.

*NOT a fallacy when:* Temporal sequence is accompanied by mechanism, controlled
comparison, or exclusion of alternative causes.

---

**FALSE CAUSE (general)**

*Detection signs:* Any causal claim based on insufficient evidence. Includes post hoc
as a subspecies, but also: confusing correlation with causation, reversing cause and effect,
ignoring common causes, and oversimplifying multi-causal phenomena.

*NOT a fallacy when:* The causal claim is supported by controlled studies, plausible
mechanism, dose-response relationship, or exclusion of confounders.

---

**SLIPPERY SLOPE**

*Detection signs:* "If we allow X, then Y will happen, then Z, then disaster." A chain
of if-then claims leading from a modest first step to a catastrophic end point. The arguer
treats the chain as inevitable.

*Key insight:* Even if each link is individually probable, the conjunction of all links
may be improbable. Eight links at .9 probability each yield .43 probability overall.
The longer the chain and the weaker any link, the less probable the endpoint.

*Why it fails:* The assertion that the chain can't be stopped is unsupported. Most slopes
are not slippery — intermediate steps can be resisted.

*NOT a fallacy when:* The causal chain is genuinely inevitable (e.g., well-established
physical or economic mechanisms), or when the arguer provides specific evidence for
each link rather than just asserting inevitability. Some slopes ARE slippery.

---

**HASTY GENERALIZATION**

*Detection signs:* A general conclusion drawn from too few instances. Reliance on
anecdotal evidence ("my neighbor's Subaru is great, so Subarus must be great"),
small unrepresentative samples, or single dramatic cases. Also includes formation
of stereotypes from limited experience with a group.

*Why it fails:* A few instances cannot reliably represent a population.

*NOT a fallacy when:* The sample is large, representative, and properly collected.
Also, a single counterexample CAN disprove a universal claim (one black swan
disproves "all swans are white") — that's not hasty generalization, that's valid
deductive refutation.

---

### III. Illicit Presumption Fallacies

Common signature: a hidden premise is smuggled in that is controversial, unsupported,
or false.

---

**BEGGING THE QUESTION (Petitio Principii)**

*Detection signs:* The conclusion appears (sometimes in different words) as one of the
premises. The argument is circular — it assumes what it's trying to prove. Often
disguised by using synonyms or rephrasing: "Capital punishment is justified because
it is legitimate for the state to put criminals to death" (the premise just restates the
conclusion in different words).

*Why it fails:* An argument must provide reasons INDEPENDENT of the conclusion.
Restating the conclusion as a premise provides no new reason to accept it.

*Note:* Formally, question-begging arguments are technically valid (if the premise is
true, the conclusion must be true — they're the same claim). The failure is pragmatic,
not formal.

*NOT a fallacy when:* The premise genuinely differs from the conclusion in content,
not just wording.

---

**FALSE DICHOTOMY (False Dilemma)**

*Detection signs:* "Either A or B" when other options exist. Often appears as a
disjunctive syllogism: "Either A or B; not A; therefore B" — where the first premise
is false because it omits options C, D, E. Common in political rhetoric: "You're
either with us or against us."

*Why it fails:* Eliminating one option of a false dichotomy doesn't establish the other.
The fix is to "escape between the horns" by naming the overlooked alternatives.

*NOT a fallacy when:* The options really are exhaustive (genuine logical dichotomies
like "either P or not-P" cannot be false dichotomies).

---

**COMPLEX QUESTION**

*Detection signs:* A question that presupposes something controversial. "Have you
stopped cheating on exams?" presupposes that you were cheating. "Why does your
policy hurt workers?" presupposes the policy hurts workers.

*Why it fails:* Answering the question (yes or no) forces acceptance of the presupposition.

*NOT a fallacy when:* The presupposition is established fact that both parties accept.

---

**SUPPRESSED EVIDENCE**

*Detection signs:* Only evidence favorable to the conclusion is presented; unfavorable
evidence is omitted. Cherry-picking studies, citing only statistics that support one side,
telling "half the truth." Hard to detect without independent knowledge of the subject.

*Why it fails:* A fair argument must account for the full body of evidence, not just
the convenient parts.

*NOT a fallacy when:* The omitted evidence is genuinely irrelevant or the arguer
explicitly acknowledges it and explains why it doesn't undermine the conclusion.

---

**ACCIDENT**

*Detection signs:* Applying a general rule to a case that is clearly an exception. "Cutting
people with knives is illegal; surgeons cut people with knives; therefore surgeons should
be arrested." The general rule is treated as exceptionless when it isn't.

*Why it fails:* Most general rules have exceptions. The inference only works if
the rule has no exceptions — and that's the illicit presumption.

*NOT a fallacy when:* The rule genuinely is exceptionless, or the arguer provides
reasons why this particular case is not an exception.

---

**COMPOSITION**

*Detection signs:* "Every part has property P, therefore the whole has property P."
Every player on the team is mediocre → the team is mediocre. Every ingredient is
healthy → the dish is healthy.

*Why it fails:* Many properties don't transfer from parts to wholes. Weight, cost, and
quality are typical non-transferring properties.

*NOT a fallacy when:* The property DOES transfer (every part is made of plastic →
the whole is made of plastic). Whether it transfers depends on the specific property.

---

**DIVISION**

*Detection signs:* "The whole has property P, therefore each part has property P."
The team won the championship → each player is a champion. The house costs $1M →
each part costs $1M.

*Why it fails:* The reverse of composition — many properties of wholes don't
distribute to their parts.

*NOT a fallacy when:* The property genuinely distributes (the whole team died in
the crash → each member died in the crash).

---

### IV. Linguistic Emphasis Fallacies

Common signature: the arguer exploits ambiguity, selective emphasis, or loaded
language rather than providing evidence.

---

**EQUIVOCATION**

*Detection signs:* A key term shifts meaning between premises. "The law requires X"
(legal law) → "There must be a lawgiver" (natural law). Watch for words with both
literal and figurative senses, technical and colloquial senses, or broad and narrow senses.
Also includes false implicature: saying something literally true that communicates a
false impression.

*Why it fails:* The argument only works if the key term means the same thing
throughout. If it shifts meaning, the premises don't connect to the conclusion.

*NOT a fallacy when:* The term is used consistently, or the arguer explicitly
acknowledges the different senses.

---

**ACCENT / SELECTIVE EMPHASIS**

*Detection signs:* Fine print that contradicts the headline. "Up to 70% off!*" where
the asterisk leads to severe restrictions. Fast-talking disclaimers at the end of ads.
Relegating strong objections to footnotes. Omitting stress or emphasis when transcribing
spoken words, changing the conveyed meaning.

*Why it fails:* Readers/listeners form conclusions based on what's emphasized.
De-emphasizing unfavorable content is a form of deception.

---

**QUOTING OUT OF CONTEXT**

*Detection signs:* Direct quotes are used, but the surrounding context that gives them
their real meaning is omitted. The quoted words are accurate but misleading. Often
involves ellipses (...) that remove crucial qualifications, or selecting a fragment from
a passage that says the opposite overall.

*Why it fails:* The meaning of words depends on context. Stripping context can
reverse the speaker's actual point.

---

**MANIPULATIVE FRAMING**

*Detection signs:* The choice of words carries an implicit argument that bypasses
rational evaluation. "Death tax" vs. "estate tax." "Pro-life" vs. "anti-choice."
"Enhanced interrogation" vs. "torture." "Job creators" vs. "the wealthy."
The framing makes one conclusion seem obvious without providing evidence.

*Why it fails:* Loaded language smuggles in conclusions that should be argued for,
not assumed through word choice.

*NOT a fallacy when:* The language is accurate and descriptive rather than
strategically chosen to bias the audience.

---

### V. Probabilistic and Statistical Fallacies

---

**CONJUNCTION FALLACY**: Judging "A and B" as more probable than A alone.
Triggered by representativeness heuristic — the conjunction sounds more "typical."

**BASE RATE FALLACY**: Ignoring prior probability when evaluating conditional
evidence. "The test is 99% accurate" is meaningless without the base rate of the
condition being tested.

**SMALL NUMBERS FALLACY**: Drawing conclusions from samples too small
to be reliable. Small samples have high variance.

**REGRESSION TO THE MEAN**: Attributing a causal explanation to what is
merely statistical regression. After an extreme performance, the next one is
likely closer to average — no intervention needed to explain it.

**GAMBLER'S FALLACY**: Believing past independent random events affect
future probabilities. "Red has come up 10 times in a row, so black is due."
Each spin is independent.

**CAUSAL SLIPPERY SLOPE (probabilistic form)**: A chain of probabilistic
conditionals whose individual probabilities are each high, but whose conjunction
is low. See Slippery Slope above for the multiplication principle.


## Edge Cases and Judgment Calls

**Multiple fallacies in one passage.** Common. A single passage can commit a straw man
AND an ad hominem AND an appeal to emotion. Report each separately.

**Fallacy labels can overlap.** The same error can sometimes be classified under more
than one heading (e.g., an ad hominem can also be a red herring). Pick the label that
best captures what's going wrong; mention the overlap if helpful.

**Context matters.** Whether something is a fallacy often depends on unstated context.
An argument that looks like an appeal to authority might be perfectly legitimate if the
authority really is expert in the relevant field. When in doubt, flag the potential fallacy
and note what additional information would resolve the question.

**Not everything bad is a fallacy.** False premises, factual errors, poor evidence, vagueness,
and bad style are not fallacies. A fallacy is specifically a *pattern of reasoning* that fails.
A factually wrong premise in a valid argument is not a fallacy — the argument is just unsound.

**Strong arguments can contain minor fallacies.** A fallacy doesn't automatically destroy
an argument. Note the severity: does the fallacy undermine the core conclusion, or is it
a peripheral rhetorical flourish that doesn't affect the main reasoning?
