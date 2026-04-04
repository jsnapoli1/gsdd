# Spec Checklist

Use this checklist while drafting or reviewing a GSDD spec.

## Business Truth

- What problem is being solved in production?
- Who benefits if this works?
- What business rules are fixed facts, and what details in the story are only examples?

## Actors And Permissions

- Who initiates the workflow?
- Who approves, edits, overrides, or views it?
- Which actions require audit logging?

## Workflow

- What starts the flow?
- What is the happy path?
- What alternate flows are allowed?
- What failures must be surfaced to the user?
- Which states exist, and what transitions are legal?

## Matching And Rules

- How do we decide whether an existing entity matches a new request?
- What fields are required?
- What must be unique?
- When do revisions, attachments, or source records invalidate prior work?

## External Effects

- Which notifications are sent?
- Which external systems are involved?
- What happens if those systems fail or are delayed?

## Acceptance

- What must be demonstrably true in the UI?
- What must be demonstrably true in APIs, jobs, or background processing?
- What is explicitly out of scope for this iteration?
