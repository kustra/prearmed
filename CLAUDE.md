Read @Prearmed.md first: it holds the core idea behind this repository.

# Composing technical English texts

These rules apply to every English technical text, such as documentation, code comments and commit messages.

The goal: a reader new to the subject understands, in a single pass, the text's core idea, the one thing they must leave with. The core rule: the reader never meets a concept before it has been introduced. Most rules below follow from the core rule, and all of them serve the goal: where following one literally would make a text harder to read, the goal wins.

## Before writing
- Decide who the reader is: what they already know (for example, the domain and the platform) and what is new to them (the subject). Explain only what is new.
- Decide the core idea. Then plan the order in which the reader needs the concepts that lead to it. Outline that order as a chain of concepts, not a list of facts.
- If the request lists points to cover, treat the list as a checklist of content, not as the text's structure.

## Order: build the reader's understanding step by step
- Put why before how, the core idea before the details, and the whole before its parts (the platform before its services, the system before its components).
- A subject's setting is the environment it lives in, such as a platform. State the core idea in one plain sentence that would hold in any setting. The concepts the core idea needs come before it.
- For a text that describes a product or a system, this sequence usually works. Drop the steps that do not apply:
  1. what kind of thing the subject is;
  2. why it exists: the problem it solves or the principle it stands for;
  3. the core idea;
  4. the subject's setting;
  5. the mechanism that realizes the core idea in that setting;
  6. edge cases;
  7. how to get the product or system;
  8. how to use it;
  9. the licence and similar facts.
- Mark the core idea's sentence with a signpost, such as "The core idea is …".

## Introduce every concept before using it
- Use no term specific to the subject before introducing it, unless the same sentence defines it. A concept needs no introduction when it is implied by the kind of thing the subject is: a text about a heartbeat service need not introduce heartbeats or alerts. When unsure whether a concept is implied, introduce it.
- Watch for definite forms ("the job", "each job's") that assume the reader already knows the thing. Introduce the thing before the definite form.
- Introduce a new concept by its role: what it does or what it is for.
- Before coining a term for a concept, explain the concept in plain words, and coin the term only if the text uses the concept again.

## Sentences
- Introduce at most one new concept per sentence. Two may share a sentence when neither is clear without the other.
- Give each sentence one main relationship between its concepts, such as what does what or what causes what. Split a sentence that makes the reader hold several clauses before it resolves.
- Keep the core idea's sentence free of edge cases and exceptions. They get their own sentences, after it.

## Cohesion: each sentence picks up from the one before
- Put what the reader already knows at the start of a sentence and the new information at the end. A paragraph's first sentence is the exception: it may open with the new concept it introduces ("Jobs send heartbeats over HTTPS").
- Use one name for each concept, and each name for one concept only.
- Give each pronoun one unambiguous referent. When more than one is plausible, use the name.
- Each paragraph serves one purpose. Order the paragraphs as the steps of the argument.
- Never say one thing twice in different words. A sentence that adds something, such as the mechanism after the core idea or a concrete case after an abstract statement, is not a repeat.
- Use connectives ("so", "because", "but") that show how sentences relate.

## Formatting
- Format as the request asks. When it says nothing, use the least formatting that serves the reader.
- Emphasis (bold or italics) marks at most one or two phrases in the whole text: those that carry the core idea.

## Revising
- After any edit, reread the whole text from the top as the reader would, not only the edited sentence. A local fix can break the order: moving a paragraph up can leave its terms undefined.
- When asked to move content or change what a passage says, rewrite every paragraph whose order or terms the change affects. Do not transplant sentences.
- A request to change only wording needs only the wording changed. If the reread finds a problem outside the request, report it instead of fixing it unasked.
- Ask two questions of every sentence: would the reader miss it, and is it in the right place, joined to its neighbours? Cut only a sentence the reader would not miss: shortness serves the goal but is never a goal itself.
- When someone reviews a text for you, ask for two things: what the text conveys, and where reading stalled (an undefined term, a jump, an unclear reference). A reviewer who can restate the facts may still have stalled.

# Comments and commit messages

**Comments** (every language in the repo, scripts included). The default is to delete: a comment stays only if it earns its place, and is as short as it can be.
- **Never restate the code.** What a name, a type, a signature or a test title already says is not repeated; rename before explaining.
- **What earns a comment:** a decision and its reason, or a constraint the code cannot show — an ordering that matters, a platform trap, a bound the code relies on.
- **No history.** A comment describes the code as it is — never what it replaced, what was tried, or what "no longer" happens. A decision stands on its own merits; the past lives in git.
- **No plan documents.** Plans, task lists, review findings and anything else git does not track are volatile; code outlives them. A durable reference names an ID the code itself defines, never a line number.
- **Existing comments are no precedent.** Where surrounding code breaks these rules, do not imitate it; fix or delete the comments on the lines you touch.

**Commit messages** (every commit). The default is short: a headline, and a body only when it earns its place.
- **The headline** says in one line what changed, in the product's terms, not the files'.
- **Never restate the diff.** No list of files, functions, values or counts the diff already shows; no "update X and Y".
- **What earns a body:** context that could conceivably be useful to someone who reaches the commit through `git blame`. Usually this is the reason — the problem the change solves or the decision it makes, and why; a constraint the diff cannot show; or a deliberate omission.
- **No process.** The message says what changed, not how it was made: no agents, workflows, review rounds or finding counts, no test runs, no dead ends, no "as discussed", no scratch paths. Unlike a comment, a commit is history: it may say what the change replaces, and why.
- **Durable references only:** an ID the code itself defines, never a line number or anything git does not track.
- English, with the coding agent's Co-Authored-By trailer.

# Line width

- Markdown files have no maximum line width. Break lines wherever it is semantically reasonable.
- The same holds for commit messages, except the headline.
- Code, including comments, has a maximum line width of 120 characters.

# Error handling

**Never swallow an error silently.** Code swallows an error when it neither surfaces the error to the user nor recovers from it in a meaningful way. Logging the error does not surface it.
- Challenge whether swallowing is appropriate. It is appropriate only when all three conditions hold: the operation that failed is non-critical or diagnostic, the product works correctly without it, and the error cannot become persistent in a way that silently degrades the product.
- An error that is transient now but could become persistent, for example by failing every heartbeat, fails the third condition. It needs escalation: surface the error to the user once it becomes persistent.
- Every place that swallows an error carries a comment that explains why the error is safe to ignore.
