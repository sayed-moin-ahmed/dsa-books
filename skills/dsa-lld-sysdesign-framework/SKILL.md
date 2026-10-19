---
name: dsa-lld-sysdesign-framework
description: End-to-end framework that takes one problem through every layer — Problem → Computational Model → Data Model → Data Structure → Algorithm → Invariant/Proof → Complexity → Java → OOP → Design Pattern → Runtime Flow → LLD → Concurrency → Failure → Scale → System Design → Production → Adversarial Verdict. Use when the user wants the layers connected — "end to end", "from DSA to system design", "connect the data structure to the design pattern", "how does this become a production system", "full breakdown of LRU cache / rate limiter / scheduler", "LLD with the algorithm behind it", "walk this through every layer", or names this framework file. Also for evidence-tagged answers (SOURCE-SUPPORTED / DERIVED / INFERRED). Single-layer questions go to the specialist — dsa-pattern-practice, design-pattern-practice, or system-design-architect; this skill is the spine linking them.
---

# DSA → Design Pattern → LLD → System Design Execution Framework

The canonical source is attached verbatim at
`references/DSA_DesignPattern_LLD_SystemDesign_Execution_Framework.txt`.
Read it when you need the exact wording of a Part. This file is the working
summary. If the two ever disagree, the reference file wins.

## 🎯 Big idea

Data structures, algorithms, design patterns, LLD and system design are **one
pipeline**, not five subjects. Each layer is *derived* from the one above it.
You never pick a data structure or pattern first — you earn it from the
requirements.

```
 PROBLEM ─► COMPUTATIONAL MODEL ─► DATA MODEL ─► REQUIRED OPERATIONS
                                                        │
   ┌────────────────────────────────────────────────────┘
   ▼
 DATA STRUCTURE ─► ALGORITHM ─► INVARIANT ─► PROOF ─► COMPLEXITY
                                                        │
   ┌────────────────────────────────────────────────────┘
   ▼
 JAVA ─► OOP ─► DESIGN PATTERN ─► RUNTIME FLOW ─► LLD
                                                    │
   ┌────────────────────────────────────────────────┘
   ▼
 CONCURRENCY ─► FAILURE MODES ─► SCALABILITY ─► SYSTEM DESIGN
                                                    │
   ┌────────────────────────────────────────────────┘
   ▼
 PRODUCTION ARCHITECTURE ─► ADVERSARIAL VALIDATION ─► VERDICT
```

## Step 0 — Pick the depth (do this first)

The framework lists 17 Parts. Not every question needs all of them. Match
depth to the ask (this scaling rule is an adaptation, not in the source):

| Ask looks like | Run these Parts |
|---|---|
| "Solve / explain this algorithm problem" | I–VI, XVII |
| "Design class X / LLD for Y" | I, III, IV, VII–XI, XIII, XVII |
| "Which pattern fits / how does DS link to pattern" | IV, VIII, IX, X, XVII |
| "Take it end to end / to production" | All I–XVII |

Say which Parts you are skipping and why, in one line. Never skip XVII.

## Step 1 — Evidence pass (before any substantive answer)

```
 ATTACHMENTS / LIBRARY ─► RETRIEVE ─► CLASSIFY ─► PICK STRONGEST
        ─► CROSS-CHECK ─► ADVERSARIAL REVIEW ─► SYNTHESIZE ─► CITE ─► ANSWER
```

1. Look for relevant material first: project files, chat attachments, and the
   user's library at `~/Sayed/Books/` (use the `books-library` skill or
   `search_books.py`).
2. Never claim you read a source you did not actually open.
3. When the task is based on a source, keep its terms and framing. Do not
   silently fill gaps or "fix" the source.
4. If sources disagree, say so and say which is stronger and why.
5. If nothing supports a claim, write: **"The available sources do not
   establish this."**
6. Never invent citations, quotes, benchmarks, complexity claims, or pattern
   relationships.
7. Tag every load-bearing claim with one label:
   - `SOURCE-SUPPORTED FACT`
   - `DERIVED CONCLUSION`
   - `INFERENCE`
   - `ENGINEERING RECOMMENDATION`
   - `UNVERIFIED / UNSUPPORTED`
8. Keep external/web evidence visibly separate from library evidence.

## Step 2 — Walk the Parts

Short checklist per Part. Full bullet lists live in the reference file.

| Part | Question it answers | Must produce |
|---|---|---|
| I Problem | What are we solving? | Functional + non-functional reqs, constraints, input sizes |
| II Computational model | What must be fast? | Dominant ops, read/write mix, sequential/concurrent/distributed/streaming, target Big-O |
| III Data model | What state exists? | Entities, relationships, what is ordered/indexed/searched/deduped → **required operations** |
| IV Data structure | What fits those ops? | Why it fits, core invariant, ops + time/space, alternatives and why they lose |
| V Algorithm | How do we compute it? | Recognition signal, steps, invariant, correctness proof, complexity, edge cases, lower-bound argument |
| VI Java | How do we write it well? | Interfaces, generics, immutability, equals/hashCode, null + exception policy, thread safety, pitfalls named |
| VII OOP | Who owns what? | Responsibilities, abstractions, collaborators, composition vs inheritance, extension points |
| VIII DS ↔ Pattern | Is there a natural link? | Only links that the problem justifies (map below) |
| IX Pattern analysis | Does the pattern earn its keep? | Intent, participants, runtime behavior, life without it, cost, when NOT to use, simpler option |
| X Runtime flow | What actually happens? | Request → API → service → abstraction → pattern → DS → algorithm → store → response, with mutation/sync/error points |
| XI LLD | What are the classes? | Use cases → domain objects → interfaces → relationships → sequence → edge cases → extension points |
| XII Concurrency | What breaks with threads? | Shared state, atomicity, visibility, ordering, races, deadlock, lock granularity, idempotency, backpressure |
| XIII Failure modes | What breaks with bad input/infra? | Empty/boundary/huge/duplicate input, stale state, partial failure, timeout, retry, dependency/network failure, corruption |
| XIV Scalability | Where is the bottleneck? | Walk method → object → JVM → threads → instances → distributed → prod; at each: latency, memory, CPU, network, contention, consistency, node loss |
| XV System design | How does it become a service? | API, persistence, cache, messaging, partitioning, replication, consistency, idempotency, rate limit, observability, security, DR |
| XVI Productionization | Is it ready to run? | Perf, reliability, availability, security, observability, testability, operability, cost. No premature optimization |
| XVII Adversarial | Is it actually right? | The 18 attack questions + verdict block (below) |

### Part VIII — data structure ↔ pattern map

These are **conceptual links, not one-to-one rules**. Check each against the
real problem. If no pattern emerges naturally, say so.

```
 ARRAY ─────────── Iterator · Strategy · Command
 LINKED STRUCTURE ─ Iterator · Chain of Responsibility · Decorator
 STACK ─────────── Command · Memento · Undo/Redo · Interpreter
 QUEUE ─────────── Command · Producer/Consumer · Scheduler · Message processing
 HASH MAP ──────── Registry · Factory · Flyweight · Cache · Proxy · State transition table
 HEAP / PQ ─────── Priority scheduling · Scheduling policies
 TREE ──────────── Composite · Iterator · Visitor · Interpreter · AST
 GRAPH ─────────── State machine · Visitor · Mediator · Workflow · Dependency graph
 HASH MAP + DLL ── LRU cache  (O(1) average get / put / evict)
```

## Step 3 — Adversarial validation (never skip)

Attack the answer before you send it:

1. Is the data structure really the best fit for this workload?
2. Is the algorithm correct? Can I build a counterexample?
3. Does the invariant hold after **every** operation?
4. Is the Big-O right? Is there a hidden O(n) step or a wasted allocation?
5. Is there a simpler, lower-memory, or asymptotically better solution?
6. Does the pattern solve a real problem, or is it decoration?
7. What happens under concurrency? Under failure? At 10×, 100×, 1000×?
8. Which assumption is most likely to fail?
9. What evidence backs each conclusion? Which claims are only inferred?

Close with this block, filled in:

```
VERDICT
-------
Correct / Mostly Correct / Needs Revision
Confidence: High / Medium / Low
Evidence:   Source-supported / Derived / Inferred / Unverified
Main Risk:  <the single weakest point, and what would prove it wrong>
```

## Worked reference — LRU cache through every layer

```
 "Keep recently used items"            ← business need
        │
 get(key), put(key,val) at O(1)        ← required ops + target
        │
 HashMap<K,Node> + doubly linked list  ← data structure
        │
 move-to-front on hit, evict tail      ← algorithm
        │
 INVARIANT: map and list hold the same keys; list order = recency
        │
 Cache<K,V> interface + LruCache impl  ← Java / OOP
        │
 Strategy: swappable EvictionPolicy    ← pattern that earns its place
 Decorator/Proxy: CachingService wraps the repository
        │
 Request → Service → Cache → (miss) DB → fill cache → Response
        │
 Concurrency: lock or ConcurrentHashMap + striped locks; failure: stampede, stale data
        │
 Scale out: distributed cache (Redis / cache cluster)
        │
 Production: TTL, eviction policy, consistency with DB, failure handling, hit-rate metrics
```

## Rules that override completeness

- Correctness and evidence beat completeness. If the sources do not establish
  it, state the gap — do not manufacture an answer.
- If no design pattern emerges naturally, say so.
- If a better data structure or algorithm exists, challenge the first idea.
- If production needs (distribution, persistence) break the original
  algorithm's assumptions, explain the change.
- Default language is **Java** unless the user asks for another.
- Optimize for: **correctness + evidence + explainability + scalability +
  practical engineering value.**

## Hand-offs

- Deep algorithm drill / STIC card → `dsa-pattern-practice`
- Spotting GoF patterns in existing code → `design-pattern-practice`
- Architecture-only questions, ADRs, SADP cards → `system-design-architect`
- Finding book evidence → `books-library`
