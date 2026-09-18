# agents.md

## what this repository is

trainery is a research project investigating whether ai agents can learn new programming environments more efficiently by transferring structured knowledge from environments they already know.

this repository is research software.

it is not primarily a product, demo, chatbot, or generic coding-agent framework.

when making changes, preserve the ability to run controlled experiments.

---

## core research principle

the central distinction is:

```text
existing knowledge
        ↓
transferable knowledge
        ↓
target-specific knowledge
```

the system should not treat every target concept as completely new if the agent already has a useful prior.

however, it must also not assume that two concepts are equivalent simply because they look similar.

---

## analogy is not equivalence

never encode an analogy as an identity unless there is evidence that the two concepts actually behave identically.

for example:

```text
react component
```

and

```text
openscad module
```

may share properties such as:

* reusable abstraction
* parameterization
* composition

but they have very different semantics.

the graph should therefore represent the relationship and its limitations.

prefer relationships such as:

```text
analogous_to
partial_analogy
generalizes
specializes
implements
composes
depends_on
contrasts_with
```

over vague:

```text
similar_to
```

when more precise semantics are available.

---

## source environments vs target environments

source environments are environments whose knowledge is treated as existing prior knowledge for an experiment.

initial sources:

```text
react
vite
python
```

initial targets:

```text
p5.js
three.js
kaboom.js
openscad
cadquery
```

do not blur these categories.

a target can later become a source for cumulative-transfer experiments, but that transition should be explicit in the experiment configuration.

---

## do not assume model knowledge

the experiment may use react, vite, or python as source environments because coding models are expected to have substantial knowledge of them.

that expectation is not experimental evidence.

when possible, measure source proficiency.

record:

* model/version
* evaluation set
* source tasks
* score
* execution success
* relevant failure modes

a transfer experiment should not silently become:

```text
model didn't know the source environment
        ↓
transfer failed
```

without identifying the problem.

---

## knowledge graph

the graph is a research artifact, not merely a retrieval index.

nodes may represent:

* concepts
* languages
* frameworks
* libraries
* apis
* operations
* abstractions
* domains
* examples
* tasks
* constraints
* environments

edges should have explicit semantics.

where possible, relationships should include:

* provenance
* evidence
* confidence
* shared properties
* differences
* examples
* known failure cases

never create large numbers of inferred edges without preserving how they were produced.

---

## graph vs vector search

vector search and graph traversal have different jobs.

vector search is useful for semantic retrieval and candidate discovery.

the graph is useful for explicit relationships and multi-hop reasoning.

do not treat:

```text
high vector similarity
```

as equivalent to:

```text
validated transfer relationship
```

the distinction matters to the validity of the research.

---

## ingestion

documentation ingestion must preserve provenance.

for every extracted piece of knowledge, try to retain:

```text
source
url
environment
version
retrieval date
document type
extraction method
```

when source versions matter, record them.

do not silently mix incompatible versions of an api into one knowledge representation.

---

## curriculum generation

curriculum generation should explicitly distinguish:

```text
known
transferable
target-specific
novel
```

a curriculum should not repeatedly teach concepts that have already been established as mastered unless the experiment specifically requires rehearsal.

transfer paths should be inspectable.

if the system produces:

```text
react component
    ↓
openscad module
```

the researcher should be able to inspect why that edge was created and what evidence supports it.

---

## experiments

every experiment should record enough information to reproduce or understand it.

at minimum:

```text
experiment id
date
model
model version
source environment(s)
target environment
training condition
dataset/version
training configuration
compute budget
evaluation set
evaluation configuration
results
notes
failures
```

do not silently modify an experiment's dataset or evaluation after seeing results.

if a benchmark changes, create a new version.

---

## baselines

the basic experiment family contains:

### target-only

```text
target data
```

### source + target

```text
source data
+
target data
```

### transfer-aware

```text
source knowledge
+
transfer graph
+
target data
```

the experiment should make it possible to distinguish the effect of transfer structure from the effect of simply receiving additional data.

---

## evaluation

prefer executable evaluation wherever practical.

for programming environments:

```text
generate
  ↓
execute
  ↓
observe
  ↓
evaluate
```

do not rely solely on:

```text
generated code
  ↓
llm says it looks correct
```

for visual environments, evaluate behavior rather than only source-code similarity.

for cad environments, evaluate resulting geometry.

---

## cad evaluation

cadquery and openscad should not be evaluated primarily through textual code similarity.

equivalent geometry can be produced by different programs.

evaluation may include:

* compilation
* successful rendering
* dimensions
* topology
* boolean operations
* feature presence
* spatial relationships
* constraints

when possible, compare artifacts rather than representations.

---

## graphics and games evaluation

for p5.js, three.js, and kaboom.js, evaluation should include execution and behavioral checks.

examples:

```text
does the application start?

does the requested object exist?

does it move?

does interaction work?

does state change correctly?

does the generated program handle an unseen specification?
```

for kaboom.js specifically, evaluation can cover:

```text
scenes
sprites
movement
controls
collisions
state
score
enemies
interactions
modification
novel game generation
```

---

## cumulative transfer

a target environment can become a later source.

example:

```text
react + vite + python
          ↓
        p5.js
          ↓
     learned p5.js
          ↓
      kaboom.js
```

when running this experiment, distinguish:

```text
fresh source knowledge
```

from:

```text
knowledge acquired during a previous experiment
```

the latter is the important condition.

---

## training backend

training infrastructure must remain separate from research logic.

trainium-specific implementation belongs under:

```text
training/trainium/
```

do not make the knowledge graph, curriculum system, or evaluation framework depend directly on trainium.

the same experiment should ideally be runnable using another backend.

trainium is an experimental compute backend.

---

## fixed compute

when an experiment is intended to compare training efficiency, keep compute budgets controlled.

record:

* hardware
* training time
* steps
* batch configuration
* relevant optimizer configuration
* model configuration
* data volume

do not increase compute for one condition after seeing that it performs poorly unless the experiment explicitly studies compute scaling.

---

## infrastructure adapters

external services should be isolated behind small interfaces.

possible services include:

```text
firecrawl
tavily
falkordb
e2b
browserbase
nebius
backboard
trainium
```

research logic should not become tightly coupled to provider-specific APIs.

this also makes experiments easier to reproduce.

---

## provenance

research data should be traceable.

for knowledge:

```text
where did this fact come from?
```

for transfer edges:

```text
why does this relationship exist?
```

for training data:

```text
what version of the dataset was used?
```

for results:

```text
what exact configuration produced this result?
```

if an answer cannot be traced, mark it as inferred or uncertain rather than presenting it as established fact.

---

## failed transfer is a valid result

do not automatically fix a failed transfer relationship because the system expected it to work.

failed transfer may reveal:

* superficial similarity
* missing target semantics
* incompatible abstractions
* domain-specific assumptions
* incorrect graph edges
* insufficient source proficiency
* insufficient target data

the failure itself can be part of the result.

---

## coding style

prefer boring, inspectable implementations over clever abstractions.

research code should be easy to instrument.

avoid hiding important experimental behavior behind opaque helper functions.

configuration should be explicit.

results should be serializable.

random seeds should be recorded where relevant.

---

## documentation

keep research reasoning separate from implementation documentation.

use:

```text
research/
```

for methodology and experimental design.

use:

```text
journal.md
```

for chronological notes, observations, weird failures, ideas, and dead ends.

use code comments for implementation details.

do not turn the README into a changelog.

---

## current priority order

unless a specific experiment requires otherwise, the intended development order is:

```text
1. research specification
2. methodology
3. experiment matrix
4. data ingestion
5. knowledge representation
6. graph
7. transfer relationships
8. curriculum generation
9. execution harness
10. evaluation
11. target-only baseline
12. source + target baseline
13. first transfer experiment
14. analysis
15. trainium implementation
16. fixed-budget experiments
17. cumulative transfer
```

do not jump directly to model training before the evaluation framework exists.

a model that improves without a reliable evaluation harness does not tell us much.

---

## what not to optimize for

do not prioritize:

* landing-page polish
* flashy demos
* arbitrary benchmark scores
* huge graphs
* maximum number of relationships
* maximum retrieval volume
* model size for its own sake
* provider-specific optimization without evidence
* premature custom kernels

the research question comes first.

---

## final rule

when making a change, ask:

> does this make the experiment more understandable, reproducible, measurable, or useful?

if not, it may not belong in the research core.
