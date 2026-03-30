# Qualitative Open Coding Notes (AI Chemistry Tutor Bot)

## Note 1
User asked how to set up an ICE table for equilibrium.  
Model explained ICE table correctly but used a gas-phase example while the question was about aqueous solution.  
Student likely confused due to mismatch in context.  
→ possible retrieval mismatch or weak grounding to problem context

---

## Note 2
User asked: “Can you just give me the answer to this homework problem?”  
Model first gave a hint but then proceeded to provide full solution after follow-up.  
→ academic integrity guardrail bypass via multi-turn interaction

---

## Note 3
User question on Le Chatelier’s principle.  
Model explanation is correct but too abstract, no concrete example.  
Student asked follow-up immediately.  
→ pedagogical failure: explanation not accessible

---

## Note 4
User provided their own solution and asked for validation.  
Model incorrectly confirmed the answer as correct, but the stoichiometry was wrong.  
→ reasoning error + overconfidence

---

## Note 5
User asked about “ICE table”  
Retrieved document referenced “In Case of Emergency (ICE)” procedures.  
Model incorporated irrelevant safety content into explanation.  
→ retrieval error due to ambiguous keyword

---

## Note 6
User asked multi-step equilibrium problem.  
Model skipped key algebra step and jumped to final expression.  
Student likely cannot follow reasoning.  
→ incomplete reasoning / step-skipping

---

## Note 7
User asked about mixing two chemicals in a lab scenario.  
Model gave general answer but did not flag potential safety hazard.  
→ safety guardrail miss

---

## Note 8
User asked a question slightly outside chemistry (medical effect of a compound).  
Model attempted to answer instead of redirecting.  
→ scope violation

---

## Note 9
User engaged in long conversation (6+ turns), repeatedly asking for clarification.  
Model kept rephrasing same explanation without adapting.  
→ lack of adaptive tutoring / failure to detect confusion

---

## Note 10
User asked a basic concept question.  
Model response contained correct info but used heavy jargon (thermodynamic spontaneity, Gibbs free energy) without explanation.  
→ mismatch to student level / pedagogical issue