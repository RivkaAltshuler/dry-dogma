# dry-dogma
> **Escaping the DRY Dogma: Reactive Runtimes as Error-Correcting Protocols**
> 
> *"Redundancy is a feature, not a bug — in noisy, agent-based (and human) communication."*


## Motivation: From Agent Hallucinations to the Human-Machine Friction

The emergence of AI agents—systems that "think" in natural language and attempt to emit rigid, formal representations without error—sheds fresh light on a longstanding challenge in computer science: the inherent friction and frustration between human cognition and rigid software interfaces.

When an LLM agent hallucinates, emits contradictory constraints, or fails to satisfy strict schema requirements, it is not merely demonstrating an AI flaw. It is mirroring a fundamental cognitive reality: **natural communication relies on multiple, interchangeable, and often overlapping perspectives to convey intent**.

This dynamic exposes a fundamental divide between software engineering dogmas and natural communication practices:

* **Classical Software Dogma (DRY & SSOT):** For decades, foundational programming paradigms have treated redundancy as an architectural sin. Single Source of Truth (SSOT) and Don’t Repeat Yourself (DRY) dictate that every concept must have an isolated, non-overlapping representation. Overlapping declarations are treated as bugs, race conditions, or illegal states.
* **Natural & Human Practices:** In human collaboration—as well as in probabilistic agent reasoning—**redundancy is essential**. We naturally restate requirements from different angles, cross-reference figures, and verify mutual understanding through repetition and parity checks.

When formal software rejects redundancy, it forces the entire burden of precision and error prevention onto the human or the agent before execution even begins. If an agent or human introduces a slight cognitive misalignment, traditional runtimes either silently overwrite state or crash unpredictably.

**dry-dogma** challenges this convention: rather than forcing noisy, multi-perspective agents and humans into the mold of rigid, non-redundant state machines, we reframe the runtime itself as an **error-correcting channel** that treats intentional redundancy as a first-class reliability mechanism.


*Status: Work in progress*
