---
routeAlias: "continuous-integration"
---

# Continuous Integration (CI)

## The safety net for AI-generated code

AI generates code faster than you can review it.

**CI is your first line of defence.**

- Every AI-generated PR triggers CI before human review
- CI catches issues that human review misses
- CI enforces the *constraints* (tests, style, types) you defined earlier

**This is not new.** CI was always about catching breakage early when humans integrated their work. With AI, the same principle applies — the pace is just faster, so the safety net matters more.

---

# Continuous Integration (CI)

- **Definition**: Continuous Integration (CI) is an automated process for verifying and integrating code changes.
- **Objective**: To detect and resolve issues early by frequently testing and integrating code changes.
- **Importance**: Ensures compatibility, functionality, and reduces the introduction of unexpected problems.

---

# Continuous Integration (CI)

## Challenges Without CI

- **Compatibility**: Ensuring code works across various OS, software versions, and hardware.
- **Consistency**: Avoiding dependencies on specific user data or development machine configurations.
- **Collaboration**: Managing code changes in tandem with other developers — **or AI** — without conflict.

<br />

## Benefits of Implementing CI

- **Efficiency**: Swift detection and resolution of integration issues.
- **Quality Assurance**: Automated tests and builds ensure code quality and functionality.
- **Reproducibility**: Standardised and automated build/deploy processes ensure consistent output.
- **AI safety net**: Automatically tests AI-generated code before human review

---

# Continuous Integration (CI)

<div class="h-6" />

## Key Principles

- **Single Source Repository**: Maintain all code and dependencies in a shared repository.
- **Automate the Build**: Automatically compile, package, and create installers for code.
- **Self-testing Builds**: Employ automated tests to validate code functionality post-build.
- **Gate for AI**: Every AI contribution must pass CI before merging

---

# CI and AI: Why This Matters More Than Ever

<div class="h-4" />

<v-clicks>

- **AI writes code in seconds** — you need automated verification in seconds too
- **AI makes plausible mistakes** — CI catches what looks right but isn't
- **AI doesn't know your test suite** — CI ensures tests are run and pass
- **AI might break existing behaviour** — regression tests in CI catch this
- **CI = trust mechanism**: passing CI builds confidence in AI output

</v-clicks>

---

# Continuous Integration Tools

<div class="h-12" />

<div class="grid grid-cols-[50px_auto] gap-4 items-center" v-mark.box.red="1">
  <img src="../img/github.png" width="50px" />
  <div>
    <h2 class="text-xl font-semibold">GitHub Actions</h2>
    A CI/CD tool within GitHub’s platform.
  </div>
</div>
<div class="h-6" />

<div class="grid grid-cols-[50px_auto] gap-4 items-center">
  <img src="../img/travis-logo.png" width="50px" />
  <div>
    <h2 class="text-xl font-semibold">Travis</h2>
    A popular CI service used in various open-source projects.
  </div>
</div>
<div class="h-6" />

<div class="grid grid-cols-[50px_auto] gap-4 items-center">
  <img src="../img/appveyor-logo.png" width="50px" />
  <div>
    <h2 class="text-xl font-semibold">AppVeyor</h2>
    CI/CD tool that allows building, testing, and deploying applications.
  </div>
</div>
<div class="h-6" />

*Note*: Each tool has unique and common features. Exploring multiple options is advised.

---
layout: instruction
---

# Continuous Integration

::left::

::center
<div class="border border-color-black">
<img src="../img/github-action-pytest.png" width="100%" />
</div>
::

<div class="absolute top-43 left-70 w-47 border border-color-black">
<img src="../img/github-issues.png" />
</div>

::right::

Follow-along:
- Add continuous integration to your repository (*Action: "Python Application" [ruff, pytest]*)
- Push changes to your repository
- (Optional) Make a change that breaks your tests, then fix them
- **Ask AI to fix the failing tests** — does AI understand what went wrong?

---
layout: two-cols-header
class: "gap-4"
---

# Platform support?

::left::

::center
"… density functional theory nuclear magnetic resonance calculations established the relative configurations of compounds 1 and 2 and revealed that the calculated shifts **depended on the operating system** when using the "Willoughby–Hoye" Python scripts to streamline the processing of the output files, a previously unrecognized flaw that could lead to incorrect conclusions."
::

<div class="absolute border border-color-black top-95 left-27 w-80 p-4 text-center">
The issue was due to
<b>different sorting of file names</b>
on <b>different operating systems</b>
</div>

::right::

::center
<img src="../img/neupane2019.png" width="80%"/>
::

<div class="h-4" />

::center
<div class="text-sm">
Organic Letters, October 8 2019<br>
https://doi.org/10.1021/acs.orglett.9b03216
</div>
::

---
layout: two-cols-header
---

# Platform support with CI

::left::

You (or an AI) might generate code that works on your machine but not on others.

**CI matrix testing** catches this:

```yaml
jobs:
  build:
    runs-on: ${{ matrix.os }}
    strategy:
        matrix:
            os: [ubuntu-latest, windows-latest, macos-latest]
            python-version: ["3.9", "3.10", "3.11", "3.12"]
```

::right::

| | ubuntu | windows | macos |
|--|:--:|:--:|:--:|
| python 3.9 | ❌ | ❌ | ❌ |
| python 3.10 | ✅ | ❌ | ✅ |
| python 3.11 | ✅ | ❌ | ✅ |
| python 3.12 | ✅ | ❌ | ✅ |

---
layout: instruction
---

# CI exercise: AI writes CI config

::left::

::center
AI generates a workflow — fix it
::

::right::

- Ask AI to write a GitHub Actions workflow for a Python project
- Take the config and create `.github/workflows/test.yml`
- **Intentionally add a mistake** (wrong Python version, missing step)
- Push to GitHub — CI fails
- Ask AI to debug the failure
- Fix the workflow so it passes

---
layout: instruction
---

# CI exercise: AI breaks, CI catches

::left::

::center
CI catches an AI bug
::

::right::

- Ask AI to add a feature to your repository that:
  - Depends on a package not in `requirements.txt`
  - Uses an API that's platform-specific
- Push the AI-generated code
- Watch CI fail
- Fix based on CI output
