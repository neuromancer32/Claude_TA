---
name: "tutor-exam"
description: "Exam mode for any class: generate practice questions from the user's course material, run drills or timed mock exams, grade answers, and track weak spots."
---

# Tutor: Exam mode

Use when the user wants to test themselves, asks for practice questions, a quiz or a mock exam, or says "exam mode". Session planning and exam-crunch triage live in the `tutor` skill; learning new material lives in `tutor-study`; card rules live in `anki-cards`.

## Learning principles behind this mode
- **Retrieval practice.** Pulling an answer from memory strengthens it far more than rereading.
- **Interleaving.** Mix topics and lectures within a set instead of blocking by topic.
- **Desirable difficulty.** Prefer prediction, application and calculation over definitions.
- **Feedback timing.** Immediate feedback in drills; delayed feedback in mock exams.
- **Calibration.** Ask for confidence before revealing answers. Confident-and-wrong answers are the highest-priority fixes.
- **Spacing.** Bring missed items back later in the same session, reworded.

## Start
Ask only what isn't already known from the conversation, project or memory (one AskUserQuestion call if available):
- Scope: which lectures or topics, and which feel weak.
- The real exam's format if known: multiple choice, short answer, calculations, figure interpretation.
- Mode: **Drill** or **Mock**, and length (default: drill of 10, mock of 15–20 with a suggested time).

Build questions from the user's own course material first (decks, notes, earlier study sessions, concept maps). Label anything that goes beyond it.

## Question design
Rough mix per set (adjust to the subject):
- Predict / what-if (a drug, a parameter change, a lesion, a mutation): ~30%
- Explain why / mechanism: ~25%
- Calculation with realistic numbers (quantitative courses): ~20%
- Figure or data interpretation (describe a trace or cite a slide figure): ~15%
- Distinguish commonly confused pairs: ~10%

Weight about 60% toward weak topics, but touch every lecture in scope.

Multiple choice: four options, one best answer, distractors built from real misconceptions (sign errors, swapping related quantities, right idea in the wrong direction). No "all of the above". The explanation says why each distractor is wrong.

Free response: write the grading rubric (key points and partial credit) before asking, then grade against it.

Check every answer key. Run calculations in code. Don't assert a fact you aren't sure of; if a model or slide is ambiguous, say so in the explanation.

Don't repeat questions the user already answered correctly this session.

## Drill
- One question at a time. Ask the user to give a confidence rating (sure / think so / guessing) with each answer.
- If they ask for help, use a hint ladder: a nudge, then a narrower nudge, then the first step worked out. Never reveal the answer before an attempt.
- Give feedback right away: correct or not, the reasoning, the misconception behind a wrong answer, and where it is in the lecture.
- For batches of multiple-choice questions, use the quiz widget (`mcp__widgets__quiz_display_v0`) when it's available: plausible distractors, a hint, an explanation, and short per-question feedback labels. Its flashcards view suits a quick final review.
- Bring each miss back 3–5 questions later as a reworded variant.

## Mock exam
- Present the full set with point values and a suggested time. No feedback until the user submits.
- Grade with the rubrics, including partial credit, and score by topic.
- List confident-and-wrong answers first.

## After every session
A short summary:
- Score by topic, confident-and-wrong items, and the misconceptions found.
- What to re-study (specific slides or concept-map sections).
- 3–6 card suggestions for the misses, following the `anki-cards` skill.
- An offer of the next set, weighted toward the misses.