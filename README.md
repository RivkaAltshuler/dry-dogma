# Reactive Runtimes as Error-Correcting Protocols

*"Redundancy is a feature, not a bug — in noisy, agent-based (and human) communication."*

## Motivation

The emergence of AI agents—systems that reason in natural language while attempting to emit rigid, formal representations reliably—sheds fresh light on a longstanding challenge in computer science: the inherent friction between informal cognition and strict software interfaces.

## Observation

### Redundancy

A central tension between the two lies in how they handle repetition. Natural-language interaction is inherently redundant and ambiguous, whereas software engineering principles such as DRY (*Don't Repeat Yourself*) and code reuse treat redundancy as undesirable.

Yet these anti-redundancy principles originated as pragmatic heuristics for a specific human limitation: the difficulty of maintaining manual consistency across a codebase.

### Noisy Channel

Communication between the two constitutes a noisy channel in the classic information-theoretic sense. In information theory, reliable transmission across a noisy medium requires intentional redundancy—such as parity checks—paired with an error-correcting protocol to detect and resolve inconsistencies.

## Our Approach

Reactive programming can serve as a protocol for error detection and correction, analogous to error-correcting codes in information theory.

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

The `Merge` function is executed locally by each variable according to a predefined **merging policy** that governs whether incoming updates are accepted, flagged, or rejected. By evaluating overlapping assignments, these policies allow the reactive runtime to operate as an error-detection and correction protocol. We identify three distinct operational modes:

1. **Self-Check:** Incoming updates are accepted, override previous values, and propagate downstream. The updates are exposed back to the user or agent, enabling self-verification.
2. **Error Feedback:** When a variable receives conflicting values from distinct, overlapping assignments, it exposes an error.
3. **Rejection:** When an incoming update conflicts with existing active assignments, it is rejected. The variable retains its previous valid value, halts downstream propagation, and reports the rejection back to the source for correction.

## Applications

We explore the practical implications of this protocol through two applications currently under development: **Chatform** and **Langform**.

- **Chatform:** Exposes a reactive domain model via a **Model Context Protocol (MCP)** server, enabling an LLM to interact with structured business logic through partial or overlapping inputs while relying on the runtime for consistency checks and feedback.
- **Langform:** A **Domain-Specific Language (DSL)** designed with overlapping constructs and consistency validation. Implemented using **Langium**, it defines both the language syntax and a **Language Server Protocol (LSP)** backend that returns validation diagnostics and suggestions—supporting both human authors and LLM-generated code.

Both applications close the feedback loop with an LLM: Chatform through direct MCP tool calls, and Langform by feeding LSP validation responses back to the generating model.

## Foundations

- **Published Research:** *Escaping the DAG Dogma: Toward Modular Reactive Architectures* (Rivka Altshuler & David H. Lorenz) — **ACM SIGPLAN SPLASH / Onward! 2026**.

  📄 [Paper on ACM Digital Library](https://doi.org/10.1145/3840586.3843206)

- **Core Engine Repositories:** [RIVarX Organization](https://github.com/RIVarX) (implementations in C#, TypeScript, and JavaScript).