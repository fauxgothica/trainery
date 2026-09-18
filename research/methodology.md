# methodology

## experimental structure

trainery uses controlled comparisons between different training conditions.

the first experiment family should contain three conditions.

### a — target-only

the model receives target-environment training data.

```text
target data
    ↓
training
    ↓
evaluation
```

### b — source + target

the model receives source-environment data in addition to target data.

```text
source data
    +
target data
    ↓
training
    ↓
evaluation
```

### c — transfer-aware

the model receives target information alongside structured knowledge about relationships between the source and target.

```text
source knowledge
       +
transfer graph
       +
target data
       ↓
training
       ↓
evaluation
```

the purpose of condition b is important.

without it, an improvement in condition c could simply come from giving the model more information.

---

## variables

### independent variables

potential independent variables include:

* source environments
* target environment
* training condition
* amount of target data
* amount of source data
* transfer graph availability
* transfer graph density
* curriculum strategy
* training compute

### dependent variables

potential dependent variables include:

* execution success
* semantic correctness
* task completion
* generalization
* debugging ability
* modification ability
* target proficiency
* target data required
* compute required

---

## source proficiency

source environments should be evaluated before being used as transfer sources when practical.

for example:

```text
source:
react + vite + python

source evaluation
        ↓
source proficiency established
        ↓
transfer experiment
```

this prevents weak source knowledge from being mistaken for a transfer failure.

---

## target proficiency

proficiency should be defined using task families rather than a single score.

for example:

```text
level 1 — syntax / basic execution

level 2 — basic concepts

level 3 — multi-concept programs

level 4 — modification

level 5 — debugging

level 6 — unseen specifications

level 7 — composition / novel tasks
```

the exact levels can vary by environment.

---

## task generation

tasks should test capabilities rather than documentation memorization.

a good task should require the model to construct something from a specification.

examples:

```text
"create a canvas containing a moving circle"

"create a scene containing a camera, light, and rotating object"

"create a game where the player collects objects"

"create a parametric box with a cylindrical cutout"
```

the evaluation should focus on whether the resulting program satisfies the specification.

---

## held-out evaluation

training examples and evaluation examples should be separated.

the evaluation set should contain:

* unseen tasks
* recombinations of known concepts
* modifications
* debugging
* novel specifications

where possible, evaluation should avoid simply asking the model to reproduce memorized examples.

---

## transfer-error analysis

every transfer-aware experiment should record incorrect transfer.

example:

```text
source concept:
react component

target:
openscad module

transfer:
reusable parameterized abstraction

correct:
both can package reusable parameterized construction

incorrect:
assuming react-style lifecycle semantics exist in openscad
```

this makes the graph more useful over time.

---

## cumulative experiment

after an environment has been learned, it can become a source for a later experiment.

example:

```text
phase 1

react + vite + python
        ↓
      p5.js


phase 2

react + vite + python
        +
learned p5.js knowledge
        ↓
     kaboom.js
```

the relevant comparison is:

```text
fresh-source kaboom learning

vs

kaboom learning with acquired p5.js knowledge
```

---

## reproducibility

each experiment should record:

```text
model
model version
source environments
target environment
dataset versions
training configuration
graph version
curriculum version
compute budget
evaluation version
random seed
results
```

the exact set of metadata can evolve, but the principle should remain.

---

## interpretation

results should distinguish between:

```text
observed result
```

and:

```text
interpretation
```

for example:

```text
observed:
transfer-aware training achieved higher execution success.

interpretation:
structured transfer may have reduced target-specific learning requirements.
```

the second statement should not be treated as proven merely because the first was observed.
