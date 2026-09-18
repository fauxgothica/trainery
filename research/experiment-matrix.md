# experiment matrix

this file defines the initial experiment space.

the goal is to test different kinds of transfer rather than only one convenient source/target pair.

---

## initial experiments

| source                | target    | condition       |
| --------------------- | --------- | --------------- |
| react + vite + python | p5.js     | target-only     |
| react + vite + python | p5.js     | source + target |
| react + vite + python | p5.js     | transfer-aware  |
| react + vite + python | three.js  | target-only     |
| react + vite + python | three.js  | source + target |
| react + vite + python | three.js  | transfer-aware  |
| react + vite + python | kaboom.js | target-only     |
| react + vite + python | kaboom.js | source + target |
| react + vite + python | kaboom.js | transfer-aware  |
| react + vite + python | openscad  | target-only     |
| react + vite + python | openscad  | source + target |
| react + vite + python | openscad  | transfer-aware  |
| python                | cadquery  | target-only     |
| python                | cadquery  | source + target |
| python                | cadquery  | transfer-aware  |

---

## why these targets?

### p5.js

```text
javascript → javascript
new creative coding environment
```

tests transfer where the underlying language is already familiar.

### three.js

```text
javascript → javascript
new 3d graphics environment
```

tests transfer into a different representation and domain.

### kaboom.js

```text
javascript → javascript
new game development environment
```

provides another specialized target and enables cumulative transfer from p5.js.

### openscad

```text
general programming knowledge
        ↓
new language
        ↓
declarative cad
```

tests a larger conceptual distance.

### cadquery

```text
python
  ↓
cadquery
```

tests transfer where the language is familiar but the domain-specific programming model is new.

---

## cumulative experiments

once individual targets have been evaluated, additional experiments can test whether acquired knowledge becomes useful.

### p5.js → kaboom.js

```text
react + vite + python
          ↓
        p5.js
          ↓
learned p5.js knowledge
          ↓
      kaboom.js
```

### three.js → another target

```text
react + vite + python
          ↓
       three.js
          ↓
learned three.js knowledge
          ↓
      later target
```

### openscad → cadquery

```text
python
  ↓
openscad
  ↓
learned cad / geometric knowledge
  ↓
cadquery
```

these should only be run after the individual environment experiments are understood.

---

## possible experiment ids

```text
001 — p5.js target-only baseline

002 — p5.js source + target

003 — p5.js transfer-aware

004 — three.js target-only baseline

005 — three.js source + target

006 — three.js transfer-aware

007 — kaboom.js target-only baseline

008 — kaboom.js source + target

009 — kaboom.js transfer-aware

010 — openscad target-only baseline

011 — openscad source + target

012 — openscad transfer-aware

013 — cadquery target-only baseline

014 — cadquery source + target

015 — cadquery transfer-aware

016 — p5.js → kaboom.js cumulative transfer
```

the numbering is organizational rather than permanent.

---

## evaluation dimensions

each environment should have environment-specific tasks covering:

```text
basic execution
basic concepts
multi-concept composition
modification
debugging
unseen specifications
generalization
```

additional environment-specific evaluation should be added where appropriate.

---

## target-specific evaluation

### p5.js

* canvas creation
* shapes
* drawing state
* animation
* interaction
* transformations
* multi-object composition

### three.js

* scene
* camera
* renderer
* geometry
* materials
* transforms
* lighting
* animation
* object hierarchy

### kaboom.js

* scene
* sprites
* movement
* controls
* collisions
* score/state
* enemies
* interactions
* game modification
* novel game generation

### openscad

* primitives
* transformations
* modules
* parameters
* unions
* differences
* intersections
* reusable geometry
* parametric models

### cadquery

* workplanes
* sketches
* extrusion
* cuts
* fillets
* chamfers
* parameterization
* reusable operations
* geometry composition
