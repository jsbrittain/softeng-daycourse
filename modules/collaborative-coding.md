---
layout: two-cols-header
routeAlias: "collaborative-coding"
---

# Collaborative Coding with AI

<span />

## Treat AI like a junior developer

::left::

- Writes code fast, sometimes wrong
- Never sleeps, works 24/7
- Has no domain knowledge
- Needs clear specifications
- **Needs code review**

::right::

<v-click>

The same tools that coordinate human teams coordinate human–AI teams:
- Shared vs fork model
- Feature branches
- Pull requests
- Code review

</v-click>

<v-click>

**This is the point.** These collaboration models weren't designed for AI. They were designed for humans. They work for both — and AI makes them more valuable, not obsolete.

</v-click>

---
layout: two-cols-header
---

# Collaborative Code Development Models

::left::

::center

Shared repository model<br />
(common in private projects)

<div class="h-4" />
<img src="../img/github-shared-repo.png" alt="Shared repository model" width="210px">
::

::right::

::center

<div v-click>

Fork and pull model<br />
(popular in open source)

<div class="h-4" />
<img src="../img/github-fork-pull.png" alt="Shared repository model" width="350px">

</div>
::

---

# Collaborative project

### ZooShowcase

https://github.com/OxfordRSE/softeng-daycourse-zoo

Add an animal to the zoo. Copy (and modify) one of the existing animals (e.g. `src/zoo/elephant.py`) to create a new animal (e.g. `src/zoo/kangaroo.py`).

```python
# src/zoo/kangaroo.py
from animal import Animal

class Kangaroo(Animal):
    def __init__(self, name="Roo"):
        super().__init__(name, species="Kangaroo")

    def sound(self):
        return "thumps"

    def action(self):
        return "hops around happily."
```

---
layout: instruction
---

# PR exercise: Human + AI

::left::

::center
Human tests, AI implementation
::

::right::

- Fork the ZooShowcase repository
- **Write a test** for a new animal *before* implementing it
  - What sound does it make? What action?
- Ask AI to implement the animal class that passes your test
- Review AI's implementation
- Create a feature branch, commit, submit a PR
- Notice the workflow: **your test was the spec AI followed**

---
layout: two-cols-header
class: "gap-4"
---

# Code Review in the AI Era

::left::

### Reviewing AI code is different

- AI code *looks* plausible but may be subtly wrong
- Check for **hallucinated APIs** (using functions that don't exist)
- Check for **edge cases** AI didn't consider
- Check for **security vulnerabilities** AI may introduce
- Check for **domain correctness** — does it make scientific sense?

::right::

<v-click>

### What hasn't changed

- Identifies defects early in the process
- Cost-effective error removal
- Enhances team learning and collaboration
- Improves overall team software development process

</v-click>

---

# Code Review and AI

<div class="h-4" />

<v-clicks>

- AI can act as a **first-pass reviewer** — checks for style, common bugs
- AI can generate **diff summaries** for PR descriptions
- AI can suggest **improvements** to code
- **Human review is still essential** — AI lacks domain understanding
- AI's review is *useful* but not *sufficient*

</v-clicks>

---
layout: instruction
---

# AI Code Review exercise

::left::

::center
Review an AI-generated PR
::

::right::

- Ask AI to add a new animal to the ZooShowcase and create a PR
- Review the PR:
  - Does the code do what it claims?
  - Are there edge cases?
  - Does it follow the project patterns?
  - Are there security concerns?
- Give constructive review feedback
- Ask AI to address your feedback

---
layout: instruction
---

# Pull Requests

::left::

::center
Code Review + Test
::

::right::

Instructor demo:
- Code Review

Task:
- Add a test *in the same feature branch*, testing locally to ensure that it passes before committing
- Navigate to your pull request, notice that your PR has been updated with your test code
