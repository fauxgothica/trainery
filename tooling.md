# tooling

this file describes what each external tool is actually doing in the trainery research stack.

the tools are infrastructure.

they are not the research hypothesis.

---

## falkordb

falkordb is the intended backend for the conceptual knowledge graph.

trainery can use it to represent:

```text
environments
concepts
apis
operations
examples
relationships
transfer edges
```

it also provides vector-search functionality, which can be used for semantic retrieval.

the graph and vector layers should remain conceptually separate:

```text
vector search:
"what is related?"

graph:
"how is it related?"
```

---

## firecrawl

firecrawl is used for documentation ingestion.

possible uses:

* crawl official documentation
* extract pages
* collect examples
* collect reference material
* create source documents for knowledge extraction

the resulting data should retain provenance.

---

## tavily

tavily is used primarily for discovery and research.

possible uses:

* find relevant documentation
* locate official references
* discover examples
* find information that should then be ingested or verified

tavily is not itself the knowledge graph.

---

## e2b

e2b provides sandboxed execution for generated code.

the purpose is to turn:

```text
generated program
```

into:

```text
observable execution result
```

this is useful for evaluation.

---

## browserbase

browserbase can provide browser-based execution environments for targets that require a browser.

this is particularly relevant for:

```text
p5.js
three.js
kaboom.js
```

where the target program may need to render or interact inside a browser environment.

---

## nebius token factory

nebius can be used for model inference and related experimentation.

the exact model and inference configuration should be recorded per experiment.

it should remain an infrastructure adapter rather than being embedded throughout the research logic.

---

## backboard

backboard can be used as part of the agent/inference experimentation layer where useful.

its role should remain isolated from:

```text
knowledge representation
transfer logic
evaluation logic
```

so that the research is not dependent on one inference provider.

---

## adaptionlabs.ai

adaptionlabs resources can be used to support model experimentation and development.

again, provider-specific behavior should be isolated where practical.

---

## trainium

aws trainium is the eventual controlled training backend.

trainium is useful because the project can perform experiments under a constrained compute budget.

the intended use is not:

```text
put the entire project on trainium
```

but:

```text
build research pipeline
        ↓
establish baselines
        ↓
run transfer experiments
        ↓
move controlled training runs to trainium
```

trainium-specific implementation belongs under:

```text
training/trainium/
```

---

## ibm bob

ibm bob can be used as a development tool while building the project.

it is not part of the research methodology.

---

## aws kiro

aws kiro can similarly be used as a development tool.

it should not become a hidden dependency of the research pipeline.

---

## general tooling principle

each tool should have one clearly defined job.

the research should still make sense if one provider is replaced.

conceptually:

```text
research logic
      │
      ├── knowledge adapter
      ├── retrieval adapter
      ├── execution adapter
      ├── inference adapter
      └── training adapter
```

this keeps infrastructure replaceable and experiments understandable.
