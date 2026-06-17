---
layout: two-cols-header
rightClass: ""
routeAlias: "version-control"
---

# Version Control as Coordination

<span />

## Git is how you coordinate with AI

::left::

- AI works on branches; you review on `main`
- Commits are atomic units of AI-generated change
- History lets you **revert** bad AI output
- PRs are the human–AI code review gateway

<v-click>

**This is not new.** Version control was built for collaboration between humans. Branches, commits, and PRs let teams work together without stepping on each other. AI agents are now collaborators too, and the same workflow applies.

</v-click>

<v-click>

AI can write Git commands — but **you** decide what to commit and merge.

</v-click>

::right::

::center

<img src="../img/phd-final.gif" alt="PhD comic: 'Final Version'" width="65%" />

::

---

# Code management & collaboration

::centralise::

::center

<i>"If you're not using version control,<br>
whatever else you might be doing with a computer,<br>
it's not science."</i><br>
<br>
Greg Wilson, SWC<br/><div style="font-size: 0.8rem;"><i>First Executive Director of Software Carpentry</i></div>

::

---

# Version Control

<div class="h-5" />

- These skills will save you time
- Always assume others will use and develop your software — **including AI agents**
- Be clear on requirements and assume they will change
- Funders are increasingly expecting software outputs to be sustainable and reusable

---

# Version Control

<span />

Three pillars — all still essential with AI:

- **Backup** — AI can lose context; Git preserves everything
- **Reproducibility** — pin exact code for each result
- **Collaboration** — coordinate human + AI contributions

---

# How do version control tools work?

<div class="h-10" />

- Start by storing the base version of the file
- After that, only changes are stored
- Like instructions for building lego

::centralise::

::center

<img src="../img/commit-doc.png" alt="Version control collaboration">

::

---
layout: two-cols-header
---

# Staging and commits

::centralise::

::left::

<div style="position: relative; top: 0px; width: 40%; height: auto; margin: auto;">

  <div class="flex flex-col items-center space-y-10">
    <div class="flex space-x-1">
    <div class="w-50 h-15 bg-orange-500 text-white flex items-center justify-center rounded">Working directory</div>
    </div>
    <div class="flex space-x-1">
      <div class="w-50 h-15 bg-amber-500 text-white flex items-center justify-center rounded">Staging area</div>
    </div>
    <div class="flex space-x-1">
      <div class="w-50 h-15 bg-yellow-500 text-white flex items-center justify-center rounded">Repository</div>
    </div>
  </div>

  <FancyArrow
    x1="-14"
    y1="30"
    x2="-75"
    y2="65"
    arc="-0.4"
    head-size="15"
  />
  
  <div class="absolute top-16.5 left--30">
    <code>git add</code>
  </div>
  
  <FancyArrow
    x1="-75"
    y1="95"
    x2="-14"
    y2="130"
    arc="-0.4"
    head-size="15"
  />
  
  <FancyArrow
    x1="188"
    y1="130"
    x2="250"
    y2="165"
    arc="0.4"
    head-size="15"
  />

  <div class="absolute top-41.5 left-50 w-30">
    <code>git commit</code>
  </div>
  
  <FancyArrow
    x1="250"
    y1="195"
    x2="188"
    y2="230"
    arc="0.4"
    head-size="15"
  />
  
</div>

::right::

<div class="h-10" />

- **Staging**: Select files to include in the next Commit (`git add`)
- **Commit**: Save the staged files to the repository (`git commit`) with a message describing the changes
- AI can generate both commands, but **verify what AI staged** — did it include generated files?

---

# Git Branches + Feature Branch Workflow

<div class="flex flex-1 items-end justify-between h-64 w-100%">

<div class="flex flex-col justify-between items-center w-45 h-100% text-sm">
Commit to main branch

```mermaid {scale: 0.8}
gitGraph BT:
  commit id: "First"
  commit id: "Second"
```

</div>

<div v-click class="flex flex-col justify-between items-center w-45 h-100% text-sm">
Create a new branch, make commits to it

```mermaid {scale: 0.8}
gitGraph BT:
  commit id: "First"
  commit id: "Second"
  branch feature
  commit id: "New thing"
```

</div>

<div v-click class="flex flex-col justify-between items-center w-45 h-100% text-sm">
Changes independent of main branch

```mermaid {scale: 0.8}
gitGraph BT:
  commit id: "First"
  commit id: "Second"
  branch feature
  commit id: "New thing"
  checkout main
  commit id: "Other work"
```

</div>

<div v-click class="flex flex-col justify-between items-center w-45 h-100% text-sm">
Merge commit

```mermaid {scale: 0.8}
gitGraph BT:
  commit id: "First"
  commit id: "Second"
  branch feature
  commit id: "New thing"
  checkout main
  commit id: "Other work"
  merge feature
```

</div>

</div>

<br>

- Main branch for tested, stable code; feature branches for AI experiments
- **AI should always work on a branch** — easy to discard bad output

---

# Git Branches

::centralise::

::center
```mermaid
gitGraph
  commit id: "A"
  branch develop
  commit id: "B"
  branch big_feature
  commit id: "C"
  checkout develop
  commit id: "D"
  checkout main
  merge develop tag: "v1.1"
  checkout develop
  branch small_feature
  commit id: "E"
  commit id: "F"
  checkout big_feature
  commit id: "G"
  checkout develop
  merge small_feature
  checkout main
  merge develop tag: "v1.2"
  checkout big_feature
  commit id: "H"
```
::

---

# AI and Version Control

<div class="h-4" />

<v-clicks>

- AI can **write Git commands** — but you need to understand the concepts
- AI can **generate commit messages** — evaluate quality, don't accept blindly
- AI can **resolve merge conflicts** — but may not understand semantics
- **Branch strategy**: AI experiments go on feature branches
- **Review AI's Git history**: did it commit the right files? Good messages?

</v-clicks>

---
layout: instruction
---

# Version Control + AI

::left::

::center
AI-generated commit messages
::

::right::
::small

- Make a change to a file
- Ask AI to generate a commit message: `git commit -m "<AI message>"`
- Evaluate: is it accurate? descriptive? helpful?
- Now ask AI to generate a **misleading** commit message
- Lesson: **AI can help or deceive** — you must review

::

---
layout: instruction
---

# Version Control + AI

::left::

::center
Branches and merging
::

::right::
::small

- Create a feature branch: `git switch -c ai-experiment`
- Ask AI to make changes and commit them
- Switch to main, make a conflicting change
- Ask AI to merge and resolve the conflict
- Switch branches and take a look at the differences: `git switch main`
- Merge your feature branch into main: `git merge ai-experiment`
- Review what AI did

::
