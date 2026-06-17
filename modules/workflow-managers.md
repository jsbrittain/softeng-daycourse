---
routeAlias: "workflow-managers"
---

# Workflow Managers

## AI-assisted pipeline design

<v-clicks>

- Manage larger pipelines
- Workflow managers encapsulate complex pipelines
- Can speed up analyses by preventing redundant computation
- **AI can help write workflow rules** — but you need to understand the DAG

</v-clicks>

<v-click>

**This is not new.** Workflow managers encoded reproducibility and DAG-based execution long before AI. The DAG concept is the same; AI just helps you build and maintain it — and makes reproducibility even more critical.

</v-click>

---

# Snakemake

<span />

A tool to create **reproducible** and **scalable** data analyses.

Workflows are described via a human **readable, Python based language**.

They can be **seamlessly scaled** to server, cluster, grid and cloud environments, without the need to modify the workflow definition.

Workflows can entail a **description of required software**, which will be automatically deployed to any execution environment.

<div class="h-8" />

::center
<img src="../img/snakemake-logo.png" width="400">
::

---

# AI + Workflow Managers

<div class="h-4" />

<v-clicks>

- **Describe your pipeline in prose** → AI generates Snakefile rules
- **AI can write individual rules** from function descriptions
- **AI can debug workflow failures** — give it the error, get a fix
- **AI can optimise for parallelisation** — add wildcards, split steps
- But: **you must understand the DAG** to verify correctness

</v-clicks>

---

# Workflow Managers

- Manage larger pipelines
- Maintains the **Recording Computational Steps** philosophy
- Workflow managers encapsulate complex pipelines
- Can speed up analyses by preventing redundant computation

---
layout: instruction
---

# Prose-to-Snakefile exercise

::left::

::center
Describe pipeline, AI generates it
::

::right::

- Navigate to the course workflows repository:
  [github.com/OxfordRSE/softeng-daycourse-workflows](https://github.com/OxfordRSE/softeng-daycourse-workflows)
- Start a new codespace
- Write a prose description of a multi-step analysis:
  - "First, generate 100 documents with random words. Then count word frequencies in each. Finally produce a chart of the top words."
- Ask AI to generate a Snakefile
- Install snakemake: `pip install snakemake`
- Run it: `snakemake --cores 1`
- Did AI get the DAG right?

---

# A simple workflow

Let's create a frequency plot of the words in a file.

<br />

Use a script to count the frequency of words in the file and output the results:

```bash
python count_words.py -in data/doc.txt -out output/wc.txt
```

Form a bar chart of the word frequencies, and save it to `words_chart.txt`:
```bash
python words_chart.py
```

---
transition: "none"
---

# Snakemake

<span />

Command:
```bash
python count_words.py -in data/doc.txt -out output/wc.txt
```

<br />

<v-click>
Translated to Snakemake:

```python
rule count_words:
    input:
        "data/doc.txt"
    output:
        "output/wc.txt"
    shell:
        """
        python count_words.py -in {input} -out {output}
        """
```

</v-click>

---

# Snakemake

<span />

Command:
```bash
python words_chart.py
```

<br />

<v-click>
Translated to Snakemake:

```python
rule words_chart:
    input:
        "output/wc.txt"
    output:
        "words_chart.txt"
    script:
        "words_chart.py"
```

</v-click>

---
layout: two-cols-header
class: "gap-4"
---

# Snakemake complete workflow

::left::

```python
rule all:
    input:
        "words_chart.txt"

rule count_words:
    input:
        "data/doc.txt"
    output:
        "output/wc.txt"
    shell:
        """
        python count_words.py -in {input} -out {output}
        """

rule words_chart:
    input:
        "output/wc.txt"
    output:
        "words_chart.txt"
    script:
        "words_chart.py"
```

::right::

<v-click>

```bash
snakemake --snakefile onefile.smk --cores 1
```

Open `words_chart.txt` to see the results.

</v-click>

---

# Snakemake — multiple files

What if we have more than one file?

```bash
python generate.py -n 100 -w 1000
```

<v-click>

AI can add wildcards to scale the workflow:

```python
rule count_words:
    input:
        "data/doc{n}.txt"
    output:
        "output/wc{n}.txt"
    shell:
        """
        python count_words.py -in {input} -out {output}
        """
```

</v-click>

---

# Snakemake — selective rebuilds

- Only runs rules when their inputs (or scripts) are **newer than their outputs**
- If nothing is out of date, snakemake does nothing

- Parallelisation
  ```
  snakemake --cores 8
  ```

---
layout: instruction
---

# AI-assisted workflow exercise

::left::

::center
Fix an AI-generated workflow
::

::right::

- Ask AI to create a Snakefile for a 3-step pipeline
- **Intentionally introduce a bug**: wrong input file name, circular dependency
- Ask AI to identify and fix the bug
- If AI can't fix it — can you?

---
layout: instruction
---

# AI-assisted workflow exercise

::left::

::center
AI optimises for parallel execution
::

::right::

- Start with a linear Snakefile (one file at a time)
- Ask AI to modify it to use wildcards
- Compare execution time:
  ```bash
  time snakemake --cores 1
  time snakemake --cores all
  ```
