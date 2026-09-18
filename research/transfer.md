# transfer model

## purpose

this document describes what trainery means by knowledge transfer.

transfer is not:

```text
find two similar words
```

and it is not:

```text
replace api a with api b
```

the intended unit of transfer is a concept and its properties.

---

## conceptual representation

a concept can be represented approximately as:

```text
concept
├── definition
├── properties
├── operations
├── constraints
├── examples
├── environment
└── relationships
```

a transfer relationship then describes how that concept relates to another environment.

---

## example

consider:

```text
parameterized reusable construction
```

in react this might appear as:

```text
component + props
```

in openscad it might appear as:

```text
module + parameters
```

there is a meaningful conceptual relationship.

but the semantics are not identical.

the transfer representation should therefore include:

```text
shared:
- reusable construction
- parameterization
- composition

different:
- rendering model
- execution semantics
- state model
- lifecycle
```

---

## transfer edge

a transfer edge can conceptually contain:

```text
source
target
relationship
confidence
evidence
shared_properties
differences
examples
failure_cases
```

example:

```text
source:
react props

target:
openscad module parameters

relationship:
partial_analogy

shared:
parameterized construction

difference:
different execution and rendering semantics
```

---

## transfer types

possible relationship types:

### analogous_to

two concepts share meaningful structural properties.

### partial_analogy

some properties correspond, but others do not.

### generalizes

the source concept is an instance of a broader concept.

### specializes

the target concept introduces domain-specific behavior.

### implements

one environment provides an implementation of a broader concept.

### composes

one concept can be constructed from other concepts.

### depends_on

one concept requires another.

### contrasts_with

the concepts appear similar but differ in an important way.

### requires

a target concept depends on another concept being understood first.

---

## transfer direction

relationships do not necessarily work equally in both directions.

for example:

```text
general programming abstraction
        ↓
domain-specific abstraction
```

may be useful.

the reverse direction may not be.

therefore edges should be directional when the evidence requires it.

---

## transfer boundaries

the system should explicitly represent where transfer stops.

example:

```text
react component
    ↓
openscad module

transferable:
reusability
parameterization
composition

not transferable:
react lifecycle
dom rendering
hooks
state updates
```

the negative information is important.

otherwise the system may over-transfer.

---

## transfer confidence

confidence should not mean:

> the model thinks these are similar.

it should represent evidence for the specific relationship.

possible evidence sources:

* documentation
* formal language semantics
* implementation behavior
* human-authored mapping
* repeated successful transfer
* controlled experiment

experimental evidence should be distinguishable from documentation-derived evidence.

---

## transfer as curriculum

the graph should ultimately help answer:

> what should the agent learn next?

for example:

```text
known:
functions
parameters
composition
iteration

target:
p5.js

already transferable:
function callbacks
iteration
coordinate transformations

target-specific:
setup/draw lifecycle
canvas state
p5.js event APIs
```

the curriculum can therefore spend more training capacity on:

```text
setup/draw
canvas state
p5-specific interaction
```

rather than reteaching generic programming concepts.

---

## failed transfer

a transfer relationship can be rejected after evaluation.

this should be stored rather than simply deleted.

for example:

```text
candidate:
react state ↔ p5.js drawing state

result:
poor transfer

reason:
surface-level similarity but different semantics
```

negative evidence can make future curriculum generation safer.
