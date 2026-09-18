# evaluation

trainery evaluates whether an agent has actually acquired a programming environment rather than merely producing plausible-looking code.

the primary principle is:

> evaluate what the program does whenever possible.

---

## evaluation pipeline

```text
task specification
        ↓
agent generates program
        ↓
program execution
        ↓
artifact / behavior
        ↓
evaluation
        ↓
result
```

---

## evaluation categories

### 1. syntax

does the generated program parse?

```text
pass
fail
```

syntax is useful but insufficient.

---

### 2. execution

does the program successfully run?

measure:

* compilation
* startup
* runtime errors
* execution completion

---

### 3. semantic correctness

does the program actually implement the requested behavior?

a program can execute successfully while doing the wrong thing.

---

### 4. modification

give the agent an existing program and request a change.

this tests whether it understands the environment rather than only generating isolated examples.

---

### 5. debugging

provide a broken program.

measure whether the agent can:

```text
identify the problem
↓
modify the program
↓
produce a working result
```

---

### 6. generalization

evaluate tasks that were not represented directly in the training set.

this is one of the most important categories.

---

## proficiency

proficiency should be represented as a vector rather than a single number where practical.

for example:

```text
execution:        0.92
basic concepts:   0.88
composition:      0.73
modification:     0.61
debugging:        0.54
generalization:   0.48
```

the exact representation may change.

the important principle is to avoid reducing the entire experiment to one arbitrary score.

---

## p5.js evaluation

possible task families:

```text
draw a shape

animate an object

respond to keyboard input

respond to mouse input

create multiple interacting objects

apply transformations

compose a scene

modify an existing sketch
```

evaluation can inspect:

* execution
* canvas state
* object position
* animation
* interaction
* requested visual elements

---

## three.js evaluation

possible task families:

```text
create a scene

add camera and renderer

create geometry

apply materials

add lighting

transform objects

animate an object

compose an object hierarchy
```

evaluation can inspect:

* successful rendering
* object existence
* transforms
* scene structure
* interaction
* animation

---

## kaboom.js evaluation

possible task families:

```text
create a scene

spawn a player

move the player

add controls

spawn objects

detect collisions

track score

create enemies

change game state

modify an existing game
```

the higher-level tasks should require composition.

for example:

```text
create a game where the player moves through a level,
collects objects, avoids enemies, and reaches an exit.
```

this tests whether individual concepts can be combined into a working system.

---

## openscad evaluation

code should be executed and the resulting geometry inspected.

possible task families:

```text
create a primitive

parameterize a dimension

combine solids

subtract a solid

intersect solids

create a reusable module

construct a multi-part object
```

evaluation should inspect geometry where possible.

---

## cadquery evaluation

possible task families:

```text
create a workplane

create a sketch

extrude geometry

cut geometry

apply a fillet

apply a chamfer

parameterize dimensions

compose multiple operations
```

again, the final geometry is more important than textual similarity.

---

## transfer-specific metrics

transfer experiments should track:

```text
target performance
target data used
source data used
training compute
training time
time to proficiency
transfer errors
generalization
```

the interesting quantity is not simply:

```text
score
```

but something closer to:

```text
capability achieved
        /
target-specific resources required
```

---

## negative transfer

the system should explicitly detect cases where source knowledge makes performance worse.

example:

```text
without transfer:
70% task success

with transfer:
61% task success
```

this should not automatically be treated as a failed implementation.

it could indicate that the transfer relationship itself is harmful.

---

## reproducibility

every evaluation result should be associated with:

```text
model
experiment
dataset
graph version
curriculum version
evaluation version
environment version
configuration
```

results should be stored rather than only printed to a terminal.
