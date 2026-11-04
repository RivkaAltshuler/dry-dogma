# Escaping the DRY Dogma: Reactive Runtimes as Error-Correcting Protocols

> *"Redundancy is a feature, not a bug — in noisy, agent-based (and human) communication."*

## Motivation: From Agent Hallucinations to Human-Machine Friction

The emergence of AI agents—systems that "think" in natural language and attempt to emit rigid, formal representations without error—sheds fresh light on a longstanding challenge in computer science: the inherent friction and frustration between human cognition and rigid software interfaces.

When an LLM agent hallucinates, emits contradictory constraints, or fails to satisfy strict schema requirements, it is not merely demonstrating an AI flaw. It is mirroring a fundamental cognitive reality: **natural communication relies on multiple, interchangeable, and often overlapping perspectives to convey intent**.

This dynamic exposes a fundamental divide between software engineering dogmas and natural communication practices:

- **Classical Software Dogma (DRY & SSOT):** For decades, foundational programming paradigms have treated redundancy as an architectural sin. Single Source of Truth (SSOT) and Don’t Repeat Yourself (DRY) dictate that every concept must have an isolated, non-overlapping representation. Overlapping declarations are treated as bugs, race conditions, or illegal states.
- **Natural & Human Practices:** In human collaboration—as well as in probabilistic agent reasoning—**redundancy is essential**. We naturally restate requirements from different angles, cross-reference figures, and verify mutual understanding through repetition and parity checks.

When formal software rejects redundancy, it forces the entire burden of precision and error prevention onto the human or the agent before execution even begins. If an agent or human introduces a slight cognitive misalignment, traditional runtimes either silently overwrite state or crash unpredictably.

**dry-dogma** challenges this convention: rather than forcing noisy, multi-perspective agents and humans into the mold of rigid, non-redundant state machines, we reframe the runtime itself as an **error-correcting channel** that treats intentional redundancy as a first-class reliability mechanism.

## Our Approach: From Historical Constraints to Error-Correcting Channels

### 1. DRY and Low Coupling as Tooling-Imposed Constraints
Principles such as DRY (*Don't Repeat Yourself*), code reuse, and loose coupling have long been treated as universal virtues. In practice, they originated as practical heuristics to address a human limitation: the difficulty of maintaining manual consistency across codebases. 

Developers minimize duplication primarily to ensure that modifications can be made safely in a single location without manual synchronization errors. In the absence of runtime mechanisms capable of synchronizing overlapping representations automatically, eliminating redundancy was the only viable strategy. When runtime tooling can maintain semantic consistency across representations, redundancy ceases to be a liability.

### 2. Human/Agent-Software Interaction as a Noisy Channel
Communication between natural-language systems (whether humans or generative AI agents) and formal software interfaces constitutes a **noisy communication channel** in the classic information-theoretic sense. 

In information theory, reliable transmission across a noisy medium requires intentional redundancy (such as parity bits and checksums) paired with an error-correcting protocol. Applying this principle to software architecture, intentional redundancy provides the overlapping signals necessary to detect misunderstandings, trace semantic drift, and guide automated recovery.

### 3. Reactive Programming for Error-Correcting Protocols
The reactive programming paradigm provides high-level abstractions to declare data dependencies with automatic consistency. This framework can be utilized to build protocols that detect and resolve errors, effectively cleaning the communication channel—inspired by error correction mechanisms in network communication.

## Enabling the Protocol: Constructive Assignment

### Brief for Constructive Assignment
Constructive assignment is a semantic model where variables can have several active assignments simultaneously. For example:

```text
Drug := Concentration * Volume
Drug := Dose * Duration
```

This model handles variables and expressions as streams of values. In each assignment, the left-hand variable subscribes to the expression so that it propagates updates to it. Having several active assignments causes the variable to receive updates from multiple expressions, applying the classic merge operation over streams.

```text
Drug = Merge([updates from Concentration * Volume], [updates from Dose * Duration])
```

**Visual walkthrough:** [Follow the interactive timeline](https://rivkaaltshuler.github.io/dry-dogma/html-animations/constructive-assignment-proportional-timeline-slides.html) alongside this explanation. It shows how inputs arrive over time and how multiple active assignments can send updates to the same variable.

### The Protocol

The merge function is executed locally by the variables, according to a *merging policy*. Basically, whenever a variable has an incoming update message it may accept or discard it. We identify three like *policies* to function as an error-detection and correction protocol:

1. **Self Check (Normal Propagation):** Silently receiving updates where older values are naturally overridden by new input. Redundant data and notifications sent to the user upon updates also assist with self-monitoring.
2. **Parity Check:** In cases where a variable receives conflicting values from distinct assignments, the accepted value holds an error.
3. **Rejection:** Rejecting input if it causes conflicts. Updates are processed sequentially through standard execution stacks. Therefore a discard may be executed throwing an exception.

## Future Horizons: Chatform, Lanform, and Beyond

To bring these principles into practical engineering domains, our ongoing work focuses on realizing error-correcting reactive runtimes through two upcoming application paradigms:

- **Chatform:** Building domain-driven models based on constructive assignment frameworks. Creating an MCP (Model Context Protocol) server that exposes the model. The server recognizes variables updated by the prompt and returns messages detailing cascading updates or rejections. Finally, testing and comparing interactions with and without model redundancy.


- **LangForm:** Developing a Domain-Specific Language (DSL) that easily defines mutually dependent tokens, supported by a Language Server Protocol (LSP) implementation that enforces the protocol principles. Evaluated using IDE environments (such as Cursor or Windsurf) to test LLM code generation interacting in real-time with the LSP server. 

We invite researchers, developers, and practitioners interested in reimagining software reliability and human-agent interaction to explore our repositories, collaborate on our open-source tools, and join us in moving beyond the DRY dogma.

## Foundations

- **Published Research:** *Escaping the DAG Dogma: Toward Modular Reactive Architectures* (Rivka Altshuler & David H. Lorenz) — **ACM SIGPLAN SPLASH / Onward! 2026**.

  📄 [Paper on ACM Digital Library](https://doi.org/10.1145/3840586.3843206)

- **Core Engine Repositories:** [RIVarX Organization](https://github.com/RIVarX) (implementations in C#, TypeScript, and JavaScript).
