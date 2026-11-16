# Reactive Runtimes as Error-Correcting Protocols

*"Redundancy is a feature, not a bug — in noisy, agent-based (and human) communication."*

## Motivation

The emergence of AI agents—systems that "think" in natural language and attempt to emit rigid, formal representations without error—sheds fresh light on a longstanding challenge in computer science: the inherent friction and frustration between human cognition and rigid software interfaces.

When an LLM agent hallucinates, emits contradictory constraints, or fails to satisfy strict schema requirements, it is not merely demonstrating an AI flaw. It is mirroring a fundamental cognitive reality: **natural communication relies on multiple, interchangeable, and often overlapping perspectives to convey intent**.

This dynamic exposes a fundamental divide between software engineering dogmas and natural communication practices:

- **Classical Software Dogma (DRY & SSOT):** For decades, foundational programming paradigms have treated redundancy as an architectural sin. Single Source of Truth (SSOT) and Don’t Repeat Yourself (DRY) dictate that every concept must have an isolated, non-overlapping representation. Overlapping declarations are treated as bugs, race conditions, or illegal states.
- **Natural & Human Practices:** In human collaboration—as well as in probabilistic agent reasoning—**redundancy is essential**. We naturally restate requirements from different angles, cross-reference figures, and verify mutual understanding through repetition and parity checks.

## Our Approach

### 1. Escape DRY
Principles such as DRY (*Don't Repeat Yourself*) and code reuse principle have long been treated as universal virtues. In practice, they originated as practical heuristics to address a human limitation: the difficulty of maintaining manual consistency across codebases. 

### 2. Noisy Channel
Communication between natural-language systems (whether humans or generative AI agents) and formal software interfaces constitutes a **noisy communication channel** in the classic information-theoretic sense. 

### 3. Reactive Programming for Error-Correcting Protocols
Handling the noisy channel should be approached similarly to information theory.

In information theory, reliable transmission across a noisy medium requires intentional redundancy (such as parity bits and checksums) paired with an error-correcting protocol. 

Likewise, reactive programming can be adressed to make an error detection and correction protocol.


## Implementation Strategy


### Constructive Assignment
Constructive assignment is a semantic model in reactive programming where variables can have several active assignments simultaneously. For example:

```text
Drug := Concentration * Volume
Drug := Dose * Duration
```

This model handles variables and expressions as streams of values. In each assignment, the left-hand variable subscribes to the expression and receives its updates. With several active assignments, updates from their expressions are `merged` into the same variable. 

```text
Drug = Merge([updates from Concentration * Volume], [updates from Dose * Duration])
```

To visualize the mechanism, see [this interactive animation](https://rivkaaltshuler.github.io/dry-dogma/html-animations/constructive-assignment-proportional-timeline-slides.html).

### The Protocol

The `Merge` function is executed locally by each variable according to a predefined **merging policy** that governs whether incoming updates are committed, flagged, or rejected. By evaluating overlapping constraints, these policies transform the reactive runtime into an error-detection and correction protocol. We identify three distinct operational modes:

1. **Self-Check (Normal Propagation):** In the absence of conflicts, variables seamlessly ingest updates, where older states are naturally overridden by new inputs. The runtime utilizes this redundant data flow to dispatch automated telemetry and parity notifications back to the user or agent, facilitating continuous self-monitoring.
2. **Parity Check (Conflict Signaling):** When a variable receives conflicting values from distinct, overlapping assignments, the system detects a semantic misalignment. Instead of silently overwriting state, the variable flags a *parity violation*. The variable moves into an error state, retaining both the discrepancy metrics and the conflicting bounds to pinpoint exactly where the cognitive drift between the human/agent intent and the domain logic occurred.
3. **Rejection (Strict Invalidation):** If an incoming update introduces an unresolvable contradiction that violates core system invariants, the merging policy denies the transaction. The runtime halts execution down that specific branch, discards the conflicting input sequentially through the standard execution stack, and throws a formal validation exception to force immediate correction at the source.

## Applications (Under Development)

For real world evaluation we think about two applications: Chatform and Langform.

- **Chatform:** Reactive Domain Models for LLM Interaction. Chatform reimagines how Generative AI interacts with structured business logic, exposing the reactive domain model via a **Model Context Protocol (MCP)** server.

- **LangForm:** Domain Specific Language designed with overlapping data with the tooling to handle the consistency. We find Langium as the correct tool as it provides the framework to both declare the syntax and Language Server Protocol that is used to provide suggestions and errors to the user. 

  Both applications are designed to interact with LLMs. Chatform integrates via the MCP protocol. For Langform, an LLM generates the code, and the LSP feeds validation responses back to the LLM.


## Foundations

- **Published Research:** *Escaping the DAG Dogma: Toward Modular Reactive Architectures* (Rivka Altshuler & David H. Lorenz) — **ACM SIGPLAN SPLASH / Onward! 2026**.

  📄 [Paper on ACM Digital Library](https://doi.org/10.1145/3840586.3843206)

- **Core Engine Repositories:** [RIVarX Organization](https://github.com/RIVarX) (implementations in C#, TypeScript, and JavaScript).
