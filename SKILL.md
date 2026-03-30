---
name: error-taxonomy-generator
description: Create a practical, root-cause-level error taxonomy for a text-based GenAI product from product requirements, technical design, and qualitative open-coding notes. This skill clusters recurring failures into a two-level taxonomy, prioritizes them, attaches examples, and identifies ambiguity or evidence gaps for later follow-up.
---

# Error Taxonomy Generator

## Overview

Use this skill to create a practical error taxonomy for a text-based GenAI product such as a chatbot, RAG application, or agentic system.

The purpose of this skill is to:
- turn qualitative evaluation evidence into a structured error taxonomy
- organize failure modes at the **root-cause level**
- make the taxonomy as mutually exclusive and collectively exhaustive as practical
- assign priorities based on severity and recurrence
- include representative examples for each error type
- identify which error types are likely in scope for later quantitative evaluation
- explicitly note where evidence is sparse, ambiguous, or insufficient

This skill is for **taxonomy creation only**. It should not design quantitative metrics, choose evaluators, define thresholds, or produce monitoring plans.

## Inputs Required
- `prd`: The path to the product requirements file.
- `technical_design`: The path to the technical design file.
- `notes`: The path to the qualitative open-coding notes file.

## Instructions

### Step 1: Read product context
Read the PRD and summarize:
- intended user value
- intended use cases
- unsupported cases
- major safety / guardrail expectations
- major launch-critical risks

### Step 2: Read the technical design
Identify:
- the major system components
- likely root-cause zones
- architecture-specific failure modes

Examples:
- RAG systems: retrieval, grounding, citation support
- agentic systems: routing, tool choice, tool execution, handoffs, recovery
- plain LLM systems: instruction handling, scope control, policy handling, context handling

### Step 3: Read qualitative open-coding notes
Identify:
- repeated failure patterns
- repeated likely causes
- representative examples
- disagreements or ambiguities in labeling
- where evidence is thin

### Step 4: Cluster the failures into root-cause groups
Group observations into candidate root-cause categories.

Use the technical design to avoid grouping together failures that look similar on the surface but arise from different system causes.

### Step 5: Organize into a taxonomy

Each specific error type should include:
- definition
- examples
- priority
- likely system area
- whether it is likely in scope for later quantitative evaluation

### Step 6: Assign priority
Assign:
- `P0` for severe, launch-blocking, or safety-critical error types
- `P1` for important and recurring error types
- `P2` for lower-priority or exploratory error types

Use both:
- severity
- recurrence

If recurrence is unknown but severity is high, it can still be `P0`.

### Step 7: Check taxonomy coverage
Review whether the taxonomy covers:
- core product behavior risks
- safety / guardrail risks
- architecture-specific failure modes
- important out-of-scope or refusal failures
- known high-risk use cases

Mark each area as:
- `covered`
- `partially_covered`
- `not_covered`

### Step 8: Note ambiguity explicitly
Create an explicit list of unresolved or ambiguous areas.

Examples:
- insufficient evidence to separate two categories
- uncertainty whether a failure is due to retrieval or generation
- uncertain severity because the use-case frequency is unknown

Do not force a clean taxonomy when the evidence does not support it.


## Output Format

Return output in the following JSON shape:

```json
{
  "error_taxonomy": [
    {
      "error_type": "string",
      "description": "string",
      "priority": "P0 | P1 | P2",
      "examples": ["string"],
      "likely_system_area": "string or null",
      "in_scope_for_quantitative_eval": true
    }
  ],
  "taxonomy_coverage_notes": [
    {
      "area": "string",
      "status": "covered | partially_covered | not_covered",
      "notes": "string"
    }
  ],
  "unresolved_or_ambiguous_areas": [
    {
      "issue": "string",
      "why_ambiguous": "string",
      "recommended_next_step": "string"
    }
  ]
}
```

## Taxonomy Design Principles

Follow these principles:

1. **Build a root-cause-level taxonomy, not a symptom-only taxonomy.**
2. **Make the taxonomy as MECE as practical.**
3. **Prefer categories that are actionable and likely to recur.**
4. **Do not invent artificial precision when the evidence is weak.**
5. **Include representative examples under each error type.**
6. **Mark whether each error type is likely in scope for later quantitative evaluation.**
7. **Explicitly preserve ambiguity when evidence is insufficient.**


## Taxonomy Quality Checks

Before finalizing the taxonomy, check for the following failure modes:

### 1) Duplicate or overlapping categories
Avoid two categories that describe essentially the same root cause.

### 2) Categories that are too broad
Example of too broad:
- `reasoning_failure`

If needed, split broad categories into more operational subtypes.

### 3) Categories that are too narrow
Avoid categories that are so specific they are unlikely to recur.

### 4) Mixing layers of abstraction
Do not mix:
- root causes
- symptoms
- business outcomes

### 5) Categories unsupported by evidence
Do not invent confident categories that are not grounded in:
- qualitative notes
- PRD risks
- technical design

### 6) Missing major risk areas
Check whether the taxonomy covers major risks implied by:
- intended use cases
- out-of-scope scenarios
- safety / guardrails
- architecture type

### 7) Sparse-evidence cases
If the evidence is too limited to confidently separate categories, say so explicitly.

“Not enough evidence” is an acceptable outcome for parts of the taxonomy.


### Example:
- retrieval
  - retrieval_miss
  - retrieval_irrelevance
- tool_use
  - tool_selection_error
  - tool_execution_failure
- policy_handling
  - refusal_logic_failure
  - unsafe_policy_bypass
