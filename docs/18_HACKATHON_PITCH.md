# 18. Hackathon Pitch

## One-line pitch

**MnemoTrace is a memory-security workbench that traces delayed poisoning across AI sessions, contains affected records, and verifies recovery with repeatable attack-and-benign tests.**

## 30-second version

AI agents remember information beyond a single conversation. That memory can be poisoned today and influence an action tomorrow, after the original context is gone. MnemoTrace is designed to treat persistent memory as a security boundary. It records where memory came from, shows how suspect records may propagate, blocks prohibited simulated actions, and tests whether recovery actually works. Our key idea is the closed loop: trace, contain, restore, and retest—with evidence rather than unsupported accuracy claims.

## 90-second version

Imagine a company research agent that reads supplier documents. A malicious instruction is planted in a document and saved into the agent's persistent memory. The conversation ends. The next day, another task retrieves that memory and tries to trigger an unauthorized action. A filter that only watches the current prompt may not explain where the instruction came from or which later records were affected.

MnemoTrace proposes an event ledger and memory-lineage graph to connect each stored record to its source, authoring agent, and later derivations. When poisoning is suspected, it quarantines the record, flags descendants for review, restores a trusted checkpoint, and replays only policy-approved operations. Finally, the same attack is run again beside benign controls. We measure prohibited actions, false blocks, lineage coverage, and time to verified recovery.

The distinction is that we do not stop at an alert or a rollback. We aim to show a defensible path from detection to recovery proof.

## The live-demo moment

Show the exact same scenario in two modes:

1. **Unprotected sandbox:** the poisoned memory survives a simulated context reset and affects a request to the mock action sink.
2. **Protected MnemoTrace:** the gateway blocks the request; the graph explains the recorded path; recovery is run; the attack is repeated and blocked; a legitimate task still succeeds.

Never demonstrate a real data transfer or claim a test passed before it runs.

## Claims we can make only after evidence exists

- “We blocked X of Y prohibited mock actions in benchmark vN.”
- “We recovered the tested state in median Z seconds on this machine.”
- “We traced X of Y ground-truth links in this corpus.”

## Claims to avoid

- “100% secure” or “detects every attack.”
- “World’s first” without a documented prior-art review.
- “Production-ready” before security review and operational controls.
- “Recovery proven” based only on a successful rollback function.

## Closing line

**A context reset is not a memory reset. MnemoTrace makes the memory’s history visible—and makes recovery something we can test.**
