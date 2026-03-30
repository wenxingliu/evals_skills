# Technical Design Document: AI Chemistry Tutor Bot

## 1. Purpose

This document describes the high-level technical design for an AI chatbot that supports students in a chemistry class.

The system is designed to:
- answer chemistry questions using course-approved materials
- provide step-by-step tutoring support
- avoid unsafe, off-scope, or academically inappropriate responses
- escalate or refuse when needed

This is a **RAG-based system with guardrails**.

---

## 2. System Goals

### Primary goals
- Provide accurate, course-aligned chemistry help
- Ground responses in approved course content
- Support multi-turn tutoring conversations
- Enforce guardrails for academic integrity and safety

### Non-goals
- Solve graded homework or exams directly
- Provide unsafe lab instructions
- Answer outside the chemistry tutor scope
- Act as a replacement for instructors or TAs

---

## 3. High-Level Architecture

```text
User
  |
  v
Chat Interface
  |
  v
Application Server / Orchestrator
  |-----------------------------|
  |                             |
  v                             v
Guardrails (input)              Conversation Memory
  |
  v
Retrieval Pipeline
  |
  v
Vector Database / Knowledge Base
  |
  v
LLM Generation
  |
  v
Guardrails (output)
  |
  v
Response to User