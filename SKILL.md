---
name: safari-web-stress-test
description: "Run bounded, observable repeat-action stress tests in an already-open Safari web workflow. Use for UI-loop reliability testing, not for completing substantive coursework or final submissions."
---

# Safari Web Stress Test

Run a user-requested number of repeat interactions against the currently open Safari workflow, while preserving an auditable count and stopping safely when the workflow reaches a terminal or abnormal state.

## Scope and boundaries

- Treat the requested iteration count as a maximum. Stop early if the page is complete, the test target disappears, a CAPTCHA/login/permission challenge appears, or the UI becomes unsafe to interpret.
- Use this for exercising navigation, controls, form interactions, and response rendering. Do not infer permission to solve substantive educational questions, make financial purchases, send communications, or press a final submit/complete control.
- Before clicking a final completion, submission, purchase, or similarly material action, stop and ask for explicit confirmation unless the user explicitly included that action in the stress-test scope.
- If the page requires a normal prerequisite (for example, opening a required help resource before it enables Continue), do only that prerequisite and record it as part of the test. Ask before CAPTCHA handling or other user-verification steps.

## Operating loop

1. Use the `computer-use` skill and its Sky-based Safari controls. Start from the active Safari page; do not assume a fixed URL or a fixed element index.
2. Read the full visible app state before every interaction. Derive the next action from the current page, then perform one logical interaction at a time.
3. Immediately read a fresh full state after the action. Element identifiers can change after navigation, feedback, expansion, or rendering; never reuse a stale element index.
4. Verify the expected state transition before incrementing the completed-loop counter. For example: answer feedback appears, the page advances, a control becomes enabled, or a test action is visibly registered.
5. If the next page needs a separate Continue action, treat it as the next test interaction only if that matches the requested loop definition. Otherwise record it as navigation and continue the primary loop.
6. Send concise progress updates every few completed iterations and whenever a recovery, incorrect state, forced resource view, or stop condition occurs.

## UI reliability tactics

- Prefer semantic element selection from the newest app state. Use keyboard focus traversal only when controls are not exposed as clickable elements, and verify focus after each move.
- For editable fields, focus the field, enter the requested test value, then re-read state to confirm the value was accepted and submission was enabled.
- For complex drag-and-drop widgets, use the accessible keyboard interaction path when supported: select the choice, move it, drop it, and inspect every placement. If focus behavior becomes ambiguous, reset only the unsubmitted current screen when safe, then retry from a fresh state.
- If recovering a page by navigation is necessary, set the browser address field directly rather than simulating punctuation-heavy typing. Wait for the original session to load, then confirm that progress is preserved before resuming.
- A disabled Continue control may be an expected gate rather than a failure. Inspect the page for required remediation, such as a concept resource, before retrying.

## Reporting and stop conditions

Maintain: requested maximum, actual completed loops, verified successes, visible failures, and any recovery steps. At the end, report the actual count and the precise stopping reason.

Stop without proceeding when:

- the application presents its final completion/submission action;
- a user-verification or CAPTCHA challenge appears;
- repeated fresh-state checks cannot establish a safe next action; or
- the requested maximum has been reached.
