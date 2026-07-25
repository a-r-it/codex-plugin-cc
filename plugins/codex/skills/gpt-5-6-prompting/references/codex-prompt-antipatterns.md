# Codex Prompt Anti-Patterns

Avoid these when prompting Codex or GPT-5.6.

## Vague task framing

Bad:

```text
Take a look at this and let me know what you think.
```

Better:

```xml
<task>
Review this change for material correctness and regression risks.
</task>
```

## Missing output contract

Bad:

```text
Investigate and report back.
```

Better:

```xml
<structured_output_contract>
Return:
1. root cause
2. evidence
3. smallest safe next step
</structured_output_contract>
```

## No follow-through default

Bad:

```text
Debug this failure.
```

Better:

```xml
<default_follow_through_policy>
Keep going until you have enough evidence to identify the root cause confidently.
</default_follow_through_policy>
```

## Asking for more reasoning instead of a better contract

Bad:

```text
Think harder and be very smart.
```

Better:

```xml
<verification_loop>
Before finalizing, verify that the answer matches the observed evidence and task requirements.
</verification_loop>
```

## Over-structuring routine work

Bad:

```text
Wrap every two-sentence task in a long stack of XML blocks, examples, reminders,
and repeated process rules.
```

Better:

```text
Fix the null-state regression in the affected component. Preserve existing
behavior elsewhere and run the focused tests before reporting the result.
```

## Using the wrong family tier

Bad:

```text
Silently replace the user's requested Luna run with Sol because the task looks hard.
```

Better:

```text
Preserve the selected model. Make a Luna prompt bounded and explicit; if the task
cannot be made reliable within that contract, report the mismatch instead of
silently changing models.
```

## Blanket brevity

Bad:

```text
Be extremely brief.
```

Better:

```text
Lead with the outcome. Keep the evidence, material caveats, validation result,
and next action; trim repetition and optional background first.
```

## Defaulting to maximum effort

Bad:

```text
Always use max reasoning so the answer is better.
```

Better:

```text
Preserve the requested or configured effort. Improve the success criteria,
evidence contract, and verification loop before recommending a higher effort.
```

## Mixing unrelated jobs into one run

Bad:

```text
Review this diff, fix the bug you find, update the docs, and suggest a roadmap.
```

Better:
- Run review first.
- Run a separate fix prompt if needed.
- Use a third run for docs or roadmap work.

## Unsupported certainty

Bad:

```text
Tell me exactly why production failed.
```

Better:

```xml
<grounding_rules>
Ground every claim in the provided context or tool outputs.
If a point is an inference, label it clearly.
</grounding_rules>
```
