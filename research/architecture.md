# architecture

trainery is organized as a set of research layers rather than one monolithic application.

```text
                    ┌─────────────────────┐
                    │    environments     │
                    │ react / vite / etc.  │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │      ingestion      │
                    │ docs / examples /   │
                    │ references / source │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │ knowledge extraction│
                    │ concepts / APIs /   │
                    │ operations / tasks  │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │  knowledge graph   │
                    │ concepts + edges    │
                    └──────────┬──────────┘
                               │
                  ┌────────────┴────────────┐
                  │                         │
                  ▼                         ▼
         ┌─────────────────┐       ┌─────────────────┐
         │ vector retrieval│       │ graph traversal │
         └────────┬────────┘       └────────┬────────┘
                  │                         │
                  └────────────┬────────────┘
                               ▼
                    ┌─────────────────────┐
                    │ transfer analysis   │
                    │ what transfers?     │
                    │ what does not?      │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │ curriculum builder  │
                    │ known → missing →   │
                    │ target-specific     │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │      training       │
                    │ baseline / transfer │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │      execution      │
                    │ sandbox / browser   │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │     evaluation      │
                    │ behavior / artifact │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │       results       │
                    │ metrics / failures  │
                    │ transfer evidence   │
                    └─────────────────────┘
```

---

## layer 1 — environments

these are the programming environments being studied.

source:

```text
react
vite
python
```

targets:

```text
p5.js
three.js
kaboom.js
openscad
cadquery
```

---

## layer 2 — ingestion

collect:

* documentation
* examples
* api references
* tutorials
* source code
* task specifications

everything should be versioned or timestamped where relevant.

---

## layer 3 — knowledge extraction

convert raw documents into structured knowledge.

possible extracted objects:

```text
concept
api
function
operation
constraint
example
task
environment
relationship
```

---

## layer 4 — knowledge graph

connect those objects.

the graph is where trainery represents the structure of the programming knowledge.

---

## layer 5 — transfer

identify relationships between source and target concepts.

the transfer layer should produce:

```text
candidate transfer
confidence
evidence
shared properties
differences
```

---

## layer 6 — curriculum

construct a learning sequence.

the curriculum should prioritize target-specific gaps while using established transferable knowledge as a prior.

---

## layer 7 — training

train or adapt the agent under controlled experimental conditions.

the training backend should be replaceable.

---

## layer 8 — execution

run generated programs.

execution is necessary because code that looks correct is not necessarily correct.

---

## layer 9 — evaluation

measure:

* execution
* behavior
* semantics
* modification
* debugging
* generalization
* artifact correctness

---

## layer 10 — results

store results in a form that allows experiments to be compared later.

results should include enough metadata to understand what produced them.
