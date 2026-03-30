# PRD: AI Chemistry Tutor Bot

## 1. Overview

**Product Name**: AI Chemistry Tutor Bot  
**Primary Goal**: Provide accurate, step-by-step chemistry learning support while enforcing academic integrity and safety constraints.

### Problem Statement
Students struggle with:
- Understanding multi-step chemistry concepts (e.g., stoichiometry, equilibrium, thermodynamics)
- Getting timely help outside office hours
- Distinguishing correct vs. misleading explanations

### Solution
An AI tutor that:
- Guides students through reasoning (not just answers)
- Adapts explanations to student level
- Escalates to human TA when needed

---

## 2. Target Users

### Primary
- Undergraduate chemistry students (Gen Chem, Organic Chem)

### Secondary
- Teaching assistants (TA support, load reduction)
- Instructors (insight into student struggles)

---

## 3. Intended Use Cases (Core Scenarios)

### U1: Concept Explanation
- “What is Le Chatelier’s principle?”
- Expected: Clear, level-appropriate explanation + example

### U2: Step-by-Step Problem Solving
- “How do I solve this equilibrium constant problem?”
- Expected: Guided steps, not full solution dump

### U3: Error Diagnosis
- “Why is my answer wrong?”
- Expected: Identify mistake + explain correction

### U4: Study Support
- “Quiz me on acid-base reactions”
- Expected: Interactive questioning + feedback

### U5: Clarification Follow-ups
- Multi-turn dialogue with memory of context

---

## 4. Non-Goals (Critical Constraints)

- ❌ Do NOT complete graded homework or exams directly  
- ❌ Do NOT fabricate chemistry facts or equations  
- ❌ Do NOT provide unsafe lab instructions  
- ❌ Do NOT answer outside defined chemistry scope (e.g., medical advice)

---

## 5. Functional Requirements

### F1: Instructional Reasoning
- Provide step-by-step explanations
- Use scaffolding (hint → partial → full explanation)

### F2: Context Awareness
- Maintain multi-turn conversation state
- Track student confusion signals

### F3: Knowledge Grounding
- Use curated chemistry knowledge base (textbook, instructor materials)
- Avoid relying solely on base LLM knowledge

### F4: Adaptive Responses
- Adjust explanation depth based on:
  - Student level
  - Past interaction signals

### F5: Escalation Mechanism
- Trigger handoff when:
  - Low confidence
  - Repeated failure
  - Safety/ambiguity risk

---

## 6. System Design (High-Level)

### Core Components
- LLM (reasoning + dialogue)
- Retrieval (RAG over course materials)
- Guardrails layer (policy + classifiers)
- Conversation memory store
- Evaluation & logging system

### Key Risks
- Retrieval mismatch (e.g., ICE = equilibrium vs emergency)
- Hallucination in scientific explanation
- Over-helping (violating academic integrity)

---

## 7. Success Metrics

### Product Metrics (North Star)
- **Resolution Rate Without Escalation**
- **Student Satisfaction (thumbs up/down)**
- **Learning Outcome Proxy** (e.g., retry success)

### Behavioral Signals (Leading Indicators)
- Repeated “regenerate” clicks
- Long multi-turn loops without resolution
- Drop-off mid-session

### System Metrics
- Latency
- Retrieval accuracy
- Escalation rate

---

## 8. Evaluation Strategy (Built-in)

### Pre-Release (Offline Evals)

#### Qualitative (First)
- SME review of ~50–100 scenarios
- Open coding → error taxonomy

#### Quantitative (Then)
- Scenario-based evals:
  - Concept accuracy
  - Reasoning correctness
  - Pedagogical quality
  - Policy compliance

---

### Post-Release (Online Analytics)

- Monitor:
  - Resolution vs escalation
  - Error category frequency
  - Drift in failure modes

- Tie eval metrics → product metrics

---

## 9. Guardrails & Safety Constraints

### Academic Integrity
- Provide guidance, not direct answers for graded work
- Use “hinting strategy” instead of full solution

### Scientific Accuracy
- Must align with validated chemistry sources
- Flag uncertainty explicitly

### Lab Safety
- Block unsafe or hazardous instructions

### Privacy (FERPA-aligned)
- Do not expose student data
- Log anonymized interactions only

---

## Notes (Design Principles)

- Scope = capability + constraints  
- Evals are tied to product metrics, not standalone  
- Human judgment anchors evaluation; automation scales it  