# research journal

this is the messy chronological notebook for trainery.

unlike the other research documents, this file is allowed to contain:

* unfinished ideas
* questions
* failed experiments
* weird observations
* implementation notes
* hypotheses that later turn out to be wrong
* decisions
* things that need to be investigated
* thoughts that are not ready for the formal methodology

the formal research documents should describe the current methodology.

this file records how we got there.

---

## 2026-09-18

### kaboom.js as the next target

kaboom.js is being added as another target environment.

the useful property is that it is javascript → javascript while still introducing a specialized programming model.

this makes it a useful complement to p5.js and three.js.

the particularly interesting experiment is cumulative transfer:

```text
react + vite + python
          ↓
        p5.js
          ↓
   learned p5.js knowledge
          ↓
      kaboom.js
```

the question is whether learning one specialized javascript environment creates a useful prior for another.

this is different from simply saying:

> p5.js and kaboom.js are both javascript.

the language-level similarity is only one variable.

the actual question is whether acquired conceptual knowledge transfers.

---

## open questions

* how should source proficiency be measured?
* what exactly counts as "proficiency" for each target?
* how should transfer relationships be generated?
* how much of the graph should be human-verified?
* how should negative transfer be represented?
* how should curriculum generation decide what to skip?
* how much target data should each condition receive?
* how should compute be normalized?
* what should count as successful cumulative transfer?
* how should visual and geometric artifacts be evaluated automatically?

---

## current principle

do not make the experiment prove the hypothesis.

make the experiment capable of disproving it.
