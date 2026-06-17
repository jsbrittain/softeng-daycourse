---
layout: two-cols-header
leftClass: m-1
rightClass: m-1
routeAlias: writing-clean-code
---

# Writing Clean Code

## The AI Context Thesis

::left::

AI coding assistants read your existing code to understand what to generate.

The quality of what AI produces depends directly on the **context** you provide.

<v-click>

These practices were not invented for AI. Meaningful names, modular code, and clear documentation have always been hallmarks of clean code. What's new is that they now serve a **dual purpose**: they help humans **and** they help AI.

</v-click>

::right::

<v-clicks>

- Well-structured repos → AI knows where files belong
- Meaningful names → AI infers correct behaviour
- Type annotations → AI respects type contracts
- Docstrings → AI understands intent
- Tests → AI knows what "correct" means

</v-clicks>

---
layout: two-cols-header
leftClass: m-1
rightClass: m-1
---

# Writing Clean Code

## Organise your files — this is AI context too

::left::

```
Flat
├─ script.py
├─ image_1.jpg
├─ script_2.py
├─ utils.py
├─ image_1.png
├─ README.md
├─ image_2.png
├─ test_utils.py
├─ pyproject.toml
├─ notes.docx
├─ .gitignore
:
:
:
:
└─
```

::right::

<v-click>

```
Structured
├─ README.md
├─ pyproject.toml
├─ .gitignore
├─ src
│  ├─ script.py
│  ├─ script_2.py
│  └─ utils.py
├─ tests
│  └─ test_utils.py
├─ images
│  ├─ image_1.png
│  ├─ image_1.jpg
│  └─ image_2.png
├─ docs
│  └─ notes.docx
└─ dist
```

<small>AI agents navigate project files to understand structure.
A flat repo confuses AI as much as it confuses humans.
</small>
</v-click>

<!--
Software projects often start as a collection of scripts and assorted files, but will soon grow and become unwieldy. Structuring your projects will not only help you keep track of your files, but also make it easier for AI to understand your project structure.
-->

---
layout: two-cols-header
class: gap-4
---

# Writing Clean Code

## Use meaningful names — provides context for AI

::left::

```python
def convert(x):
    ...
```

::right::

<v-click>

```python
def celsius_to_fahrenheit(celsius):
    ...
```

</v-click>

---
layout: two-cols-header
class: gap-4
---

# Writing Clean Code

## Names as prompts for AI

::left::

```python
def convert(x):
    if isinstance(x, str):
        return x.upper()
    elif isinstance(x, int):
        return x * 2
    elif isinstance(x, list):
        return [convert(i) for i in x]
    else:
        return None
```

::right::

```python
def celsius_to_fahrenheit(celsius):
    """Convert Celsius to Fahrenheit."""
    return (celsius * 9/5) + 32
```

<v-click>

- Meaningful names help *us* understand the code
- But they also provide **context to AI models**
- Thus, AI models can provide **better suggestions**
- The function name is a *prompt* — `celsius_to_fahrenheit` tells the AI what you want

</v-click>

---
layout: two-cols-header
class: gap-4
---

# Writing Clean Code

## But context can also be a constraint for AI

::left::

```python
def levenshtein(a, b):
```

produces

```python {*}{maxHeight:'280px'}
def levenshtein(a, b):
    """Compute the Levenshtein distance
       between two strings."""

    if len(a) < len(b):
        return levenshtein(b, a)

    if len(b) == 0:
        return len(a)

    previous_row = range(len(b) + 1)
    for i, c1 in enumerate(a):
        current_row = [i + 1]
        for j, c2 in enumerate(b):
            insertions = previous_row[j + 1] + 1
            deletions = current_row[j] + 1
            substitutions = previous_row[j] \
                + (c1 != c2)
            current_row.append(
                min(
                    insertions,
                    deletions,
                    substitutions
                )
            )
        previous_row = current_row

    return previous_row[-1]
```

::right::

<v-click>

```python
from Levenshtein import distance

def levenshtein(a, b):
```

</v-click>

<v-click>

makes appropriate use of the imported library:

```python
def levenshtein(a, b):
    return distance(a, b)
```

</v-click>

<v-click>

AI (re)-invented the algorithm because the **import context constrained** it

</v-click>

<v-click>

Key insight: **what you put in the file shapes what AI produces** — use imports, types, and tests to guide AI

</v-click>

---

# Writing Clean Code

## Use consistent naming conventions

<div class="h-10" />

- Makes code more consistent (hence readable)
- Conventions are usually language-specific
    - [PEP 8](https://peps.python.org/pep-0008/) - Style Guide for Python Code
    - Python typically uses `snake_case` for function and variable names
- Conventions can provide context
    - Python typically uses `PascalCase` for class names
    - AI models are trained on codebases that follow these conventions

<div class="absolute right-5 top-35 w-[20%] text-xl">
<pre><code>
camelCase
PascalCase
kebab-case
snake_case
</code></pre>
</div>

---

# Writing Clean Code

## Type annotations — machine-readable contracts

<div class="h-4" />

```python
def process(data):
    # What type is data? What does it return?
```

<v-click>

vs

</v-click>

<v-click>

```python
def process(data: pd.DataFrame) -> pd.Series:
    # AI knows: pandas in, pandas out
```

</v-click>

<v-click>

- Type annotations are **machine-readable**
- AI models respect them — they constrain what AI generates
- Linters (mypy, pyright) verify type correctness automatically
- They serve as both documentation for humans and constraints for AI

</v-click>

---

# Writing Clean Code

## Linters

- Compares your code to a standard (e.g. PEP 8)
- Identifies programming errors, bugs, stylistic errors
- **Insulates AI output from quality issues** — AI code often violates style

<div class="h-5" />

::left::

<style>
code {
    font-size: 1.2rem;
    line-height: 2.0;
}
</style>

```python
import os

def hello():
    print(name)
```

::right::

<div class="h-2" />

<div class="twoslash lsp">
  <div class="twoslash-error-line twoslash-error-level-warning">
    <div class="twoslash-popup">
      <div class="twoslash-popup-content">
        <div>'os' imported but unused</div>
      </div>
    </div>
  </div>
</div>

<div class="h-7" />

<div class="twoslash lsp">
  <div class="twoslash-error-line">
    <div class="twoslash-popup">
      <div class="twoslash-popup-content">
        <div>expected 2 blank lines, found 1</div>
      </div>
    </div>
  </div>
</div>

<div class="twoslash lsp">
  <div class="twoslash-error-line">
    <div class="twoslash-popup">
      <div class="twoslash-popup-content">
        <div>undefined name 'name'</div>
      </div>
    </div>
  </div>
</div>

---

# Writing Clean Code

## Auto-formatters

<div class="flex justify-center">

<div class="w-1/2 p-4">

```python
def calc(a,b,c=2):
    x=a+b+c
    y=( a+b+c)/ 3 
    return  { "sum":x ,"avg":y }

nums=[1,2,3]
out=calc(   nums [0],nums [1] ,c = 5  )
print( out )
```

</div>
<div class="w-1/2 p-4">

```python
def calc(a, b, c=2):
    x = a + b + c
    y = (a + b + c) / 3 
    return {"sum": x, "avg": y}


nums = [1, 2, 3]
out = calc(nums[0], nums[1], c=5)
print(out)
```

</div>
</div>

<v-clicks>

- Run `ruff format` to automatically fix AI-generated style issues
- AI code often has inconsistent formatting — formatters fix this instantly
- Pair linters + formatters for a **zero-effort quality gate on AI output**

</v-clicks>

---

# Writing Clean Code

## Single responsibility principle — helps AI too

<div class="h-10" />

- Long functions conflate purpose, can easily introduce bugs
- Break long functions into smaller functions
- **AI works better with small, focused functions** — it can generate them more accurately
- Easier to replace smaller functions when new methods become available

---
layout: "two-cols-header"
---

# Writing Clean Code

## Single responsibility principle — helps AI too

::left::

<div class="p-4 pt-0" >

One large script

```python {*}{maxHeight:'330px'}
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
from sklearn.decomposition import PCA
from scipy.stats import ttest_ind

# 1. Load data
df = pd.read_csv("gene_expression.csv")

# 2. Preprocess
df = df.dropna()
df = df[df['quality'] > 0.8]

# 3. Perform PCA
pca = PCA(n_components=2)
pca_result = pca.fit_transform(df.iloc[:, 2:])

# 4. Statistical test
group1 = df[df['condition'] == 'treated']
group2 = df[df['condition'] == 'control']
p_value = ttest_ind(group1['geneX'], group2['geneX'])[1]

# 5. Plot results
sns.scatterplot(x=pca_result[:, 0], y=pca_result[:, 1])
plt.title("PCA of Gene Expression")
plt.show()

# 6. Save report
with open("report.txt", "w") as f:
    f.write(f"P-value for geneX: {p_value}")
```

</div>

::right::

<div class="p-4 pt-0">

Re-focus on logic (not implementation) — **each function is a better prompt for AI**

```python
df = load_and_clean("gene_expression.csv")
pca_result = run_pca(df)
p_value = run_ttest(df, "geneX")
plot_pca(pca_result)
write_report(p_value)
```

```python
def load_and_clean(filename)
def run_pca(df)
def run_ttest(df, gene)
def plot_pca(pca_result)
def write_report(p_value)
```

<div class="list-disc space-y-0 leading-tight">
<ul>
  <li v-click>Easier to read</li>
  <li v-click>Each function is a <b>clear prompt</b> for AI generation</li>
  <li v-click>AI can modify one function without breaking others</li>
</ul>
</div>

</div>

---

# Writing Clean Code

## Documentation

<div class="h-10" />

Instructions (README.md):
- Brief description of project
- How to install
- Preferably provide a minimal example
- **AI reads README to understand project purpose**

In code:
- Docstrings
- Annotations

---

# Writing Clean Code

## Documentation — docstrings

<div class="h-10" />

Docstrings ([PEP-257](https://peps.python.org/pep-0257/))
- Single or multiline
- Can be applied to functions and classes
- Forms self-documenting code (`help(function_name)`)
- **AI reads docstrings to understand function purpose without analysing implementation**

---
layout: "two-cols-header"
---

# Writing Clean Code

## Documentation — docstrings

::left::

<div class="p-4">

```python
def celsius_to_fahrenheit(celsius):
    """Convert celsius to Fahrenheit"""
    return 32 + 1.8 * celsius
```

</div>

::right::

<div class="p-4">

```python
> help(celsius_to_fahrenheit)

celsius_to_fahrenheit(celsius)
    Convert celsius to Fahrenheit
```

</div>

---
layout: "two-cols-header"
---

# Writing Clean Code

## Documentation — docstrings

::left::

<div class="p-4">

```python
def add3(a, b, c):
    """Add three numbers

    A longer description of the
    function, if one is necessary.

    Params:
        a, b, c: numbers to add

    Returns:
        Sum of three numbers
    """
    ...
```

</div>

<v-click>

Use cases for AI:
- use AI to generate docstrings, or
- docstrings become **natural language prompts** for code generation

</v-click>

::right::

<div class="p-4">

```python
> help(add3)

add3(a, b, c)
    Add three numbers

    A longer description of the
    function, if one is necessary.

    Params:
        a, b, c: numbers to add

    Returns:
        Sum of three numbers
```

</div>

---
transition: none
---

# Writing Clean Code

## Documentation — scaffolding

<br>

<div class="w-3/4 p-4">

Using comments as **scaffolding for AI**:

```python
# Read data from file
...

# Calculate word count and add 10
...

# Print final word count
...
```

</div>

---
transition: none
---

# Writing Clean Code

## Documentation — scaffolding

<div class="w-3/4 p-4">

Using comments as **scaffolding for AI**:

```python
# Read data from file
data = read_data(filename)

# Calculate word count and add 10
word_count = calculate_word_count(data)
word_count = word_count + 10

# Print final word count
print(word_count)
```

AI can use this scaffold to implement each step — each comment is a prompt
</div>

---
transition: none
---

# Writing Clean Code

## Documentation — scaffolding

<div class="w-3/4 p-4">
Tidy-up — consolidate comments:

```python
# Report word count
data = read_data(filename)
word_count = calculate_word_count(data)
word_count = word_count + 10
print(word_count)
```

</div>

---

# Writing Clean Code

## Documentation — annotations

<div class="w-3/4 p-4">

Real world example (useful):

```python
# we don't use path.splitext to also handle extensions like .cdt.dpa
filename, ext = filepath.split(".", maxsplit=1)
```

</div>

<br>

::: center

<v-click>
Don't state <b>what</b> <i>(the code already tells us that)</i><br>
explain <b>why</b> <i>(provide context — for both humans and AI)</i>
</v-click>

:::

---

# Writing Clean Code

## Coding with AI

<div class="h-4" />

<v-clicks>

- AI *can* be very helpful in checking the logic, consistency and overall correctness of your code
- AI *can* help to restructure long scripts into shorter, more modular functions
- AI *can* help spot (and fix) bugs in your code
- **BUT** AI *does not have your understanding of the problem*, and may just as easily introduce bugs
- AI can restructure your code, but in-so-doing change the logic in subtle ways

</v-clicks>

---

# Writing Clean Code

## Coding with AI

<div class="h-4" />

::center

**Professional Software Developers Don't Vibe, They Control:<br />
AI Agent Use for Coding in 2025**

Through field observations (N=13) and qualitative surveys (N=99), we find that while<br/><b>experienced developers value agents as a productivity boost,<br />they retain their agency in software design and implementation</b><br/>out of insistence on fundamental software quality attributes, employing<br/>strategies for controlling agent behavior leveraging their expertise.

[Huang et al. 2025](https://arxiv.org/html/2512.14012v1)

::

<v-clicks>

- Always review AI-generated code carefully
- Test thoroughly!
- Clean code practices give you the **control** that professionals insist on

</v-clicks>

---

# Recording computational steps

<span />

**A comment on workspaces in JuPyter / Matlab / R:**
- A script / program records a series of computational steps
- Workspaces are designed to resume previous sessions (persistent state)
- This can introduce manual steps that are <span v-mark.underline.orange="1">not recorded</span>, making it <span v-mark.underline.red="2">impossible to reproduce</span> the previous result(s)

**Regularly 'run from the top'**
- Select 'Run All' cells or the equivalent when you start work for the day
- Fix any problems before you continue creating
- If it doesn't take long to run, *always* run all cells

---
layout: instruction
---

# Clean Code + AI exercise

::left::

::center
AI in a flat vs structured repo
::

::right::
Navigate to the project:<br />
<small>
<a href="https://github.com/OxfordRSE/softeng-daycourse-cleancode">github.com/OxfordRSE/softeng-daycourse-cleancode</a>
</small>

- Open in Codespaces
- Ask an AI to add a new feature to the messy `fixme.py`
- Then organise the files properly
- Ask the AI again — compare output quality
- Run the linter: `pip install ruff && ruff check`
- Fix the AI's style issues with: `ruff format`

---
layout: instruction
---

# Clean Code + AI exercise

::left::

::center
Type annotations as AI constraints
::

::right::

- Open `main.py`
- Ask AI to implement a function described without types
- Then add full type annotations and ask again
- Compare: did the AI get the types right the first time?
- Scaffolding exercise:
  - Write a comment listing steps (e.g. "load data, compute stats, plot results")
  - Ask AI to implement each step
  - Notice how the comments act as prompts
