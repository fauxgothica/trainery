# research hypothesis

## primary hypothesis

an ai agent can acquire proficiency in a new programming environment more efficiently when its existing conceptual knowledge is explicitly identified and transferred into the target learning process.

the hypothesis is not that two environments need to be syntactically similar.

the hypothesis is that programming knowledge contains reusable concepts that can act as priors across environments.

---

## motivating observation

a programming environment contains both:

```text
general programming knowledge
```

and:

```text
environment-specific knowledge
```

for example, an agent may already understand:

```text
functions
parameters
loops
composition
abstraction
state
events
transformation
modules
coordinate systems
```

before it encounters a particular framework or language.

if the target environment introduces a new representation of one of these concepts, the existing concept may provide a useful starting point.

---

## core question

the experiment asks:

> does explicitly structured conceptual transfer improve target-environment acquisition compared with target-only learning and source-plus-target learning?

---

## secondary questions

### q1: does transfer reduce target data requirements?

can an agent reach a particular proficiency level with fewer target-specific examples?

### q2: does transfer reduce compute requirements?

can the same target capability be reached with less training compute?

### q3: does transfer improve generalization?

does the agent perform better on tasks it has not directly seen during training?

### q4: where does transfer fail?

which concepts appear transferable but produce incorrect behavior when mapped to the target environment?

### q5: does acquired knowledge compound?

after learning one new environment, does that knowledge make learning another environment easier?

---

## stronger long-term hypothesis

learning may be cumulative.

instead of:

```text
learn environment a
forget / isolate environment a

learn environment b
start again
```

we want to test:

```text
learn a
  ↓
retain transferable knowledge
  ↓
learn b using a
  ↓
retain transferable knowledge
  ↓
learn c using a + b
```

the important variable is not simply the amount of knowledge.

it is whether previously acquired capabilities improve the efficiency of acquiring future capabilities.

---

## null hypothesis

there may be no meaningful benefit from explicit conceptual transfer.

possible explanations include:

* modern models already internally perform the necessary transfer
* the graph adds no useful information
* the transfer relationships are too noisy
* target data is sufficient
* source knowledge does not meaningfully reduce target learning
* transfer introduces incorrect assumptions
* the model cannot reliably use structured transfer information

these outcomes should be treated as legitimate experimental results.

---

## alternative outcomes

transfer could produce:

```text
positive transfer
```

where source knowledge improves target learning.

or:

```text
negative transfer
```

where source assumptions actively hurt target performance.

or:

```text
conditional transfer
```

where certain concepts transfer while others do not.

conditional transfer is especially interesting because it would suggest that the useful unit of transfer is not an entire programming environment, but individual concepts and relationships.
