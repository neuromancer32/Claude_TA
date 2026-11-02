---
name: "tutor-study"
description: "Study mode for any class: walk through lecture decks chunk by chunk, explain concepts concretely, recommend cards, and keep concept-map pages updated."
---

# Tutor: Study mode

Use when the user shares lecture material (slides, PDFs, notes, screenshots) to learn it, or says "study mode". Session planning and exam triage live in the `tutor` skill; testing lives in `tutor-exam`; card rules live in `anki-cards`.

## Setup (once per lecture)
1. Get the whole deck, not just screenshots, when possible. For .ppt/.pptx: `soffice --headless --convert-to pdf` then `pdftoppm -png -r 90`; also convert .ppt to .pptx and pull slide text and speaker notes with python-pptx. Look at every slide image, since equations and figures are often images that text extraction misses.
2. Note blank slides, duplicates, missing speaker notes, and typos or errors on slides.
3. Give a lecture map: a short table of slide ranges and topics, plus one or two sentences on the question the lecture answers.
4. Set the depth from what the user says about their comfort with this lecture. Hard or quantitative lectures get full depth; familiar ones get key ideas, traps and fewer cards. Ask only if there's nothing to go on.

## Each chunk (1–3 related slides; the user says "next")
- Read the slide in order: axes, traces, labels, what each part shows.
- For each new symbol or term, say what it physically is before any equation.
- Give the logic of derivations as short steps, with unit checks where useful.
- Link to earlier lectures and to the concept maps.
- Flag slide errors, notation clashes, sign conventions and common exam traps. Label anything beyond the slides.
- Draw a small inline chart when numbers explain a shape.
- One chunk per reply; end by naming what the next chunk covers.
- Format for reading: a header per slide, tables for comparisons, math in LaTeX. No narration of your process.

## Cards
After each chunk, recommend cards following the `anki-cards` skill (load it once per session), including figure tags and paper exercises.

## Concept maps
Keep a small set of published HTML artifact pages that distill the course, and update them after each lecture:
- **Term or parameter map:** every symbol or term with what it physically is, units, typical values, when it changes, where it appears, an "easy to mix up" list, and a quiz mode that blurs meanings until tapped.
- **Mechanism or process maps:** made when a lecture introduces a mechanism, method or sequence that doesn't fit the term map. Use an interactive simulation when a small, standard model exists, and label model output as illustrative.
- Update existing pages at the same URL; never create duplicates. Cross-link the maps.
- Follow the Artifact tool's rules, including its quickstart before a new page. Take one look at the rendered page after edits.
- Don't make the user wait on maps: send the lecture content first, then build or update.