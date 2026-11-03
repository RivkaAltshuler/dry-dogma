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

## Our Approach: From Historical Constraints to Error-Correcting Channels

### 1. DRY and Low Coupling as Tooling-Imposed Constraints
Principles such as DRY (*Don't Repeat Yourself*), code reuse, and loose coupling have long been treated as universal virtues. In practice, they originated as practical heuristics to address a human limitation: the difficulty of maintaining manual consistency across codebases. 

Developers minimize duplication primarily to ensure that modifications can be made safely in a single location without manual synchronization errors. In the absence of runtime mechanisms capable of synchronizing overlapping representations automatically, eliminating redundancy was the only viable strategy. When runtime tooling can maintain semantic consistency across representations, redundancy ceases to be a liability.

### 2. Human/Agent-Software Interaction as a Noisy Channel
Communication between natural-language systems (whether humans or generative AI agents) and formal software interfaces constitutes a **noisy communication channel** in the classic information-theoretic sense. 

In information theory, reliable transmission across a noisy medium requires intentional redundancy (such as parity bits and checksums) paired with an error-correcting protocol. Applying this principle to software architecture, intentional redundancy provides the overlapping signals necessary to detect misunderstandings, trace semantic drift, and guide automated recovery.

### 3. Intentional Redundancy via the RIVar Computational Model
To operationalize error-correcting channels without falling into the traps of traditional paradigms, we leverage the **RIVar** computational model:

* **Beyond Traditional FRP (Cycle-Safe Invariant Dependencies):** Conventional Functional Reactive Programming mandates Directed Acyclic Graphs (DAGs) and single-assignment semantics. RIVar's constructive assignment natively accommodates multi-directional, cyclic dependencies and evaluates conflicting specifications deterministically rather than terminating the reactive stream.
* **Beyond Classical Constraint Solvers (Event-Driven Merge Policies):** While constraint satisfaction systems solve global equations, they often function as monolithic, batch-oriented solvers that obscure local state transitions. RIVar operates over decentralized reactive event streams, enabling flexible, localized **merge strategies** that can dynamically evaluate conflicts and negotiate resolutions directly with the user or agent.

This mechanism powers three deterministic operational modes:
1. **Propagation (Partial Specification):** Derives missing state across interdependent relationships when a partial update is provided.
2. **Parity Verification (Redundant Specification):** Evaluates overlapping inputs against domain invariants, confirming convergence when specifications align.
3. **Structured Rejection & Self-Healing (Conflict Detection):** Isolates contradictory constraints without discarding existing state, returning an actionable diagnostic explanation to the user or agent for resolution.

## Foundations

* **Published Research:** *Escaping the DAG Dogma: Toward Modular Reactive Architectures* (Rivka Altshuler & David H. Lorenz) — **ACM SIGPLAN SPLASH / Onward! 2026**.

  📄 [Paper on ACM Digital Library](https://doi.org/10.1145/3840586.3843206)

* **Core Engine Repositories:** [RIVarX Organization](https://github.com/RIVarX) (implementations in C#, TypeScript, and JavaScript).

