# trainery

trainery is a research project about teaching ai agents new programming environments by transferring knowledge they already have.

the basic idea is pretty simple:

> if an agent already knows how programming concepts work, does it really need to learn every new programming environment from scratch?

an agent that already understands functions, parameters, iteration, composition, abstraction, modules, transformations, coordinate systems, declarative construction, state, events, and other programming concepts should have useful prior knowledge when it encounters a new environment.

the problem is that existing training approaches often treat the target environment as a mostly independent learning problem.

trainery experiments with making the relationship between environments explicit.

instead of:

```text
model
  ↓
target documentation
  ↓
target examples
  ↓
learn target
```

trainery is interested in:

```text
model's existing knowledge
          ↓
   conceptual graph
          ↓
what transfers / what doesn't
          ↓
target-specific knowledge
          ↓
     curriculum
          ↓
      training
          ↓
      evaluation
```

the goal is not to make an ai explain analogies to a human.

the goal is to find out whether structured knowledge about relationships between programming environments can actually make an ai agent better at acquiring a new one.

---

## what are we trying to find out?

the central research question is:

> can an ai agent acquire proficiency in a new programming environment more efficiently when training is informed by structured knowledge of concepts it already understands?

there are several parts to this.

### 1. can knowledge transfer?

if an agent already understands something like:

```text
function
parameter
composition
iteration
state
event
transformation
module
abstraction
coordinate system
```

can those concepts act as useful priors when learning a new environment?

### 2. does structured transfer work better than simply adding more data?

this is important.

if we give a model source material plus target material and it performs better, that doesn't necessarily mean the conceptual graph helped.

the experiment therefore needs to separate:

```text
target-only learning

source + target learning

transfer-aware learning
```

so that we can measure whether the explicit transfer mechanism contributes something beyond additional training data.

### 3. can learning compound?

the longer-term hypothesis is more interesting.

suppose an agent knows:

```text
react
vite
python
```

and learns:

```text
p5.js
```

does that newly acquired p5.js knowledge become useful when it later learns:

```text
kaboom.js
```

?

in other words:

```text
react + vite + python
          ↓
        p5.js
          ↓
   acquired knowledge
          ↓
       kaboom.js
```

if this works, learning could become cumulative instead of repeatedly starting from zero.

---

## what trainery is not

trainery is not primarily:

* a coding chatbot
* a documentation chatbot
* a generic rag system
* a vector database wrapper
* an autocomplete system
* a prompt engineering framework
* a benchmark that only measures syntax
* an analogy generator for humans

retrieval is useful.

documentation is useful.

vector search is useful.

fine-tuning is useful.

but none of those things alone answer the research question.

the target is **capability acquisition**.

we want to know whether an agent can become competent in a new environment faster, with less target-specific information, or with better generalization because it can use knowledge it already possesses.

---

## initial source environments

the initial source environments are:

* react
* vite
* python

these are deliberately chosen as environments where modern coding agents are likely to have substantial existing knowledge.

however, trainery should not simply assume that the model knows them.

where possible, source proficiency should be measured.

the experiment should distinguish between:

```text
knowledge the model actually has

knowledge the training pipeline assumes it has
```

because otherwise a failed transfer experiment could simply be a failed source-knowledge assumption.

---

## target environments

the initial target environments are deliberately different.

### p5.js

p5.js gives us a javascript → javascript transfer condition.

the language itself is familiar, but the programming environment and domain are different.

the agent has to learn things such as:

* setup and draw
* canvas state
* rendering
* interaction
* animation
* coordinate systems
* visual transformations
* event handling
* creative coding patterns

this lets us ask whether conceptual transfer works even when the target language syntax is already familiar.

---

### three.js

three.js provides another javascript → javascript condition, but with a substantially different programming model.

the agent has to reason about things such as:

* scenes
* cameras
* renderers
* meshes
* materials
* geometry
* transforms
* lighting
* animation
* object hierarchies
* 3d coordinates

this makes three.js useful for testing transfer into a new representation and domain rather than merely testing syntax acquisition.

---

### kaboom.js

kaboom.js is another javascript → javascript target, but focused on game development.

it gives us another specialized environment where the underlying language is familiar while the environment introduces new concepts and APIs.

possible evaluation areas include:

* scenes
* sprites
* movement
* controls
* collisions
* enemies
* score/state
* interactions
* game loops
* modifying existing games
* building a novel game from a specification

kaboom.js is especially interesting for cumulative-transfer experiments.

for example:

```text
react + vite + python
          ↓
        p5.js
          ↓
   learned knowledge
          ↓
      kaboom.js
```

if learning p5.js makes kaboom.js easier to acquire, that gives us evidence for a stronger form of transfer.

---

### openscad

openscad is deliberately much further away.

it introduces:

* a different language
* declarative construction
* parametric modeling
* constructive solid geometry
* transformations
* boolean operations
* geometric composition
* constraints
* 3d spatial reasoning

this is useful because trainery should not only work when the target is syntactically similar to something the model already knows.

openscad lets us test transfer across a larger conceptual boundary.

---

### cadquery

cadquery provides another useful condition.

the source language is python:

```text
python
   ↓
cadquery
```

but cadquery introduces a specialized programming model for parametric cad.

this creates a different experiment from openscad.

the language is familiar, but the domain and api are specialized.

that distinction matters.

---

## why use multiple targets?

the point is not to prove transfer with one convenient example.

different targets let us test different kinds of transfer.

```text
p5.js
javascript → javascript
creative coding

three.js
javascript → javascript
3d graphics

kaboom.js
javascript → javascript
game development

openscad
new language + cad domain
declarative / csg modeling

cadquery
python → python
specialized cad api
```

these are different experimental conditions.

we should not collapse them into a single idea of "similarity."

---

## the conceptual graph

one of the core components of trainery is a structured knowledge graph.

the graph represents concepts and their relationships across environments.

a simplified example might look like:

```text
react component
      │
      ├── analogous_to ──→ openscad module
      │
      ├── specializes ──→ reusable abstraction
      │
      └── differs_from ──→ geometric primitive
```

another example:

```text
javascript function
        │
        ├── generalizes ──→ callable abstraction
        │
        └── relates_to ──→ openscad module
```

the graph should not simply say:

```text
react component = openscad module
```

because that would be false.

instead, it should encode:

```text
shared properties
differences
scope of correspondence
evidence
confidence
examples
failure cases
```

analogy is not equivalence.

this distinction is fundamental to the project.

---

## graph + vectors

trainery uses two different kinds of retrieval.

### vector retrieval

vector search helps answer:

> what things are semantically related to this thing?

this is useful for discovering candidate relationships and retrieving relevant examples.

### graph traversal

the graph helps answer:

> how are these things explicitly related?

for example:

```text
concept
  ↓
source implementation
  ↓
transfer relationship
  ↓
target concept
  ↓
target implementation
```

semantic similarity alone should not be treated as proof of a transfer relationship.

the two systems therefore serve different purposes.

---

## falkordb

falkordb is intended to provide the graph and vector infrastructure for this knowledge layer.

the graph can contain nodes representing things such as:

* programming concepts
* languages
* frameworks
* libraries
* apis
* operations
* abstractions
* domain concepts
* examples
* tasks
* constraints
* environments

relationships can be typed.

examples include:

```text
analogous_to
partial_analogy
implements
composes
depends_on
generalizes
specializes
requires
contrasts_with
represents
operates_on
```

relationships should ideally contain provenance and evidence rather than being unexplained edges.

---

## the training pipeline

the eventual pipeline looks approximately like:

```text
documentation
examples
source code
benchmarks
        │
        ▼
    ingestion
        │
        ▼
knowledge extraction
        │
        ▼
concept / environment graph
        │
        ▼
transfer analysis
        │
        ▼
curriculum generation
        │
        ▼
training
        │
        ▼
execution
        │
        ▼
evaluation
        │
        ▼
results
```

the curriculum should distinguish between:

```text
already known

transferable

target-specific

novel
```

the point is not to waste target-training capacity teaching something the model already understands.

---

## data ingestion

documentation and examples need to be collected from the target environments.

the project can use:

* firecrawl for crawling and extracting documentation
* tavily for discovery and research
* structured parsers where available
* source repositories and official examples

all ingested information should retain provenance.

we should be able to answer:

> where did this piece of knowledge come from?

training data should also be versioned where practical.

---

## execution and evaluation

generated programs should be executed whenever possible.

a model producing syntactically plausible code is not enough.

for example:

```text
model output
     ↓
compile / execute
     ↓
observe result
     ↓
compare with expected behavior
```

possible infrastructure includes:

* e2b for sandboxed execution
* browserbase for browser-based environments and evaluation

the evaluation system should prefer behavioral evidence over textual similarity.

---

## evaluating graphics

for p5.js, three.js, and kaboom.js, evaluation can include execution and rendered behavior.

examples:

```text
does the sketch run?

does the object appear?

does it move correctly?

does interaction work?

does the requested state change occur?

does the program behave correctly on an unseen task?
```

the goal is not necessarily pixel-perfect reproduction.

the evaluation should measure whether the generated program actually implements the requested behavior.

---

## evaluating cad

cad needs different evaluation.

code similarity is especially weak here.

two programs can produce equivalent geometry while looking completely different as code.

therefore the evaluation should inspect the resulting model.

possible checks include:

* whether the model compiles
* whether geometry exists
* dimensions
* topology
* boolean results
* spatial relationships
* required features
* geometric constraints

the actual artifact matters.

---

## baselines

the minimum experimental comparison should contain three conditions.

### condition 1: target only

```text
target data
    ↓
model
    ↓
target capability
```

this establishes the baseline.

### condition 2: source + target

```text
source data + target data
          ↓
        model
          ↓
   target capability
```

this tells us whether simply adding source material helps.

### condition 3: transfer-aware

```text
source knowledge
       +
transfer graph
       +
target data
       ↓
    training
       ↓
target capability
```

this tests the actual trainery hypothesis.

the third condition should not quietly receive more information than the others without that being accounted for.

---

## what we measure

possible metrics include:

### execution

* syntax validity
* compilation success
* execution success
* runtime failures

### task performance

* task completion
* semantic correctness
* behavioral correctness
* modification tasks
* composition tasks
* debugging tasks

### generalization

* unseen tasks
* novel combinations
* tasks outside the training examples
* specification → implementation

### learning efficiency

* target-specific examples required
* training steps
* compute
* wall-clock time
* time to proficiency

### transfer quality

* successful transfer
* partial transfer
* incorrect transfer
* transfer failures
* hallucinated correspondences

failed transfer is still useful data.

in fact, understanding where transfer stops working is one of the research questions.

---

## trainium

trainium is not the foundation of the entire project.

the research infrastructure should work independently of the training backend.

the intended progression is:

```text
research design
      ↓
knowledge ingestion
      ↓
graph
      ↓
transfer system
      ↓
curriculum
      ↓
evaluation
      ↓
baseline experiments
      ↓
initial transfer experiments
      ↓
analysis
      ↓
trainium experiments
```

this keeps the research logic separate from the hardware infrastructure.

trainium then gives us a controlled environment for fixed-budget experiments.

the important question becomes something like:

> under the same compute budget, does transfer-aware training produce more target capability from the available target data?

that is much more informative than simply throwing more compute at the problem.

---

## current infrastructure

the project has access to or may use:

### knowledge / research

* firecrawl
* tavily
* falkordb

### execution

* e2b
* browserbase

### model / inference infrastructure

* nebius token factory
* backboard
* adaptionlabs.ai

### development

* ibm bob
* aws kiro

### training

* aws trainium / trainium frontier

these are infrastructure components, not the research hypothesis.

providers should be isolated behind adapters where practical so that experiments are reproducible and not permanently coupled to one service.

---

## eventual interface

the eventual user-facing interface could allow someone to define:

```text
what does the agent already know?

[ react ]
[ vite ]
[ python ]
[ ... ]

what should it learn?

[ p5.js ]
[ three.js ]
[ kaboom.js ]
[ openscad ]
[ cadquery ]
```

trainery would then construct a transfer-aware learning path.

conceptually:

```text
known environments
        ↓
known concepts
        ↓
transfer graph
        ↓
target concepts
        ↓
missing knowledge
        ↓
curriculum
        ↓
training
        ↓
evaluation
```

but the interface is downstream of the research.

the first goal is proving that the mechanism works.

---

## cumulative learning

one of the longer-term experiments is whether acquired knowledge remains useful.

for example:

```text
react + vite + python
          ↓
        p5.js
          ↓
      p5.js knowledge
          ↓
       kaboom.js
```

we could compare:

```text
baseline:
react + vite + python → kaboom.js

cumulative:
react + vite + python + learned p5.js → kaboom.js
```

and eventually:

```text
react
  ↓
p5.js
  ↓
kaboom.js
  ↓
three.js
  ↓
another environment
```

the interesting result would not simply be that the model knows more.

it would be whether **learning itself becomes easier as the knowledge base grows**.

---

## project status

this repository is the experiment, not the conclusion.

### research

* [ ] formalize hypothesis
* [ ] define experimental variables
* [ ] define proficiency criteria
* [ ] define evaluation tasks
* [ ] define baseline conditions
* [ ] define transfer conditions
* [ ] define cumulative-transfer experiments

### knowledge system

* [ ] documentation ingestion
* [ ] concept extraction
* [ ] environment representation
* [ ] graph schema
* [ ] transfer relationship schema
* [ ] provenance
* [ ] vector retrieval
* [ ] graph traversal

### curriculum

* [ ] known/unknown classification
* [ ] transfer path generation
* [ ] target-specific gap detection
* [ ] curriculum generation
* [ ] curriculum versioning

### environments

* [ ] p5.js
* [ ] three.js
* [ ] kaboom.js
* [ ] openscad
* [ ] cadquery

### evaluation

* [ ] execution harness
* [ ] behavioral tests
* [ ] graphics evaluation
* [ ] cad geometry evaluation
* [ ] generalization tests
* [ ] transfer-error tracking

### training

* [ ] target-only baseline
* [ ] source + target baseline
* [ ] transfer-aware training
* [ ] trainium backend
* [ ] fixed-budget experiment
* [ ] cumulative transfer

---

## repository philosophy

trainery should optimize for research validity before demo quality.

that means:

* reproducible experiments over impressive demos
* explicit assumptions over hidden assumptions
* measured source knowledge over assumed source knowledge
* typed relationships over vague similarity
* behavioral evaluation over code resemblance
* provenance over unexplained data
* baselines over cherry-picked results
* failed experiments over discarded experiments
* isolated infrastructure over vendor lock-in
* documented methodology over unexplained model behavior

the most interesting outcome is not necessarily:

> trainery works.

it could be:

> transfer works for some classes of concepts but fails for others.

that would still tell us something important about how ai agents acquire programming environments.

---

## the core hypothesis

trainery ultimately tests a simple idea:

> an ai agent should not have to relearn everything it already knows every time it enters a new programming environment.

the research question is whether explicitly representing what the agent knows, how that knowledge relates to the target environment, and where those relationships stop being valid can make new capability acquisition more efficient and more generalizable.

if it works, learning environments may become cumulative.

if it doesn't, the failure should tell us where conceptual transfer breaks down.

either result is useful.
