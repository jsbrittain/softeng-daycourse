---
routeAlias: "testing"
---

# Testing in the AI Era

<span />

## Tests are the contract you give AI

<v-clicks>

- Tests define what "correct" means
- AI needs specifications — tests are **executable specifications**
- AI can generate code from test cases alone
- **Without tests, you cannot trust anything AI produces**

</v-clicks>

<v-click>

**This is not new.** Tests were always about verification and regression prevention. What's changed is the speed at which code is produced — making tests more critical, not less.

</v-click>

---

# All Software has Issues

<span />

Code will always have issues
- e.g. bugs, things we want to add or improve

<div class="h-4" />

With AI, code is generated faster — **more code, more potential issues**

It's not enough to know about them, we need to <span v-mark.underline.orange="1">manage</span> them
- Identify, record, prioritise

---

# Testing

<div class="h-5" />

Humans are fallible! Our software will contain defects
  - In requirements, design, as well as code
  - 1-10-150 hours to fix in design/development/production
  - Microsoft Study estimated 10-20 defects per 1000 lines of code

<div class="h-5" />

<v-click>

**AI-generated code introduces a new challenge**: plausible-looking but wrong code
  - AI writes code that *looks* correct but has subtle bugs
  - AI *confirms its own mistakes* if it writes both code and tests

</v-click>

---
layout: two-cols-header
---

# Repercussions of Software Bugs

## Basic science

::left::

<div class="h-5"></div>

- Highly-cited papers published on multidrug resistance transporters (2001 - 2010)
- Results couldn't be reproduced - 5 retractions
- Caused by error in an internal software utility
- Flipped two columns of data, inverting electron-density map used to derive protein structure

::right::

::center

<div class="h-10"></div>

<img src="../img/chem.png" alt="Chemistry" width="60%" />

*"I didn't question it then. Obviously now I check it all the time."* - Geoffrey Chang

::

---
layout: two-cols-header
---

# Repercussions of Software Bugs

## AI makes this worse

::left::

AI generates code faster, but:
- AI may **hallucinate APIs** that don't exist
- AI may **miss edge cases** that a domain expert would catch
- AI may **introduce security vulnerabilities**
- AI **cannot reason about your specific research domain**

::right::

<v-click>

The only defence: **automated tests that encode your domain knowledge**

</v-click>

---

# The Role of Automation in Software Testing

<div class="h-5" />

Manual testing *is* necessary.

<v-click>

However...
- Prone to error
- Can be time-consuming, expensive
- **Cannot keep up with AI code generation speed**

</v-click>

<v-click>

Automated testing involves writing code to test software
- Computers are great at repetitive tasks!
- Define complex, repeatable processes with fewer errors
- **Tests become the specification you give to AI**

</v-click>

---

# Automated Testing

<span />

**Unit tests**: Test specific units of functionality, ensuring expected outputs from given inputs.

<v-click>

```python
def celsius_to_fahrenheit(celsius):
    return 32 + 1.8 * celsius

celsius_to_fahrenheit(1.0)
> 33.8

celsius_to_fahrenheit(12.34)
> 54.212
```

</v-click>

<v-click at="2">
<div>

```python {none|all|none}
def test_celsius_to_fahrenheit():
    assert celsius_to_fahrenheit(1.0) == 33.8
    assert celsius_to_fahrenheit(12.34) == 54.212
```

</div>
</v-click>

<v-click at="3">

```python
import numpy as np

def test_celsius_to_fahrenheit():
    assert np.isclose(celsius_to_fahrenheit(1.0), 33.8)
    assert np.isclose(celsius_to_fahrenheit(12.34), 54.212)
```

</v-click>

---
layout: two-cols-header
class: "gap-4"
leftClass: "justify-center"
rightClass: "justify-center ml-10"
---

#  Code breakdown

::left::

```python {all|1|2-11|12|14-17}
def add3(a, b, c):
    """Add three numbers

    This code adds three numbers together

    Parameters:
        a, b, c: numbers to add

    Returns:
        Sum of three numbers
    """
    ...


def test_add3(a, b, c):
    assert add3(1, 2, 3) == 6
    assert add3(1, 2, None) is None
```

::right::

<v-click at="1">
<h3>Code signature</h3>
<div class="text-sm">How to run the function — AI reads this</div>
<div class="h-5"></div>
</v-click>

<v-click at="2">
<h3>Documentation</h3>
<div class="text-sm">What the function does — AI reads this</div>
<div class="h-5"></div>
</v-click>

<v-click at="3">
<h3>Implementation</h3>
<div class="text-sm">AI can generate this from the test + docs</div>
<div class="h-5"></div>
</v-click>

<v-click at="4">
<h3>Test</h3>
<div class="text-sm">Defines behaviour — the <b>most important input for AI</b></div>
</v-click>

---

# Test-First AI Development

<span />

A new workflow for coding with AI:

1. **Write a test** that defines the desired behaviour
2. **Ask AI to implement** just enough code to make the test pass
3. **Run the test** — it should pass
4. **Write more tests** for edge cases
5. **Ask AI to handle new cases** — iterate

<v-click>

This is TDD (Test-Driven Development) adapted for AI:
- The test is the **prompt**
- The test is the **verification**
- The test is the **documentation**

</v-click>

---
transition: "none"
---

# Automated Testing

<div>
<b>Unit tests</b>: Test specific units of functionality, ensuring expected outputs from given inputs.
</div>

---
transition: "none"
---

# Automated Testing

<div class="text-gray-400">
<b>Unit tests</b>: Test specific units of functionality, ensuring expected outputs from given inputs.
</div>

<b>Integration (functional) tests</b>: Test functional paths through the code, especially useful for exposing faults in unit interactions.

---
transition: "none"
---

# Automated Testing

<div class="text-gray-400">
<b>Unit tests</b>: Test specific units of functionality, ensuring expected outputs from given inputs.

<b>Integration (functional) tests</b>: Test functional paths through the code, especially useful for exposing faults in unit interactions.
</div>

<b>Regression tests</b>: Ensure unchanged program output despite code modifications.

<br />

::center

<v-click>
When working with a <b>legacy</b> codebase,
<br />start with a few <b>regression tests</b> to ensure
<br />that the output is not changing.
</v-click>

<br />

<v-click>
<br />Then, start adding <b>unit tests</b> for
<br />new features or bug fixes.
</v-click>

---

# AI and Testing

<div class="h-4" />

::center

When working with <b>AI</b>, verify the code
<br />behaves as expected with <b>tests</b>.

<v-click>
<br />When relying heavily on AI,
<br />allow it to write <b><i>either</i></b> code <b><i>or</i></b> some tests.
<br /><b>Not both</b> — this defeats the purpose of testing!
</v-click>

<v-click>

<br />Why? AI has **confirmation bias** — it writes tests that pass on its own flawed code.

</v-click>

::

---

# PyTest

<span />

**pytest**: a framework for automated testing

<v-click>

- Automatically finds any function starting in `test_` or ends in `_test`
- Produces a report indicating test status
- Many advanced features (e.g. exception testing, mocks, fixtures)
- Install with `pip install pytest`
- Run with `pytest` (or `pytest -v` for an itemised view)

</v-click>

<v-click>

Testing investment should match the software's complexity and usage

</v-click>

---
layout: instruction
---

# Testing with AI

::left::

::center
Test-first AI exercise
::

::right::

- Instructor: demo pytest install and running the test suite
- **Write tests first** for the `smoothie` function in `smoothie.py`
- Then ask AI to implement the function to pass the tests
- **Then let AI write its own tests** — compare quality
- Write a test that fails (to see the output)
- Think of edge cases that can be added to the test suite

---
layout: instruction
---

# Testing with AI

::left::

::center
AI writes both code and tests
::

::right::

- Ask AI to write a function **and** its tests
- Now intentionally introduce a bug in the function
- Run the tests — do they catch the bug?
- **AI often writes tests that pass despite bugs** (confirmation bias)
- Lesson: always have a human write tests, or write tests *before* asking AI for code
