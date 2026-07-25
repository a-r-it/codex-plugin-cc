# GPT-5.6 Model Profiles

Use the profile matching the model explicitly selected for the Codex handoff. Preserve the selected model and do not put runtime flags inside the prompt.

## Family routing

| Model | Use for | Prompt emphasis |
| --- | --- | --- |
| `gpt-5.6-sol` | Complex coding, deep review, security, research, computer use, and quality-first work | Outcome, hard constraints, evidence, completion bar, and rigorous validation |
| `gpt-5.6-terra` | Everyday implementation, debugging, maintenance, and balanced review | Concrete task, local context, acceptance criteria, and focused validation |
| `gpt-5.6-luna` | Fast, bounded, high-volume, classification, extraction, routing, and lightweight coding | Narrow scope, explicit inputs, deterministic output, and a clear stop condition |

The `gpt-5.6` family alias routes to Sol. Use an explicit variant when the user names one.

## Shared GPT-5.6 rules

- Keep prompts lean and outcome-first.
- State each instruction once.
- Preserve hard constraints, approval boundaries, evidence requirements, and success criteria.
- Expose or mention only task-relevant tools.
- Let the model choose routine execution steps.
- Require validation that matches the risk of the task.
- Do not request hidden reasoning or chain-of-thought.
- Do not silently change the selected model or reasoning effort.

## Sol

Use Sol for the hardest quality-first work.

Prompt Sol with:

- the user-visible outcome and the full completion bar;
- architectural, security, compatibility, or product constraints that must survive;
- the evidence required for findings and decisions;
- explicit validation for multi-file or high-risk changes;
- permission boundaries for external, destructive, or scope-expanding actions.

Avoid:

- step-by-step micromanagement when the destination is clear;
- repeated "be thorough" or "think harder" instructions;
- globally forcing `max` effort without a measured need;
- mixing unrelated objectives into one long run.

For long-running work, request sparse updates only at major phase changes. For adversarial review, ask for material findings ordered by severity and grounded in inspected evidence.

## Terra

Use Terra for balanced everyday engineering.

Prompt Terra with:

- one concrete implementation, diagnosis, or review objective;
- the relevant local context and behavior to preserve;
- concise acceptance criteria;
- the smallest useful validation set;
- a compact output contract focused on outcome, touched areas, and checks.

Avoid:

- Sol-sized scaffolding for routine maintenance;
- broad repository exploration when the target is already known;
- multiple loosely related cleanup requests;
- verbose examples that duplicate the acceptance criteria.

Favor a short prompt that lets Terra act autonomously inside a clearly bounded task.

## Luna

Use Luna for fast, repeatable, tightly bounded work.

Prompt Luna with:

- a single narrow task;
- explicit inputs, allowed scope, and required output format;
- deterministic acceptance criteria;
- a clear stop condition;
- a small, targeted validation step when code changes are allowed.

Avoid:

- open-ended architecture, deep research, or broad security review;
- ambiguous success criteria;
- large mixed-context dumps without a named target;
- asking Luna to infer several hidden stages or reconcile unrelated goals.

For classification, extraction, or routing, provide the exact schema or labels and define how to handle missing or ambiguous input. For coding, name the affected behavior and keep the requested change small. If the task remains inherently broad or quality-first, preserve the user's model choice but make the mismatch explicit in the forwarded contract rather than pretending it is a routine Luna task.
