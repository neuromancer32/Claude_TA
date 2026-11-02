---
name: "tutor"
description: "Start or plan a study session for any class: set course context and time to exam, pick Study or Exam mode, and plan the session. Use for /tutor or \"help me study\"."
---

# Tutor

The entry point for studying any class. This skill sets up context, picks the mode, and plans the session. The work itself happens in three other skills; load them as needed:

| Skill | Use it for |
|---|---|
| `tutor-study` | Learning material: lecture walkthroughs, explanations, concept maps |
| `tutor-exam` | Testing: practice questions, drills, mock exams, grading |
| `anki-cards` | Designing and formatting flashcards |

## Learning principles (shared by all modes)
- **Retrieval practice:** testing yourself beats rereading.
- **Spacing:** review across days; revisit misses later in a session.
- **Interleaving:** mix topics when practicing.
- **Elaboration:** explain why, and connect new material to old.
- **Concrete before abstract:** what a term or symbol physically refers to comes before the math.
- **Dual coding:** pair words with figures.
- **Generation effect:** the user writes their own cards.
- **Calibration:** compare confidence with correctness; confident-and-wrong gets fixed first.
- **Sleep:** consolidation happens overnight; protect it before exams.

## 1. Gather context
Check the conversation, project instructions and files, and memory first. Ask only for what's missing, in one AskUserQuestion call if available:
- Course, exam date and time, exam format if known.
- Lectures or topics in scope, which are already covered, and which feel weak or strong.
- Existing concept maps (artifact links) and cards already made.
- Time available today.

## 2. Pick the mode
- Material not yet covered or not understood → **Study** (`tutor-study`).
- Material covered and the user wants to check it → **Exam**, drill (`tutor-exam`).
- Mid-study "quiz me on what we just did" → a 3–5 question drill, then back to Study.
- Final review → a mock exam across the full scope, then drills on what it exposes.
- Cards from any other source (paper, chapter, notes) → `anki-cards` directly.

## 3. Plan the session by time to exam
- **More than a week:** study remaining lectures at full depth with cards; a short drill at the end of each lecture; spaced review sessions about 1, 3 and 7 days after each.
- **2–7 days:** study remaining lectures, with depth set by the user's weak and strong ratings; a daily interleaved drill; cards mainly for weak spots.
- **48 hours or less:** coverage and understanding first; 3–5 card suggestions per lecture, to make later; drills on weak areas; one short mock; stop in time for sleep.
- **Morning of the exam:** a light mixed drill and a pass over key formulas and traps. No new material.

Give the plan as a short ordered list with rough time per block, then start.

## 4. Run it
- Load the mode skill and follow it. Switch modes whenever the user asks.
- Tune depth per lecture: full depth for hard or quantitative lectures, key ideas and traps for ones the user is comfortable with.
- At each transition, give a two-line status: what's covered, weak spots so far, what's next.

## 5. End of session
A short summary: what was covered, weak spots found, cards suggested, and the plan for the next session.