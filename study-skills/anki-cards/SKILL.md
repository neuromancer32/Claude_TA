---
name: "anki-cards"
description: "Design and format Anki flashcards from any material (lectures, papers, notes): pick the card type per concept, write atomic cards, tag figures, and format them to paste."
---

# Anki cards

Use whenever flashcards are wanted: during `tutor-study` walkthroughs, for misses after a `tutor-exam` session, or on their own from a paper, chapter or notes.

## Default output
Recommend cards in chat, one code block per card, grouped under a short header per card type. The user makes the cards by hand, which is itself a study method. Produce an import file only when asked.

## Plan before writing
1. List the examinable concepts in the chunk first: mechanisms, causal links, experimental logic, predictions, and anything the user or instructor flagged as important. Skip slide framing, citations and trivia.
2. If past exams or instructor hints are known, phrase cards the way the course asks (predict the result, explain why, what does this experiment show).
3. Aim for roughly one card per key fact; a dense chunk is usually 8–15 cards, not 30. Fewer good cards beat many weak ones.
4. Check the plan against every card already given in the conversation before writing anything.

## Choosing the type

| Type | Use for | Avoid when |
|---|---|---|
| Basic | Why/how questions, mechanisms, consequences, "what happens if" | The answer is a list of several facts |
| Basic and reversed | Short pairs needed both ways: term ↔ short definition, drug ↔ target, symbol ↔ meaning. Both sides a few words. | Either side is longer than a short phrase, or the reverse question would be ambiguous |
| Type-in | Short numbers, one-word predictions (increases/decreases), which-one choices | The answer needs explanation or has several valid phrasings |
| Cloze | A single equation; parallel facts that don't give each other away; multi-step pathways or processes (one note per pathway, each meaningful step its own cloze number; visible neighboring steps are fine as cues) | Clozes on one note would reveal each other, or the deletion is a trivial linking word |
| Image Occlusion | Diagram labels, curve identities, circuit parts, traces to sketch | The figure isn't worth remembering visually |

Several cards on one concept from different angles (definition, mechanism, application) is fine for important ideas, as long as each angle tests something the others don't.

## Writing and quality rules
- **Atomic.** One fact per card. The back is short and specific: one idea, ideally under ~20 words.
- **Standalone.** Each card makes sense on its own inside a large deck, months later, with no slides open. No slide numbers, figure numbers, lecturer names, "as on the slide", or named models/papers as the cue on the front or back (e.g., ask "How does CaMKII strengthen existing AMPARs?" not "In the X/Y/Z model, …"). [IO]/[BACK] tags are instructions, not card text, and may reference slides.
- **Visual over prose.** When the answer is structural or a multi-step pathway, put a compact arrow chain or text diagram on the back (inside the code block), use a pathway cloze, or point to a figure with [IO]/[BACK], rather than writing a paragraph. Never put a diagram on the front that reveals the answer.
- **One right answer.** Make the front specific enough that only one answer fits.
- **No giveaways.** The answer must not be visible elsewhere on the card, including cloze siblings and nearby text.
- **Test understanding.** Ask why, how, or what happens if. Don't ask the user to recall the slide's wording or how a slide was organized.
- **No trivial corollaries.** Don't write a card whose answer follows directly from another card's answer (e.g., after a definition card "silent synapse = NMDAR only", skip "which receptor carries a silent synapse's response?").
- **Equations:** cloze the meaningful part (a whole right-hand side, a key term), not a trivial symbol. Two formulas that share variables go on separate notes.
- **Numbers:** give units, and state the expected format in the question ("nearest 10, with sign").
- **Type-in:** the back holds only the answer, because Anki compares the whole field. List the allowed options in the question when it's a choice.
- **No duplicates** of cards already recommended in the conversation or that the user says they have. The same fact asked from a reworded angle counts as a duplicate unless it tests something different.

## Revising cards
- When the user says cards are poor, name what's wrong with specific cards, then give one consolidated replacement set and say explicitly which earlier sets it replaces. Don't patch across several messages; that is how duplicates appear.
- Mark which earlier cards the user can keep, so they don't rewrite good ones.

## Formatting
- Math uses MathJax: `\( \)` inline, `\[ \]` display. Anki does not read `$$`.
- In a cloze, when `}}` would follow a math brace, add a space: `{{c1::\frac{a}{b} }}`.
- Plain text with Unicode subscripts (E_Na, K⁺) is fine where MathJax isn't needed.

## Figures
- `[IO: slide N, region; what to cover as which groups; Hide One or Hide All]`. Cover labels and key parts, not the whole figure. Hide One suits independent labels; Hide All suits labels that would give each other away. For traces worth sketching, cover the trace and sketch it before revealing.
- `[BACK: slide N figure → which card]` for context images on card backs.
- Image Occlusion notes can't be imported from text; the user makes them by hand.

## Paper exercises
For derivations, sketches and calculations, which flashcards test badly, suggest a short paper exercise instead of, or alongside, cards.

## Card validation (run on every card before sending; drop or rewrite any that fail)
- **Atomic:** one fact; short, specific back.
- **Standalone:** no slide, figure, lecturer or model-name references in the card text.
- **One right answer**, and the answer is not visible on the card or its cloze siblings.
- **New:** not already given in the conversation, not a reworded duplicate, not a trivial corollary of another card.
- **In scope:** relies only on the knowledge body the user specified (attached documents or chat history).
- **Worth it:** the user would lose exam points or real understanding without it, and it will still matter in a month.

## Import file (only when asked)
Tab-separated text with these header lines:
```
#separator:tab
#html:true
#notetype column:1
#deck:Course::Lecture
#tags column:4
```
Columns: note type, field 1, field 2, tags. Use the default note type names ("Basic", "Basic (and reversed card)", "Basic (type in the answer)", "Cloze"); Anki 2.1.55 or later. HTML-escape `<`, `>` and `&`. Tags like `course::lecture::topic`, plus `needs-image::slideNN-description` on cards that should get a figure, so the user can find them with `tag:needs-image*`.