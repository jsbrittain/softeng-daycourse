---
layout: two-cols-header
routeAlias: "dependency-management"
---

# Dependency management in the AI era

::left::

```python
import numpy as np

def main():
    ...
```

::center
<br>

*<v-click>Which version of numpy?</v-click>*

::

<v-click>

AI can write `import` statements instantly.
But which version? Does that package exist?
**Dependency management is verification work.**

<v-click>

**This is not new.** Lock files, environments, and audits existed before AI. They ensured reproducibility for human teams. AI just raises the stakes — hallucinated packages and version drift are now realistic threats.

</v-click>

</v-click>

::right::

<img src="../img/numpy-versions.png" alt="Numpy versions" />

---

# AI-Specific Dependency Risks

<div class="h-4" />

<v-clicks>

- **Hallucinated packages**: AI may suggest nonexistent packages
  - Real risk: if the name is plausible, someone could publish a malicious package with that name
- **Outdated versions**: AI may not know about recent releases or security patches
- **Compatibility errors**: AI may suggest packages that conflict with your environment
- **Transitive dependencies**: AI may not consider the full dependency tree

</v-clicks>

---
layout: two-cols-header
leftClass: "items-center justify-center gap-10"
rightClass: "items-center justify-center gap-10"
---

# Dependency management

::left::

<div class="flex flex-col items-center">
<b>Semantic versioning (SemVer)</b><br>
<small>API stability, communication, dependency management</small>
</div>

<div class="flex flex-col items-center">
<b>Calendar versioning (CalVer)</b><br>
<small>Regular releases, simplicity</small>
</div>

::right::

<div class="flex flex-col items-center">
<b>4.3.1</b><br>
<small>(major.minor.patch)</small>
</div>

<div class="flex flex-col items-center">
<b>2025.01</b><br>
<small>(year.month)</small>
</div>

---
layout: two-cols-header
---

# Dependency management

::left::

```python
import numpy as np

def main():
    ...
```

::right::

<img src="../img/numpy-versions.png" alt="Numpy versions" />

<v-click>
  <FancyArrow
    x1="400"
    y1="270"
    x2="535"
    y2="340"
    arc="-0.2"
    head-size="20"
    v-click="1"
  />
</v-click>

---

# Dependency management

<div style="position: absolute; top: 100, left: 100; width: 100; height: 100;">
<img src="../img/numpy-logo.svg" alt="Numpy logo" />
</div>

<div class="h-10"></div>

::center

**numpy** is a top-20 downloaded package on PyPI<br>
which in June 2024 released a new major version.

<v-click>

Numpy v1 and v2 were no longer entirely compatible.

</v-click>

<v-click>

The official release notes included the phrase:

_"This major release includes <span v-mark.circle.red="3">breaking changes</span>…<br>
including API changes …"_

</v-click>

::

---

# Virtualisation

<div style="position: relative; top: 40px; width: 100%; height: auto; margin: auto;">

  <div class="flex flex-col items-center space-y-1">
    <div class="flex space-x-1">
      <span v-mark.circle.red="8">
        <div class="w-40 h-20 bg-yellow-500 text-white flex items-center justify-center rounded">venv</div>
      </span>
    </div>
    <div class="flex space-x-1">
      <div class="w-80 h-20 bg-amber-500 text-white flex items-center justify-center rounded" v-click="2">conda</div>
    </div>
    <div class="flex space-x-1">
      <div class="w-120 h-20 bg-orange-500 text-white flex items-center justify-center rounded" v-click="4">Container</div>
    </div>
    <div class="flex space-x-1">
      <div class="w-160 h-20 bg-red-500 text-white flex items-center justify-center rounded" v-click="6">Virtual Machine</div>
    </div>
  </div>
  
  <div class="absolute top--10 right-25" v-click="1">
    Python & packages
  </div>
  
  <FancyArrow
    x1="673"
    y1="-10"
    x2="525"
    y2="40"
    arc="0.2"
    head-size="20"
    v-click="1"
  />
  
  <div class="absolute top-12 left-10" v-click="3">
    General software
  </div>
  
  <FancyArrow
    x1="110"
    y1="75"
    x2="265"
    y2="125"
    arc="-0.2"
    head-size="20"
    v-click="3"
  />
  
  <div class="absolute top-33 right--6" v-click="5">
    Environment
  </div>
  
  <FancyArrow
    x1="835"
    y1="160"
    x2="685"
    y2="210"
    arc="0.2"
    head-size="20"
    v-click="5"
  />
  
  <div class="absolute top-55 left--8.5" v-click="7">
    System
  </div>
  
  <FancyArrow
    x1="0"
    y1="245"
    x2="110"
    y2="295"
    arc="-0.2"
    head-size="20"
    v-click="7"
  />

</div>

---

# Dependency management

<br />

How do we keep a record of our dependencies?

One very simple but effective way is to record them in a `requirements.txt` file:

```text
numpy==1.26.2       # version tagged
pandas<3            # version range
scipy               # unspecified! (latest version)
```

To install the dependencies in a `requirements.txt` file, use the command:
```bash
pip install -r requirements.txt
```

AI can generate this file for you — **but always verify the packages exist and are correct**

---
layout: instruction
---

# Dependency management — AI exercise

::left::

::center
Detect hallucinated packages
::

::right::

::small

- Ask AI to write a requirements.txt for a data science project
- Include some plausible but nonexistent packages in your prompt
- Try to install: `pip install -r requirements.txt`
- Run `pip-audit` to check for known vulnerabilities
- Lesson: **AI-suggested dependencies must be verified**

---
layout: instruction
---

# Dependency management — AI exercise

::left::

::center
AI resolves version conflicts
::

::right::

- Run the script `old_script.py` — it will tell you its requirements
- Ask AI to identify the version conflict and create a working `requirements.txt`
- Create a `venv` and install:
  ```bash
  python -m venv venv
  source venv/bin/activate
  pip install -r requirements.txt
  ```
- Run the software: `python old_script.py`
- Adjust and retry until it works
