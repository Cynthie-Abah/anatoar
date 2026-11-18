# LLD — Learning Modules, Quizzes, and Local Progress

## Purpose

Provide structured learning content connected to the 3D anatomy viewer, plus simple knowledge checks and local-only progress.

## Content model

A learning module contains:
- stable module ID
- title and overview
- anatomy system ID
- ordered learning steps
- related structure IDs
- content references
- review status

A learning step may contain:
- heading
- explanatory text
- related structure IDs
- optional model action (select/highlight a structure)
- optional animation ID
- source references

## Learning flow

1. Learner opens the cardiovascular module.
2. Learner selects a learning step.
3. The step's explanation is displayed.
4. Related model structures are selected/highlighted when requested.
5. Learner moves to the next step.
6. Completion is recorded locally if the learner chooses to track progress.

## Quiz behavior

Initial question types:
- multiple choice
- true/false

Each question contains:
- ID
- prompt
- answer options
- correct option ID
- explanation
- source/review metadata

On submission:
1. Validate that an option has been selected.
2. Compare the selected option with the answer key.
3. Display correct/incorrect feedback.
4. Display the explanation.
5. Update the local session result.

Because the quiz content and answer key are delivered to the browser, this is an educational knowledge check, not a secure examination system. Do not market it as a proctored or tamper-proof assessment.

## Local progress

- Store only non-identifying module completion and bookmark IDs.
- Version the local storage schema.
- Validate parsed values before using them.
- Recover gracefully from malformed or unavailable local storage.
- Include a clear-progress action.
- Do not sync data to a server or associate it with a user identity.

## Content quality

- Use reviewed educational sources.
- Keep citations with the relevant content.
- Have anatomy content checked by a suitably knowledgeable reviewer before presenting it as authoritative.
- Flag draft or unreviewed content during development.

## Acceptance criteria

- Learner can move through a module without an account.
- Learning steps can highlight associated model structures.
- Quiz answers produce clear feedback and explanations.
- Progress/bookmarks remain local to the browser.
- Clearing local data works.
- No learner data is sent to a backend.
