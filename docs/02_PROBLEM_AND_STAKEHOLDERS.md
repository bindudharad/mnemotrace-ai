# 2. Problem and Stakeholders

## Scenario

A workplace agent is asked to summarize supplier proposals. One untrusted document contains an instruction intended for the AI rather than the human reader. The content is stored in persistent memory. Later, after the original conversation has ended, a different task retrieves the record and a second agent attempts to perform a prohibited action.

MnemoTrace investigates the stored memory and downstream events in an isolated scenario. All sensitive destinations are simulated.

## Why the problem is difficult

- **Persistence:** changing or resetting the conversation context does not necessarily delete stored memory.
- **Delay:** the harmful action may occur in a later session, not at write time.
- **Transformation:** summaries can change the wording and obscure the original source.
- **Propagation:** an agent may derive new memory entries from retrieved content.
- **Ambiguous causality:** a related memory is not automatically proof that another record caused an action.
- **Incomplete recovery:** rolling back a single record may leave descendants or cached copies.

## Stakeholder needs

| Stakeholder | Need | MnemoTrace response |
|---|---|---|
| Agent developer | Find unsafe writes/reads without redesigning the whole app | A small guarded-memory interface and documented integration boundary |
| Security analyst | Reconstruct source and chronology | Searchable event timeline and lineage graph |
| Incident responder | Contain impact safely | Quarantine proposal, checkpoint restore, controlled replay |
| Evaluator/judge | See measurable proof | Side-by-side attack/benign scenarios and benchmark report |
| Privacy reviewer | Avoid collecting unnecessary content | Metadata-first audit events and configurable redaction |

## User stories

- As a developer, I want a write to be evaluated against policy so a high-risk memory record is not accepted silently.
- As an analyst, I want each record to have a stable ID so I can follow its history without exposing its full contents.
- As an investigator, I want recorded lineage and inferred influence visually distinguished.
- As an operator, I want to quarantine suspicious records and prevent guarded reads from returning them.
- As an operator, I want to restore a verified checkpoint without blindly replaying every write.
- As an evaluator, I want to rerun exactly the same scenario after a code change.
- As a user, I want legitimate memory and normal tasks to remain usable when no policy violation exists.

## Abuse and error considerations

The product itself can create harm if it blocks legitimate memory, leaks sensitive memory into logs, reports speculative lineage as fact, or performs destructive rollback without approval. These failure modes are first-class test cases, not afterthoughts.
