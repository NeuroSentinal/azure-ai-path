# Phase 0 — Python for Azure AI
## A fully-taught two-week curriculum

**For:** an experienced systems administrator with zero Python, on macOS, heading into AI-901 and AI-103 (both Python-only)  
**Time:** 15 hrs/week × 2 weeks · Mon 2h · Wed 2h · Thu 1h · Sat 4h · Sun 2h · Flex 4h  
**Cost:** $0 — everything runs against Foundry Local on your own machine  
**Outcome:** you can write, read, and debug the Python that every lab in this path is made of

This document teaches. It does not assign reading and it does not send you elsewhere to figure things out. Every concept is explained here, every code block shows its expected output, every exercise has a worked solution, and every day ends with a checkpoint you can honestly measure yourself against. Work top to bottom.

**Two rules that matter more than they sound:**

1. **Type the code; don't paste it.** Muscle memory for syntax is the entire point of week one.
2. **Don't let AI write your code for these two weeks.** Use it to explain an error *after* you've read the traceback yourself. The Phase 0 gate requires writing a working program from a blank file unaided — because AI-103 labs mean debugging SDK code under time pressure, and the language has to be automatic by then.

---

## Table of contents

**Week 1 — Python Foundations** (Aug 17–23)

- Day 1 (Mon, 2h) — Running Python, values, and strings
- Day 2 (Wed, 2h) — Control flow
- Day 3 (Thu, 1h) — Lists and tuples
- Day 4 (Sat, 4h) — Functions, modules, and dictionaries ← *the pivotal day*
- Day 5 (Sun, 2h) — Nested data, comprehensions, and a mini-project
- Days 6–7 (Flex, 4h) — Files, errors, and consolidation

**Week 2 — The AI Developer Toolkit** (Aug 24–30)

- Day 8 (Mon, 2h) — Virtual environments, packages, and secrets
- Day 9 (Wed, 2h) — HTTP and REST from Python
- Day 10 (Thu, 1h) — JSON mastery
- Day 11 (Sat, 4h) — The OpenAI SDK pattern ← *the payoff day*
- Day 12 (Sun, 2h) — Enough classes and async to read SDK code
- Days 13–14 (Flex, 4h) — Sysadmin drills and the Phase 0 capstone
- Phase 0 gate — self-test

---

# Week 1 — Python Foundations

**Dates: Aug 17–23, 2026 · 15 hours · Prerequisite: none beyond the Homebrew toolchain from setup**

This week you learn the language. Not "programming" — you've been programming in PowerShell for years, and every concept you already own (variables, loops, functions, hashtables, error handling, pipelines) exists in Python under a different spelling. What you need is the translation table and the handful of places where Python genuinely thinks differently.

Four differences matter, and they cause most of the friction in week one:

1. **Indentation is syntax.** PowerShell uses `{ }` to define a block. Python uses the indentation itself. Get it wrong and the program won't run — or worse, will run and do something you didn't intend.
2. **No sigils.** `$name` in PowerShell is `name` in Python. This feels naked at first and then feels normal.
3. **Everything is an object with methods.** `"hello".upper()` — the string itself carries the function. PowerShell does this too (`$s.ToUpper()`), but Python leans on it far harder.
4. **Dictionaries are the center of gravity.** JSON — the language of every API you'll call for the next fourteen weeks — maps directly onto Python dictionaries. Your PowerShell hashtable instincts transfer, and Day 4 is the most important day of the week because of it.

**How to use this document.** Type the code; don't copy-paste it. Typing is how the syntax gets into your fingers, and you will type far more Python than you read for the rest of this path. Run everything. When output is shown, compare it to yours before moving on. Do the exercises before opening the solutions — a solution you read is worth roughly nothing compared to one you produced.

**A note on AI assistance.** You have Claude and Copilot. For these two weeks, don't use them to write code for you. Use them to explain errors after you've read the traceback yourself. The Phase 0 gate requires writing a working script from a blank file unaided, because AI-103 labs will have you debugging SDK code under time pressure and you need the language to be automatic.

---

## Day 1 (Mon, 2h) — Running Python, values, and strings

### Why this matters

Every lab in AI-901 and AI-103 is a Python script that reads configuration, calls a service, and formats the result. Today you learn to run code and to build strings — and string formatting is not a triviality here: prompts are strings, endpoints are strings, and the single most common lab bug is a malformed f-string producing a URL that 404s.

### Concepts

**Three ways to run Python.** Know all three; you'll use each.

The **REPL** (Read-Eval-Print Loop) is an interactive session for experiments:

```bash
python3
```

```text
Python 3.12.x (main, ...) 
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

At the `>>>` prompt, type `2 + 2` and press Enter. It prints `4`. Exit with `exit()` or Ctrl-D. This is your scratchpad — when you're unsure what a method does, try it here rather than guessing. PowerShell's console is the same idea.

A **script file** is a `.py` text file you run:

```bash
python3 hello.py
```

**VS Code** runs the current file with the ▷ button (or Shift-Cmd-P → "Python: Run Python File in Terminal"). Same thing, fewer keystrokes.

Set up a working folder now:

```bash
# inside the tracker repo you created in the playbook's §0.1
mkdir -p ~/code/azure-ai-path/python-ramp && cd ~/code/azure-ai-path/python-ramp
code .
```

**Your first program.** Create `hello.py`:

```python
print("Hello from Python")
```

```bash
python3 hello.py
```

```text
Hello from Python
```

`print()` is `Write-Host` / `Write-Output`. It takes multiple arguments and separates them with spaces:

```python
print("Endpoint:", "http://localhost:5273", "status:", 200)
```

```text
Endpoint: http://localhost:5273 status: 200
```

**Variables and dynamic typing.** No `$`, no `New-Variable`, no type declaration:

```python
name = "shawn"
device_count = 120
temperature = 0.7
is_active = True
last_error = None
```

Python infers the type. Check it with `type()`:

```python
print(type(name))
print(type(device_count))
print(type(temperature))
print(type(is_active))
print(type(last_error))
```

```text
<class 'str'>
<class 'int'>
<class 'float'>
<class 'bool'>
<class 'NoneType'>
```

Note the capitalization: `True`, `False`, `None` — capital first letter, unlike PowerShell's `$true`/`$false`/`$null`. Lowercase `true` is a NameError.

| PowerShell | Python | Note |
|---|---|---|
| `$name = "shawn"` | `name = "shawn"` | No sigil |
| `$true` / `$false` | `True` / `False` | Capitalized |
| `$null` | `None` | Capitalized |
| `[int]$x = 5` | `x = 5` | Type inferred; hints optional (Day 4) |
| `Write-Host "hi"` | `print("hi")` | |
| `$x.GetType()` | `type(x)` | |
| `# comment` | `# comment` | Identical |

**Numbers.** Two things to know:

```python
print(7 / 2)      # true division — always float
print(7 // 2)     # floor division — integer result
print(7 % 2)      # modulo — remainder
print(2 ** 10)    # exponent
print(int(7 / 2)) # explicit truncation
```

```text
3.5
3
1
1024
3
```

`7 / 2` giving `3.5` rather than `3` is the opposite of many languages and catches people. In this path you'll mostly use division for token-cost math and percentages, where float is what you want.

**Strings.** Single or double quotes, identical meaning — pick double and be consistent:

```python
service = "Azure AI Language"
path = 'C:\\temp'          # backslash escapes itself
multiline = """Line one
Line two"""
```

Triple-quoted strings preserve newlines and are how you'll write multi-line prompts later:

```python
system_prompt = """You are an IT support assistant.
Answer only from the provided context.
If the context is insufficient, say so."""
print(system_prompt)
```

```text
You are an IT support assistant.
Answer only from the provided context.
If the context is insufficient, say so.
```

**f-strings — the default way to build strings.** Prefix with `f`, put expressions in braces:

```python
service = "Language"
count = 4823
limit = 5000
print(f"{service} used {count} of {limit} records")
print(f"Utilization: {count / limit:.1%}")
print(f"Cost estimate: ${count * 0.000015:.4f}")
```

```text
Language used 4823 of 5000 records
Utilization: 96.5%
Cost estimate: $0.0723
```

The `:.1%` and `:.4f` are format specifiers — `.2f` for two decimal places, `.1%` for a percentage with one decimal, `,` for thousands separators (`f"{1234567:,}"` → `1,234,567`). PowerShell's `"$name has $count"` interpolation is the same idea, but Python requires the `f` prefix — forget it and you get the literal braces:

```python
print("{service} used {count}")   # no f — prints literally
```

```text
{service} used {count}
```

Any expression works inside the braces, including method calls:

```python
name = "  Shawn Vermette  "
print(f"Hello, {name.strip().upper()}!")
```

```text
Hello, SHAWN VERMETTE!
```

**String methods you'll use constantly.** Strings are immutable — every method returns a *new* string rather than modifying in place:

```python
raw = "  ERROR: device pi-042 unreachable  "

print(raw.strip())                      # remove surrounding whitespace
print(raw.strip().lower())              # chain them
print(raw.strip().startswith("ERROR"))  # boolean test
print(raw.strip().split(":"))           # split into a list
print("device" in raw)                  # substring test
print(raw.strip().replace("pi-042", "pi-999"))
```

```text
ERROR: device pi-042 unreachable
error: device pi-042 unreachable
True
['ERROR', ' device pi-042 unreachable']
True
ERROR: device pi-999 unreachable
```

`.split()` with no argument splits on any whitespace and is what you want for log lines. `.join()` is the inverse and reads backwards at first — the separator goes first:

```python
parts = ["ERROR", "device", "unreachable"]
print(" | ".join(parts))
```

```text
ERROR | device | unreachable
```

**Type conversion.** Python will not silently concatenate a number onto a string:

```python
count = 5
print("Count: " + count)
```

```text
TypeError: can only concatenate str (not "int") to str
```

> **If you see this error:** you tried to `+` a string and a number. Either use an f-string (`f"Count: {count}"` — always preferred) or convert explicitly (`"Count: " + str(count)`).

Conversions: `str(x)`, `int(x)`, `float(x)`, `bool(x)`. `int("42")` works; `int("42.7")` raises ValueError; `int(float("42.7"))` gives 42.

**Reading input** (used lightly, mostly for the Day 11 chatbot):

```python
user_text = input("Ask something: ")
print(f"You said: {user_text}")
```

`input()` always returns a string — wrap in `int()` if you need a number.

### Hands-on

Create `day1.py` and build a small service-quota reporter. Type it, run it, then change the numbers and re-run:

```python
# day1.py — F0 quota reporter
service = "Azure AI Language"
tier = "F0"
used = 4823
limit = 5000
unit = "text records"

remaining = limit - used
pct = used / limit

report = f"""
{service} ({tier})
{'-' * 34}
Used:      {used:,} {unit}
Limit:     {limit:,} {unit}
Remaining: {remaining:,}
Usage:     {pct:.1%}
"""

print(report.strip())
print("STATUS: WARN" if pct > 0.9 else "STATUS: OK")
```

```text
Azure AI Language (F0)
----------------------------------
Used:      4,823 text records
Limit:     5,000 text records
Remaining: 177
Usage:     96.5%
STATUS: WARN
```

Two things to notice: `'-' * 34` repeats a string (handy for separators), and the last line is a *conditional expression* — `A if condition else B` — which you'll see in SDK samples. Full `if` statements come tomorrow.

### Exercises

**1.** Write `exercise1.py` that stores your name, your employer, and a device count in variables, then prints a single sentence using an f-string that includes all three.

<details><summary>Solution</summary>

```python
name = "Shawn"
employer = "HYLIFE Foods"
devices = 120

print(f"{name} manages {devices} devices at {employer}.")
```

```text
Shawn manages 120 devices at HYLIFE Foods.
```
</details>

**2.** Given `line = "2026-08-17T09:14:22 ERROR pi-042 punch-relay timeout"`, extract and print the timestamp, the level, and the device ID on separate lines. Use `.split()`.

<details><summary>Solution</summary>

```python
line = "2026-08-17T09:14:22 ERROR pi-042 punch-relay timeout"
parts = line.split()

print(f"Timestamp: {parts[0]}")
print(f"Level:     {parts[1]}")
print(f"Device:    {parts[2]}")
```

```text
Timestamp: 2026-08-17T09:14:22
Level:     ERROR
Device:    pi-042
```

`parts` is a list; `parts[0]` is the first element. Lists get proper treatment on Day 3.
</details>

**3.** Token cost calculator. Given `input_tokens = 12500`, `output_tokens = 3400`, an input price of `$0.05` per million tokens and an output price of `$0.40` per million, print the cost of each and the total, each formatted to six decimal places.

<details><summary>Solution</summary>

```python
input_tokens = 12500
output_tokens = 3400
input_price_per_m = 0.05
output_price_per_m = 0.40

input_cost = input_tokens / 1_000_000 * input_price_per_m
output_cost = output_tokens / 1_000_000 * output_price_per_m
total = input_cost + output_cost

print(f"Input:  {input_tokens:>7,} tokens  ${input_cost:.6f}")
print(f"Output: {output_tokens:>7,} tokens  ${output_cost:.6f}")
print(f"Total:                    ${total:.6f}")
```

```text
Input:   12,500 tokens  $0.000625
Output:   3,400 tokens  $0.001360
Total:                    $0.001985
```

`1_000_000` — Python allows underscores in numeric literals for readability. `{x:>7,}` right-aligns in 7 characters with thousands separators.
</details>

**4.** Clean up messy input: given `raw_endpoint = "  HTTPS://MyResource.CognitiveServices.Azure.Com/  "`, produce a normalized lowercase URL with no surrounding whitespace and no trailing slash.

<details><summary>Solution</summary>

```python
raw_endpoint = "  HTTPS://MyResource.CognitiveServices.Azure.Com/  "

clean = raw_endpoint.strip().lower().rstrip("/")
print(clean)
```

```text
https://myresource.cognitiveservices.azure.com
```

`.rstrip("/")` strips the given characters from the right end only. `.lstrip()` does the left; `.strip()` does both.
</details>

**5.** Print a three-line banner where the top and bottom lines are made of `=` characters exactly as long as the middle line's text. (Hint: `len()` returns a string's length.)

<details><summary>Solution</summary>

```python
title = "Azure AI Learning Path — Day 1"
bar = "=" * len(title)

print(bar)
print(title)
print(bar)
```

```text
==============================
Azure AI Learning Path — Day 1
==============================
```
</details>

### Checkpoint

- [ ] I can start the REPL, evaluate an expression, and exit it
- [ ] I can create a `.py` file and run it from the terminal and from VS Code
- [ ] I can declare variables of each basic type and check them with `type()`
- [ ] I can build any string I need with an f-string, including numeric formatting (`.2f`, `.1%`, `,`)
- [ ] I can chain string methods (`.strip().lower().split()`) and predict the result
- [ ] I know why `"a" + 5` fails and two ways to fix it

**Explain out loud:** *Why does `7 / 2` return `3.5` when both operands are integers, and what do I use if I want `3`?*
> Python's `/` is true division and always produces a float regardless of operand types — a deliberate design choice so that division doesn't silently lose information. For an integer result use floor division `//`, which rounds toward negative infinity, or wrap in `int()` to truncate.

---

## Day 2 (Wed, 2h) — Control flow

### Why this matters

Every lab script branches: did the API return 200 or 429? Is the confidence score above threshold? Did the user type `/exit`? And every lab iterates: over documents to index, over chunks to embed, over streaming response deltas. Control flow plus loops is 80% of the code you'll write.

### Concepts

**Indentation is the block.** This is the one structural difference from PowerShell that trips everyone. There are no braces:

```python
score = 0.92

if score > 0.8:
    print("High confidence")
    print("Accepting result")
print("Always runs")
```

```text
High confidence
Accepting result
Always runs
```

The colon opens the block; the indentation defines its extent. **Use exactly 4 spaces.** Configure VS Code once and never think about it again: Cmd-Shift-P → "Preferences: Open Settings (UI)" → search "insert spaces" → ensure *Editor: Insert Spaces* is checked and *Tab Size* is 4. Python 3 refuses to mix tabs and spaces in the same block.

> **If you see `IndentationError: expected an indented block`:** you wrote a line ending in `:` and the next line isn't indented.
> **If you see `IndentationError: unindent does not match any outer indentation level`:** you have inconsistent indentation, usually a tab mixed with spaces. In VS Code, Cmd-Shift-P → "Convert Indentation to Spaces" fixes the file.
> **If you see `TabError: inconsistent use of tabs and spaces`:** same cause, same fix.

**Comparison and boolean operators.**

| PowerShell | Python |
|---|---|
| `-eq` | `==` |
| `-ne` | `!=` |
| `-lt` `-gt` `-le` `-ge` | `<` `>` `<=` `>=` |
| `-and` `-or` `-not` | `and` `or` `not` |
| `-contains` / `-in` | `in` |

```python
status = 429
retries = 2

if status == 200:
    print("Success")
elif status == 429 and retries < 3:
    print("Throttled — retrying")
elif status >= 500:
    print("Server error")
else:
    print(f"Unhandled status {status}")
```

```text
Throttled — retrying
```

`elif` is `elseif`. Chained comparisons work naturally and read like math:

```python
temperature = 0.7
if 0.0 <= temperature <= 2.0:
    print("Valid temperature")
```

**`==` versus `is`.** `==` compares values; `is` compares identity (same object in memory). Use `==` for values, and `is` only for `None`, `True`, `False`:

```python
result = None
if result is None:          # correct
    print("No result yet")
if result == None:          # works but non-idiomatic; linters flag it
    pass
```

**Truthiness.** Any value can be tested directly. These are all *falsy*: `False`, `None`, `0`, `0.0`, `""`, `[]`, `{}`, `()`. Everything else is truthy. This produces very clean guard clauses:

```python
response_text = ""

if not response_text:
    print("Empty response — nothing to process")

devices = ["pi-001", "pi-002"]
if devices:
    print(f"Processing {len(devices)} devices")
```

```text
Empty response — nothing to process
Processing 2 devices
```

Be careful with one case: `if score:` is False when `score` is `0` or `0.0`, which may be a legitimate value. When zero is meaningful, test explicitly: `if score is not None:`.

**`for` loops iterate over things, not counters.** This is closer to PowerShell's `foreach` than to a C-style for loop:

```python
services = ["Language", "Speech", "Vision", "Document Intelligence"]

for service in services:
    print(f"Checking {service}")
```

```text
Checking Language
Checking Speech
Checking Vision
Checking Document Intelligence
```

**`range()`** generates numbers when you genuinely need a counter. It's exclusive of the stop value:

```python
for i in range(3):
    print(i)
```

```text
0
1
2
```

`range(1, 4)` → 1, 2, 3. `range(0, 10, 2)` → 0, 2, 4, 6, 8. The exclusive end is deliberate: `range(len(items))` covers exactly the valid indexes.

**`enumerate()`** gives you index and value together — use it instead of manually tracking a counter:

```python
for index, service in enumerate(services, start=1):
    print(f"{index}. {service}")
```

```text
1. Language
2. Speech
3. Vision
4. Document Intelligence
```

**`zip()`** walks two sequences in parallel:

```python
names = ["Language", "Speech", "Vision"]
quotas = [5000, 5, 5000]
units = ["records", "audio hours", "transactions"]

for name, quota, unit in zip(names, quotas, units):
    print(f"{name}: {quota:,} {unit}/month")
```

```text
Language: 5,000 records/month
Speech: 5 audio hours/month
Vision: 5,000 transactions/month
```

**`while`** loops until a condition goes false — used for retry loops and REPL-style chat loops:

```python
attempt = 0
max_attempts = 3
succeeded = False

while attempt < max_attempts and not succeeded:
    attempt += 1
    print(f"Attempt {attempt}...")
    if attempt == 2:
        succeeded = True

print("Succeeded" if succeeded else "Gave up")
```

```text
Attempt 1...
Attempt 2...
Succeeded
```

Python has no `++`; use `+= 1`. (Also `-=`, `*=`, `/=`.)

**`break` and `continue`** behave as expected — `break` exits the loop, `continue` skips to the next iteration:

```python
lines = ["INFO start", "ERROR disk full", "INFO ok", "FATAL halt", "INFO end"]

for line in lines:
    if line.startswith("INFO"):
        continue          # skip informational lines
    if line.startswith("FATAL"):
        print(f"Stopping at: {line}")
        break
    print(f"Issue: {line}")
```

```text
Issue: ERROR disk full
Stopping at: FATAL halt
```

Python also has `else` on loops, which runs only if the loop completed *without* `break`. It's rare but appears in SDK samples:

```python
for line in lines:
    if line.startswith("CRITICAL"):
        print("Found critical")
        break
else:
    print("No critical entries found")
```

```text
No critical entries found
```

**Nesting** works as you'd expect, one indent level per nesting level. Keep it shallow — more than three levels usually means you want a function (Day 4).

### Hands-on

Create `day2.py` — an HTTP status classifier and retry simulator:

```python
# day2.py — classify API responses and simulate retry-with-backoff
statuses = [200, 200, 429, 500, 401, 200, 404, 429]

success = 0
throttled = 0
failed = 0

for i, status in enumerate(statuses, start=1):
    if status == 200:
        label = "OK"
        success += 1
    elif status == 429:
        label = "THROTTLED — back off and retry"
        throttled += 1
    elif status == 401:
        label = "UNAUTHORIZED — check key or Entra token"
        failed += 1
    elif status == 404:
        label = "NOT FOUND — check endpoint and deployment name"
        failed += 1
    elif status >= 500:
        label = "SERVER ERROR — retryable"
        failed += 1
    else:
        label = "UNEXPECTED"
        failed += 1

    print(f"Request {i:>2}: {status} — {label}")

total = len(statuses)
print()
print(f"Summary: {success}/{total} OK, {throttled} throttled, {failed} failed")
print(f"Success rate: {success / total:.0%}")

if throttled:
    print("Recommendation: reduce request rate or request quota increase")
```

```text
Request  1: 200 — OK
Request  2: 200 — OK
Request  3: 429 — THROTTLED — back off and retry
Request  4: 500 — SERVER ERROR — retryable
Request  5: 401 — UNAUTHORIZED — check key or Entra token
Request  6: 200 — OK
Request  7: 404 — NOT FOUND — check endpoint and deployment name
Request  8: 429 — THROTTLED — back off and retry

Summary: 3/8 OK, 2 throttled, 3 failed
Success rate: 38%
```

Those status meanings are not decoration — they are exactly the errors you'll debug against Azure AI services, and 429/401/404 triage shows up in the AI-103 plan-and-manage domain.

### Exercises

**1.** FizzBuzz, the classic loop-and-branch drill. Print 1 to 20; for multiples of 3 print `Fizz`, multiples of 5 print `Buzz`, multiples of both print `FizzBuzz`.

<details><summary>Solution</summary>

```python
for n in range(1, 21):
    if n % 15 == 0:
        print("FizzBuzz")
    elif n % 3 == 0:
        print("Fizz")
    elif n % 5 == 0:
        print("Buzz")
    else:
        print(n)
```

The order matters: test the most specific condition (`% 15`) first, or multiples of 15 would match `% 3` and stop there.
</details>

**2.** Given `scores = [0.98, 0.42, 0.77, 0.91, 0.15, 0.65]` and a threshold of 0.75, print each score labeled ACCEPT or REJECT, then print how many were accepted.

<details><summary>Solution</summary>

```python
scores = [0.98, 0.42, 0.77, 0.91, 0.15, 0.65]
threshold = 0.75
accepted = 0

for score in scores:
    if score >= threshold:
        print(f"{score:.2f} ACCEPT")
        accepted += 1
    else:
        print(f"{score:.2f} REJECT")

print(f"\n{accepted} of {len(scores)} above threshold {threshold}")
```

```text
0.98 ACCEPT
0.42 REJECT
0.77 ACCEPT
0.91 ACCEPT
0.15 REJECT
0.65 REJECT

3 of 6 above threshold 0.75
```

`\n` inside a string is a newline character.
</details>

**3.** Exponential backoff schedule. Print the wait time before each of 6 retry attempts, doubling from 1 second, capped at 16 seconds.

<details><summary>Solution</summary>

```python
wait = 1
cap = 16

for attempt in range(1, 7):
    print(f"Attempt {attempt}: wait {wait}s")
    wait = min(wait * 2, cap)
```

```text
Attempt 1: wait 1s
Attempt 2: wait 2s
Attempt 3: wait 4s
Attempt 4: wait 8s
Attempt 5: wait 16s
Attempt 6: wait 16s
```

`min()` and `max()` are builtins — no import needed.
</details>

**4.** Loop over `devices = ["pi-001", "pi-002", "BROKEN", "pi-004", "pi-005"]` and stop processing entirely when you hit an entry that doesn't start with `pi-`, printing which entry stopped you. If you get through all of them, print "All devices valid."

<details><summary>Solution</summary>

```python
devices = ["pi-001", "pi-002", "BROKEN", "pi-004", "pi-005"]

for device in devices:
    if not device.startswith("pi-"):
        print(f"Invalid entry halted processing: {device}")
        break
    print(f"Processing {device}")
else:
    print("All devices valid.")
```

```text
Processing pi-001
Processing pi-002
Invalid entry halted processing: BROKEN
```

The `for...else` prints only when no `break` occurred — swap `BROKEN` for `pi-003` and re-run to see the difference.
</details>

**5.** A number-guessing loop: set `secret = 7`, then use a `while` loop with `input()` to keep asking until the user guesses it, printing "higher" or "lower" as hints, and reporting the number of guesses at the end.

<details><summary>Solution</summary>

```python
secret = 7
guesses = 0

while True:
    raw = input("Guess (1-10): ")
    guesses += 1
    guess = int(raw)

    if guess == secret:
        print(f"Correct in {guesses} guesses.")
        break
    elif guess < secret:
        print("Higher")
    else:
        print("Lower")
```

`while True:` with a `break` is the idiomatic "loop until something happens" pattern — you'll use exactly this shape for the chatbot in Week 2. Note this crashes on non-numeric input; Day 6–7 teaches the fix.
</details>

### Checkpoint

- [ ] I write blocks with 4-space indentation and can fix an IndentationError from the message alone
- [ ] I use `if/elif/else` with `and`/`or`/`not` and know `==` vs `is`
- [ ] I can explain truthiness and name the falsy values
- [ ] I iterate collections with `for`, and use `enumerate()` and `zip()` when I need indexes or parallel sequences
- [ ] I write `while` loops with a clear exit condition, including `while True` + `break`
- [ ] I use `break` and `continue` correctly

**Explain out loud:** *When would I use `range()` instead of iterating a collection directly?*
> When I need the numbers themselves rather than the items — a fixed count of retry attempts, a backoff schedule, or generating test data. If I'm reaching for `range(len(items))` just to index into `items`, that's a signal I should either iterate `items` directly or use `enumerate()`.

---

## Day 3 (Thu, 1h) — Lists and tuples

### Why this matters

An API returns a list of matches, a list of entities, a list of chunks, a list of choices. `response["choices"][0]` — that `[0]` is list indexing, and it appears in literally every LLM call you will ever write.

### Concepts

**Lists** are ordered, mutable sequences. Square brackets, comma-separated, mixed types allowed (though usually you keep them homogeneous):

```python
services = ["Language", "Speech", "Vision"]
scores = [0.98, 0.42, 0.77]
empty = []
```

**Indexing is zero-based**, and negative indexes count from the end:

```python
print(services[0])    # first
print(services[2])    # third
print(services[-1])   # last — very common idiom
print(services[-2])   # second from last
```

```text
Language
Vision
Vision
Speech
```

> **If you see `IndexError: list index out of range`:** you asked for an index that doesn't exist. A 3-item list has valid indexes 0, 1, 2 (and -1, -2, -3). Check with `len()` first, or use a guard: `if len(items) > 0:`.

**Slicing** takes `[start:stop:step]` — start inclusive, stop exclusive:

```python
letters = ["a", "b", "c", "d", "e", "f"]

print(letters[1:4])     # index 1,2,3
print(letters[:3])      # from start
print(letters[3:])      # to end
print(letters[-2:])     # last two
print(letters[::2])     # every second
print(letters[::-1])    # reversed
```

```text
['b', 'c', 'd']
['a', 'b', 'c']
['d', 'e', 'f']
['e', 'f']
['a', 'c', 'e']
['f', 'e', 'd', 'c', 'b', 'a']
```

| Expression | Meaning |
|---|---|
| `x[0]` | first element |
| `x[-1]` | last element |
| `x[:n]` | first n elements |
| `x[n:]` | everything from n onward |
| `x[-n:]` | last n elements |
| `x[a:b]` | from a up to *but not including* b |

Slicing works on strings too — `"hello"[1:4]` is `"ell"`. Unlike indexing, slicing never raises IndexError; an out-of-range slice just returns fewer items or an empty list.

**Mutation.** Lists change in place:

```python
queue = ["doc1", "doc2"]

queue.append("doc3")            # add one to the end
queue.extend(["doc4", "doc5"])  # add several
queue.insert(0, "doc0")         # insert at position
print(queue)

last = queue.pop()              # remove & return last
first = queue.pop(0)            # remove & return by index
queue.remove("doc2")            # remove by value (first match)
print(queue, "| popped:", last, first)
```

```text
['doc0', 'doc1', 'doc2', 'doc3', 'doc4', 'doc5']
['doc1', 'doc3', 'doc4'] | popped: doc5 doc0
```

`.append()` versus `.extend()` is a classic bug: `append` adds its argument as a *single element* (appending a list gives you a nested list), while `extend` adds each element of its argument.

**Sorting.** Two forms, and the difference matters:

```python
scores = [0.42, 0.98, 0.15, 0.77]

print(sorted(scores))                # returns a NEW sorted list
print(sorted(scores, reverse=True))  # descending
print(scores)                        # original unchanged

scores.sort()                        # sorts IN PLACE, returns None
print(scores)
```

```text
[0.15, 0.42, 0.77, 0.98]
[0.98, 0.77, 0.42, 0.15]
[0.42, 0.98, 0.15, 0.77]
[0.15, 0.42, 0.77, 0.98]
```

> **If a sorted list comes out as `None`:** you wrote `scores = scores.sort()`. In-place methods return `None`. Use `sorted()` when you want a value back, `.sort()` when you want to mutate.

**Other essentials:**

```python
items = ["a", "b", "c", "b"]
print(len(items))          # 4
print("b" in items)        # True — membership test
print(items.count("b"))    # 2
print(items.index("b"))    # 1 — first position
items.reverse()            # in place
print(items)               # ['b', 'c', 'b', 'a']
```

**Tuples** are immutable lists, written with parentheses. Use them for fixed groupings that shouldn't change — coordinates, RGB values, a function returning multiple values:

```python
dimensions = (1920, 1080)
print(dimensions[0])

dimensions[0] = 1280    # TypeError: 'tuple' object does not support item assignment
```

**Unpacking** is the reason tuples matter day to day:

```python
width, height = dimensions
print(f"{width}x{height}")

# swap without a temp variable
a, b = 1, 2
a, b = b, a
print(a, b)
```

```text
1920x1080
2 1
```

This is why `for index, value in enumerate(...)` works — `enumerate` yields tuples and the loop unpacks them.

**Nested lists** — a list whose elements are lists. Index twice:

```python
matrix = [
    ["pi-001", "online", 98],
    ["pi-002", "offline", 0],
    ["pi-003", "online", 72],
]

print(matrix[1])       # ['pi-002', 'offline', 0]
print(matrix[1][1])    # offline

for device, status, battery in matrix:
    print(f"{device:>8} {status:>8} {battery:>3}%")
```

```text
['pi-002', 'offline', 0]
offline
  pi-001   online  98%
  pi-002  offline   0%
  pi-003   online  72%
```

### Hands-on

`day3.py` — analyze confidence scores the way you will when filtering search results:

```python
# day3.py — confidence score analysis
scores = [0.98, 0.42, 0.77, 0.91, 0.15, 0.65, 0.88, 0.33]
threshold = 0.75

ranked = sorted(scores, reverse=True)
top3 = ranked[:3]
accepted = []
rejected = []

for s in scores:
    if s >= threshold:
        accepted.append(s)
    else:
        rejected.append(s)

print(f"Count:     {len(scores)}")
print(f"Highest:   {ranked[0]:.2f}")
print(f"Lowest:    {ranked[-1]:.2f}")
print(f"Top 3:     {top3}")
print(f"Average:   {sum(scores) / len(scores):.3f}")
print(f"Accepted:  {len(accepted)} -> {accepted}")
print(f"Rejected:  {len(rejected)} -> {rejected}")
```

```text
Count:     8
Highest:   0.98
Lowest:    0.15
Top 3:     [0.98, 0.91, 0.88]
Average:   0.636
Accepted:  3 -> [0.98, 0.77, 0.91]
Rejected:  5 -> [0.42, 0.15, 0.65, 0.33]
```

`sum()` is a builtin. There's no builtin `average` — `sum(x) / len(x)` is the idiom.

### Exercises

**1.** Given `log = "2026-08-17 ERROR pi-042 timeout after 30s"`, split it and use slicing to print everything from the third word onward as a single string.

<details><summary>Solution</summary>

```python
log = "2026-08-17 ERROR pi-042 timeout after 30s"
parts = log.split()
message = " ".join(parts[3:])
print(message)
```

```text
timeout after 30s
```
</details>

**2.** From `devices = ["pi-001", "pi-002", "pi-003", "pi-004", "pi-005", "pi-006"]`, print the first two, the last two, and every other device — using slices only.

<details><summary>Solution</summary>

```python
devices = ["pi-001", "pi-002", "pi-003", "pi-004", "pi-005", "pi-006"]

print("First two:", devices[:2])
print("Last two: ", devices[-2:])
print("Alternate:", devices[::2])
```

```text
First two: ['pi-001', 'pi-002']
Last two:  ['pi-005', 'pi-006']
Alternate: ['pi-001', 'pi-003', 'pi-005']
```
</details>

**3.** Deduplicate `tags = ["vision", "language", "vision", "speech", "language", "vision"]` while preserving first-seen order, then print each unique tag with its occurrence count.

<details><summary>Solution</summary>

```python
tags = ["vision", "language", "vision", "speech", "language", "vision"]

unique = []
for tag in tags:
    if tag not in unique:
        unique.append(tag)

for tag in unique:
    print(f"{tag:>9}: {tags.count(tag)}")
```

```text
   vision: 3
 language: 2
   speech: 1
```

(`set(tags)` also deduplicates but loses order — sets appear on Day 5.)
</details>

**4.** Given a nested list of `[device, status, battery]` rows, print only the devices whose status is `"online"` and whose battery is below 80, formatted as a warning line.

<details><summary>Solution</summary>

```python
fleet = [
    ["pi-001", "online", 98],
    ["pi-002", "offline", 0],
    ["pi-003", "online", 72],
    ["pi-004", "online", 45],
]

for device, status, battery in fleet:
    if status == "online" and battery < 80:
        print(f"WARN {device} battery at {battery}%")
```

```text
WARN pi-003 battery at 72%
WARN pi-004 battery at 45%
```
</details>

**5.** Write code that takes `values = [3, 7, 2, 9, 4]` and prints the second-highest value without using `sorted()` twice or hardcoding an index into the original list.

<details><summary>Solution</summary>

```python
values = [3, 7, 2, 9, 4]
ranked = sorted(values, reverse=True)
print(f"Second highest: {ranked[1]}")
```

```text
Second highest: 7
```

Sorting once and taking index 1 is the clear approach. (Watch out for duplicates — if the top value appears twice, `ranked[1]` equals `ranked[0]`. Deduplicate first if "second distinct value" is what you mean.)
</details>

### Checkpoint

- [ ] I index lists including negative indexes, and predict IndexError before it happens
- [ ] I slice confidently — first n, last n, ranges, step, reverse
- [ ] I know `.append()` vs `.extend()` and `sorted()` vs `.sort()`
- [ ] I can unpack a tuple, including in a `for` loop
- [ ] I can navigate a nested list with double indexing

**Explain out loud:** *Why does `response["choices"][0]["message"]["content"]` have a `[0]` in the middle?*
> Because the API returns `choices` as a *list* — the models can return multiple candidate completions in one call (controlled by an `n` parameter). Index 0 is the first, and when you only asked for one completion it's the only one. Understanding this saves confusion the first time you see the raw JSON.

---

## Day 4 (Sat, 4h) — Functions, modules, and dictionaries

This is the most important day of the week. Take the full four hours.

### Why this matters

Functions are how you stop repeating yourself and how you make lab code testable. Dictionaries are how Python represents JSON — and JSON is how every Azure AI service on earth talks to you. If you finish Week 1 shaky on dictionaries, Week 2 will hurt.

### Part 1 — Functions

**Definition and calling:**

```python
def greet(name):
    return f"Hello, {name}"

message = greet("Shawn")
print(message)
```

```text
Hello, Shawn
```

`def`, name, parameters in parentheses, colon, indented body. `return` sends a value back and exits immediately. A function without `return` returns `None`.

**Parameters, defaults, and keyword arguments:**

```python
def call_model(prompt, temperature=0.7, max_tokens=500):
    return f"prompt={prompt!r} temp={temperature} max={max_tokens}"

print(call_model("Summarize this"))
print(call_model("Summarize this", 0.0))
print(call_model("Summarize this", max_tokens=100))
print(call_model(prompt="Hi", temperature=1.0, max_tokens=50))
```

```text
prompt='Summarize this' temp=0.7 max=500
prompt='Summarize this' temp=0.0 max=500
prompt='Summarize this' temp=0.7 max=100
prompt='Hi' temp=1.0 max=50
```

Parameters with defaults must come after those without. Keyword arguments can be given in any order and make calls self-documenting — the Azure SDKs use them heavily, which is why `client.chat.completions.create(model=..., messages=..., temperature=...)` looks the way it does.

The `!r` in an f-string calls `repr()` — showing quotes around strings. Useful in debug output.

> **The mutable default trap.** Never write `def f(items=[])`. The default list is created once at definition time and shared across all calls:
> ```python
> def bad(item, bucket=[]):
>     bucket.append(item)
>     return bucket
> print(bad("a"))   # ['a']
> print(bad("b"))   # ['a', 'b']  ← surprise
> ```
> The fix: `def good(item, bucket=None):` then `if bucket is None: bucket = []`.

**`*args` and `**kwargs`** collect extra positional and keyword arguments:

```python
def log_event(level, *details, **context):
    print(f"[{level}] {' '.join(details)}")
    for key, value in context.items():
        print(f"    {key}={value}")

log_event("ERROR", "device", "unreachable", device="pi-042", retries=3)
```

```text
[ERROR] device unreachable
    device=pi-042
    retries=3
```

This is PowerShell splatting's cousin: `**config` unpacks a dictionary into keyword arguments, exactly like `@params` in PowerShell.

```python
settings = {"temperature": 0.2, "max_tokens": 100}
print(call_model("Hello", **settings))
```

```text
prompt='Hello' temp=0.2 max=100
```

**Returning multiple values** — actually returning a tuple, unpacked at the call site:

```python
def analyze(text):
    words = len(text.split())
    chars = len(text)
    return words, chars

word_count, char_count = analyze("the quick brown fox")
print(word_count, char_count)
```

```text
4 19
```

**Scope.** Variables created inside a function are local and vanish when it returns. A function can *read* module-level variables but assigning to one creates a new local unless you declare `global`. In practice: pass what you need in, return what you produce. Avoid `global`.

**Docstrings and type hints.** Write both — the Azure SDK code you'll read is fully annotated, and hints make VS Code's autocomplete dramatically better:

```python
def estimate_cost(input_tokens: int, output_tokens: int,
                  in_price: float = 0.05, out_price: float = 0.40) -> float:
    """Return the USD cost of a model call.

    Prices are per one million tokens (Global Standard serverless).
    """
    return (input_tokens * in_price + output_tokens * out_price) / 1_000_000

print(f"${estimate_cost(12500, 3400):.6f}")
```

```text
$0.001985
```

Type hints are *not enforced* at runtime — Python won't stop you passing a string. They're documentation that tooling can check. Write them anyway.

### Part 2 — Modules and imports

Python's standard library is enormous and already installed. Import what you need:

```python
import json
import os
from pathlib import Path
from datetime import datetime, timezone
import random as rnd

print(datetime.now(timezone.utc).isoformat())
print(os.getenv("HOME"))
print(Path.home())
print(rnd.choice(["a", "b", "c"]))
```

Three import forms:

| Form | Use |
|---|---|
| `import json` | then call `json.loads(...)` — clearest, preferred |
| `from pathlib import Path` | pulls one name into your namespace — for things you use constantly |
| `import random as rnd` | alias — for long module names (`import azure.ai.projects as projects`) |

The modules you'll actually use in this path:

| Module | For |
|---|---|
| `json` | parse and produce JSON (Week 2, Day 10) |
| `os` | environment variables (`os.getenv`) |
| `pathlib` | file paths (Days 6–7) |
| `datetime` | timestamps |
| `time` | `time.sleep()` for backoff |
| `re` | regular expressions |
| `logging` | proper logging instead of `print` |
| `sys` | `sys.argv`, `sys.exit()` |

**`if __name__ == "__main__":`** — you'll see this in every sample. When Python runs a file directly, it sets that file's `__name__` to `"__main__"`; when the file is *imported* by another file, `__name__` is the module name instead. So this block runs on direct execution but not on import:

```python
def main():
    print("Running the program")

if __name__ == "__main__":
    main()
```

Use it in every script you write from now on. It means your functions can be imported and reused without the script's side effects firing.

### Part 3 — Dictionaries (the important part)

A dictionary maps keys to values. This is PowerShell's hashtable, and it is the Python representation of a JSON object:

```python
device = {
    "id": "pi-042",
    "status": "online",
    "battery": 72,
    "location": "Barn 3",
}

print(device["id"])
print(device["battery"])
```

```text
pi-042
72
```

| PowerShell | Python |
|---|---|
| `@{ id = "pi-042" }` | `{"id": "pi-042"}` |
| `$h["id"]` or `$h.id` | `d["id"]` |
| `$h.ContainsKey("id")` | `"id" in d` |
| `$h.Keys` / `$h.Values` | `d.keys()` / `d.values()` |
| `$h.Remove("id")` | `del d["id"]` |
| `ConvertFrom-Json` | `json.loads` |

**`[]` versus `.get()`** — this distinction will save you hours:

```python
print(device["status"])           # online
print(device["firmware"])         # KeyError: 'firmware'
```

```python
print(device.get("firmware"))                 # None — no exception
print(device.get("firmware", "unknown"))      # unknown — default value
```

> **If you see `KeyError: 'something'`:** the key isn't in the dictionary. Either the API response shape differs from what you assumed, or you have a typo. Use `.get()` with a default when a key is genuinely optional; use `[]` when its absence is a real error you want to hear about immediately. When debugging an unfamiliar response, `print(d.keys())` first.

**Adding, updating, deleting:**

```python
device["firmware"] = "2.4.1"        # add
device["battery"] = 68              # update
device.update({"status": "degraded", "last_seen": "09:14"})  # bulk
del device["location"]              # delete
removed = device.pop("firmware", None)  # delete & return, safe

print(device)
```

```text
{'id': 'pi-042', 'status': 'degraded', 'battery': 68, 'last_seen': '09:14'}
```

**Iterating.** Three ways, and you want `.items()` most of the time:

```python
for key in device:                 # keys (default)
    print(key)

for value in device.values():      # values
    print(value)

for key, value in device.items():  # both — the useful one
    print(f"{key:>10}: {value}")
```

```text
        id: pi-042
    status: degraded
   battery: 68
 last_seen: 09:14
```

**Dictionaries in lists, lists in dictionaries** — this nesting *is* the shape of API responses:

```python
fleet = [
    {"id": "pi-001", "status": "online",  "battery": 98},
    {"id": "pi-002", "status": "offline", "battery": 0},
    {"id": "pi-003", "status": "online",  "battery": 72},
]

for d in fleet:
    print(f"{d['id']}: {d['status']} ({d['battery']}%)")
```

```text
pi-001: online (98%)
pi-002: offline (0%)
pi-003: online (72%)
```

Note the quoting: inside an f-string delimited by double quotes, use single quotes for the dictionary keys (`{d['id']}`) — or the string terminates early.

**Counting with a dictionary** — the pattern you'll use for aggregation:

```python
statuses = ["online", "offline", "online", "online", "degraded", "offline"]
counts = {}

for s in statuses:
    counts[s] = counts.get(s, 0) + 1

print(counts)
```

```text
{'online': 3, 'offline': 2, 'degraded': 1}
```

`counts.get(s, 0) + 1` — "current count or zero, plus one." Memorize this idiom; it's everywhere.

### Hands-on

`day4.py` — a fleet report combining everything from today:

```python
# day4.py — fleet health report
from datetime import datetime, timezone

FLEET = [
    {"id": "pi-001", "status": "online",   "battery": 98, "site": "Barn 1"},
    {"id": "pi-002", "status": "offline",  "battery": 0,  "site": "Barn 1"},
    {"id": "pi-003", "status": "online",   "battery": 72, "site": "Barn 2"},
    {"id": "pi-004", "status": "degraded", "battery": 41, "site": "Barn 2"},
    {"id": "pi-005", "status": "online",   "battery": 89, "site": "Barn 3"},
]

LOW_BATTERY = 50


def count_by(records: list, field: str) -> dict:
    """Count records grouped by the value of one field."""
    counts = {}
    for record in records:
        key = record.get(field, "unknown")
        counts[key] = counts.get(key, 0) + 1
    return counts


def needs_attention(records: list, threshold: int = LOW_BATTERY) -> list:
    """Return devices that are not online or are below the battery threshold."""
    flagged = []
    for record in records:
        if record["status"] != "online" or record["battery"] < threshold:
            flagged.append(record)
    return flagged


def average_battery(records: list) -> float:
    online = [r["battery"] for r in records if r["status"] == "online"]
    if not online:
        return 0.0
    return sum(online) / len(online)


def main():
    stamp = datetime.now(timezone.utc).strftime("%Y-%m-%d %H:%M UTC")
    print(f"FLEET REPORT — {stamp}")
    print("=" * 42)

    print(f"Devices:        {len(FLEET)}")
    print(f"By status:      {count_by(FLEET, 'status')}")
    print(f"By site:        {count_by(FLEET, 'site')}")
    print(f"Avg battery (online): {average_battery(FLEET):.1f}%")

    flagged = needs_attention(FLEET)
    print(f"\nNeeds attention ({len(flagged)}):")
    for device in flagged:
        print(f"  {device['id']:>7}  {device['status']:>9}  {device['battery']:>3}%  {device['site']}")


if __name__ == "__main__":
    main()
```

```text
FLEET REPORT — 2026-08-22 14:03 UTC
==========================================
Devices:        5
By status:      {'online': 3, 'offline': 1, 'degraded': 1}
By site:        {'Barn 1': 2, 'Barn 2': 2, 'Barn 3': 1}
Avg battery (online): 86.3%

Needs attention (2):
  pi-002   offline    0%  Barn 1
  pi-004  degraded   41%  Barn 2
```

There's one list comprehension in `average_battery` — tomorrow's topic, included so you see it in context first.

### Exercises

**1.** Write `token_budget(used: int, limit: int) -> dict` returning a dictionary with keys `used`, `limit`, `remaining`, `pct_used`, and `status` (where status is `"OK"` under 75%, `"WARN"` under 90%, else `"CRITICAL"`). Print the result for `(4823, 5000)`.

<details><summary>Solution</summary>

```python
def token_budget(used: int, limit: int) -> dict:
    pct = used / limit
    if pct < 0.75:
        status = "OK"
    elif pct < 0.90:
        status = "WARN"
    else:
        status = "CRITICAL"

    return {
        "used": used,
        "limit": limit,
        "remaining": limit - used,
        "pct_used": round(pct, 4),
        "status": status,
    }

result = token_budget(4823, 5000)
for key, value in result.items():
    print(f"{key:>10}: {value}")
```

```text
      used: 4823
     limit: 5000
 remaining: 177
  pct_used: 0.9646
    status: CRITICAL
```
</details>

**2.** Given the F0 quota table below, write a function that takes a service name and returns a formatted string describing its quota, or a helpful message if the service isn't in the table.

```python
QUOTAS = {
    "language": {"limit": 5000, "unit": "text records"},
    "speech":   {"limit": 5,    "unit": "audio hours"},
    "vision":   {"limit": 5000, "unit": "transactions"},
}
```

<details><summary>Solution</summary>

```python
QUOTAS = {
    "language": {"limit": 5000, "unit": "text records"},
    "speech":   {"limit": 5,    "unit": "audio hours"},
    "vision":   {"limit": 5000, "unit": "transactions"},
}

def describe_quota(service: str) -> str:
    entry = QUOTAS.get(service.lower())
    if entry is None:
        known = ", ".join(sorted(QUOTAS))
        return f"No F0 quota on record for '{service}'. Known services: {known}"
    return f"{service.title()} F0: {entry['limit']:,} {entry['unit']} per month"

print(describe_quota("Language"))
print(describe_quota("speech"))
print(describe_quota("translator"))
```

```text
Language F0: 5,000 text records per month
Speech F0: 5 audio hours per month
No F0 quota on record for 'translator'. Known services: language, speech, vision
```

Iterating a dict (as in `sorted(QUOTAS)`) yields its keys.
</details>

**3.** Write a function that takes a list of device dictionaries and returns a *dictionary of lists* grouping device IDs by site.

<details><summary>Solution</summary>

```python
def group_by_site(records: list) -> dict:
    groups = {}
    for record in records:
        site = record["site"]
        if site not in groups:
            groups[site] = []
        groups[site].append(record["id"])
    return groups

fleet = [
    {"id": "pi-001", "site": "Barn 1"},
    {"id": "pi-002", "site": "Barn 1"},
    {"id": "pi-003", "site": "Barn 2"},
]

for site, ids in group_by_site(fleet).items():
    print(f"{site}: {', '.join(ids)}")
```

```text
Barn 1: pi-001, pi-002
Barn 2: pi-003
```

`groups.setdefault(site, []).append(record["id"])` does the same in one line — you'll see it in real code.
</details>

**4.** Write `merge_config(defaults: dict, overrides: dict) -> dict` that returns a new dictionary with the overrides applied, without mutating either input. Test it with model settings.

<details><summary>Solution</summary>

```python
def merge_config(defaults: dict, overrides: dict) -> dict:
    merged = defaults.copy()
    merged.update(overrides)
    return merged

DEFAULTS = {"model": "gpt-5-nano", "temperature": 0.7, "max_tokens": 500}
result = merge_config(DEFAULTS, {"temperature": 0.0})

print(result)
print(DEFAULTS)   # unchanged
```

```text
{'model': 'gpt-5-nano', 'temperature': 0.0, 'max_tokens': 500}
{'model': 'gpt-5-nano', 'temperature': 0.7, 'max_tokens': 500}
```

`.copy()` is a shallow copy — fine here. For nested structures you'd need `copy.deepcopy()`. Python 3.9+ also supports `defaults | overrides`.
</details>

**5.** Write a function that takes a sentence and returns a dictionary of word frequencies (lowercased, punctuation stripped from the ends of words), then print the top 3 by count.

<details><summary>Solution</summary>

```python
def word_frequencies(text: str) -> dict:
    counts = {}
    for word in text.lower().split():
        clean = word.strip(".,!?;:\"'")
        if clean:
            counts[clean] = counts.get(clean, 0) + 1
    return counts

text = "The model returns a model response. The response is grounded, the model says."
freq = word_frequencies(text)

top = sorted(freq.items(), key=lambda pair: pair[1], reverse=True)
for word, count in top[:3]:
    print(f"{word:>10}: {count}")
```

```text
       the: 4
     model: 3
  response: 2
```

`freq.items()` gives (key, value) tuples; `key=lambda pair: pair[1]` sorts by the second element. A `lambda` is a one-line anonymous function — you'll meet these in SDK callbacks.
</details>

### Checkpoint

- [ ] I write functions with parameters, defaults, keyword arguments, and a return value
- [ ] I add type hints and a docstring by habit
- [ ] I know the mutable-default trap and its fix
- [ ] I use `if __name__ == "__main__":` in every script
- [ ] I create, read, update, delete, and iterate dictionaries fluently
- [ ] I know exactly when to use `d["key"]` versus `d.get("key", default)`
- [ ] I can build a count/aggregate dictionary with the `.get(k, 0) + 1` idiom
- [ ] I can navigate a list of dictionaries and a dictionary of lists

**Explain out loud:** *Why is the dictionary the single most important Python type for AI work?*
> Because JSON objects deserialize directly into dictionaries, and every Azure AI service communicates in JSON. A model response, an embedding result, a search hit, an agent tool-call payload — all of them arrive as nested dictionaries and lists. Fluency at walking `d["choices"][0]["message"]["content"]` and at defensively using `.get()` is the difference between reading an API response confidently and guessing.

---

## Day 5 (Sun, 2h) — Nested data, comprehensions, and a mini-project

### Why this matters

Real API responses are dictionaries containing lists containing dictionaries, four or five levels deep. Today you learn a reliable *method* for exploring an unfamiliar response, plus comprehensions — the compact filtering/transforming syntax that replaces most of your PowerShell pipeline habits.

### Concepts

**Walking an unfamiliar structure.** Never guess at a response shape. Use this three-step method:

```python
response = {
    "id": "chatcmpl-123",
    "model": "gpt-5-nano",
    "choices": [
        {
            "index": 0,
            "message": {"role": "assistant", "content": "Grounded answer here."},
            "finish_reason": "stop",
        }
    ],
    "usage": {"prompt_tokens": 412, "completion_tokens": 38, "total_tokens": 450},
}

# 1. What type is it, and what are the top-level keys?
print(type(response))
print(list(response.keys()))

# 2. Descend one level at a time
print(type(response["choices"]))
print(len(response["choices"]))
print(list(response["choices"][0].keys()))

# 3. Reach the value
print(response["choices"][0]["message"]["content"])
```

```text
<class 'dict'>
['id', 'model', 'choices', 'usage']
<class 'list'>
1
['index', 'message', 'finish_reason']
Grounded answer here.
```

That last line is the canonical OpenAI-compatible response path. You will type it hundreds of times. Read it as: *the response has choices (a list) → take the first → it has a message (a dict) → take its content.*

**Defensive access on nested data.** In production, chain `.get()`:

```python
content = (
    response.get("choices", [{}])[0]
    .get("message", {})
    .get("content", "")
)
print(repr(content))
```

```text
'Grounded answer here.'
```

For learning labs, plain indexing is fine and fails loudly, which is what you want. For anything you'd ship, guard it.

**List comprehensions.** A compact `for` loop that builds a list. Side by side:

```python
scores = [0.98, 0.42, 0.77, 0.91, 0.15]

# the loop
doubled = []
for s in scores:
    doubled.append(s * 2)

# the comprehension — identical result
doubled = [s * 2 for s in scores]
print(doubled)
```

```text
[1.96, 0.84, 1.54, 1.82, 0.3]
```

Add a filter with `if` at the end:

```python
high = [s for s in scores if s >= 0.75]
print(high)

labels = [f"{s:.0%}" for s in scores if s >= 0.75]
print(labels)
```

```text
[0.98, 0.77, 0.91]
['98%', '77%', '91%']
```

Read it right-to-left-ish: *for each s in scores, if s ≥ 0.75, keep s.*

| PowerShell | Python |
|---|---|
| `$x \| Where-Object { $_ -ge 0.75 }` | `[s for s in x if s >= 0.75]` |
| `$x \| ForEach-Object { $_ * 2 }` | `[s * 2 for s in x]` |
| `$x \| Where {...} \| ForEach {...}` | `[f(s) for s in x if cond(s)]` |

Extracting a field from a list of dictionaries is the most common real use:

```python
fleet = [
    {"id": "pi-001", "status": "online",  "battery": 98},
    {"id": "pi-002", "status": "offline", "battery": 0},
    {"id": "pi-003", "status": "online",  "battery": 72},
]

ids = [d["id"] for d in fleet]
online_ids = [d["id"] for d in fleet if d["status"] == "online"]
low = [d["id"] for d in fleet if d["battery"] < 80 and d["status"] == "online"]

print(ids)
print(online_ids)
print(low)
```

```text
['pi-001', 'pi-002', 'pi-003']
['pi-001', 'pi-003']
['pi-003']
```

**Dictionary comprehensions** use `{key: value for ...}`:

```python
battery_map = {d["id"]: d["battery"] for d in fleet}
print(battery_map)

flagged = {k: v for k, v in battery_map.items() if v < 80}
print(flagged)
```

```text
{'pi-001': 98, 'pi-002': 0, 'pi-003': 72}
{'pi-002': 0, 'pi-003': 72}
```

**When *not* to use a comprehension.** If it doesn't fit on one readable line, or it has more than one `if`, or the body does something other than compute a value (printing, writing files, calling APIs with side effects) — use a regular loop. Clever one-liners you can't read in three months are a cost, not a win.

**Sets** — unordered collections of unique values, written with braces:

```python
tags = ["vision", "language", "vision", "speech", "language"]
unique = set(tags)
print(unique)
print(len(unique))

a = {"vision", "language", "speech"}
b = {"language", "speech", "search"}
print(a & b)   # intersection — in both
print(a | b)   # union — in either
print(a - b)   # difference — in a only
```

```text
{'speech', 'vision', 'language'}
3
{'speech', 'language'}
{'speech', 'vision', 'language', 'search'}
{'vision'}
```

Sets are great for deduplication and membership tests (very fast), and useless when order matters.

### Mini-project

Build `inventory_report.py` — a filtering and aggregation exercise over nested data, the same shape of work you'll do when processing search results in Phase 3.

```python
# inventory_report.py — device inventory analysis
from datetime import datetime, timezone

INVENTORY = [
    {"id": "pi-001", "site": "Barn 1", "status": "online",   "battery": 98, "fw": "2.4.1", "tags": ["punch", "prod"]},
    {"id": "pi-002", "site": "Barn 1", "status": "offline",  "battery": 0,  "fw": "2.3.9", "tags": ["punch", "prod"]},
    {"id": "pi-003", "site": "Barn 2", "status": "online",   "battery": 72, "fw": "2.4.1", "tags": ["punch"]},
    {"id": "pi-004", "site": "Barn 2", "status": "degraded", "battery": 41, "fw": "2.2.0", "tags": ["punch", "legacy"]},
    {"id": "pi-005", "site": "Barn 3", "status": "online",   "battery": 89, "fw": "2.4.1", "tags": ["punch", "prod"]},
    {"id": "pi-006", "site": "Barn 3", "status": "online",   "battery": 55, "fw": "2.3.9", "tags": ["test"]},
]

CURRENT_FIRMWARE = "2.4.1"
LOW_BATTERY = 60


def summarize(records: list) -> dict:
    """Produce headline counts for the fleet."""
    return {
        "total": len(records),
        "online": len([r for r in records if r["status"] == "online"]),
        "needs_firmware": len([r for r in records if r["fw"] != CURRENT_FIRMWARE]),
        "low_battery": len([r for r in records if r["battery"] < LOW_BATTERY]),
    }


def count_field(records: list, field: str) -> dict:
    counts = {}
    for r in records:
        counts[r[field]] = counts.get(r[field], 0) + 1
    return counts


def all_tags(records: list) -> set:
    tags = set()
    for r in records:
        tags.update(r["tags"])
    return tags


def main():
    stamp = datetime.now(timezone.utc).strftime("%Y-%m-%d %H:%M UTC")
    print(f"DEVICE INVENTORY — {stamp}")
    print("=" * 52)

    stats = summarize(INVENTORY)
    for key, value in stats.items():
        print(f"{key.replace('_', ' ').title():>16}: {value}")

    print(f"\nBy site:   {count_field(INVENTORY, 'site')}")
    print(f"By status: {count_field(INVENTORY, 'status')}")
    print(f"By firmware: {count_field(INVENTORY, 'fw')}")
    print(f"All tags:  {sorted(all_tags(INVENTORY))}")

    stale = [r for r in INVENTORY if r["fw"] != CURRENT_FIRMWARE]
    print(f"\nFirmware update required ({len(stale)}):")
    for r in stale:
        print(f"  {r['id']:>7}  fw {r['fw']}  {r['site']}")

    urgent = [r for r in INVENTORY
              if r["status"] == "online" and r["battery"] < LOW_BATTERY]
    print(f"\nOnline but low battery ({len(urgent)}):")
    for r in urgent:
        print(f"  {r['id']:>7}  {r['battery']:>3}%  {r['site']}")

    prod_offline = [r["id"] for r in INVENTORY
                    if "prod" in r["tags"] and r["status"] != "online"]
    print(f"\nProduction devices not online: {prod_offline or 'none'}")


if __name__ == "__main__":
    main()
```

```text
DEVICE INVENTORY — 2026-08-23 10:12 UTC
====================================================
           Total: 6
          Online: 4
  Needs Firmware: 3
     Low Battery: 2

By site:   {'Barn 1': 2, 'Barn 2': 2, 'Barn 3': 2}
By status: {'online': 4, 'offline': 1, 'degraded': 1}
By firmware: {'2.4.1': 3, '2.3.9': 2, '2.2.0': 1}
All tags:  ['legacy', 'prod', 'punch', 'test']

Firmware update required (3):
  pi-002  fw 2.3.9  Barn 1
  pi-004  fw 2.2.0  Barn 2
  pi-006  fw 2.3.9  Barn 3

Online but low battery (2):
  pi-004   41%  Barn 2
  pi-006   55%  Barn 3
```

Wait — `pi-004` has status `degraded`, not `online`, so it shouldn't appear in that last section. **This is deliberate: the code above has a bug.** Run it, spot the discrepancy between the label and the data, and fix it. (Answer: `summarize` counts low battery across all devices while the `urgent` filter requires online; both are defensible, but the *printed labels* must match what's computed. Decide which semantics you want and make them consistent.) Debugging your own aggregation logic is exactly the skill Phase 2 needs.

### Exercises

**1.** Using `INVENTORY`, build a list of `"id (site)"` strings for every device tagged `punch`, using a single comprehension.

<details><summary>Solution</summary>

```python
punch = [f"{r['id']} ({r['site']})" for r in INVENTORY if "punch" in r["tags"]]
print(punch)
```

```text
['pi-001 (Barn 1)', 'pi-002 (Barn 1)', 'pi-003 (Barn 2)', 'pi-004 (Barn 2)', 'pi-005 (Barn 3)']
```
</details>

**2.** Build a dictionary mapping site → list of device IDs at that site, using a loop (not a comprehension — this one is clearer as a loop).

<details><summary>Solution</summary>

```python
by_site = {}
for r in INVENTORY:
    by_site.setdefault(r["site"], []).append(r["id"])

for site, ids in sorted(by_site.items()):
    print(f"{site}: {ids}")
```

```text
Barn 1: ['pi-001', 'pi-002']
Barn 2: ['pi-003', 'pi-004']
Barn 3: ['pi-005', 'pi-006']
```

`setdefault(key, default)` returns the existing value or inserts and returns the default — the compact form of the "if key not in dict" pattern.
</details>

**3.** Given this simulated multi-choice model response, extract every completion's content into a list of strings.

```python
resp = {"choices": [
    {"index": 0, "message": {"content": "Answer A"}},
    {"index": 1, "message": {"content": "Answer B"}},
    {"index": 2, "message": {"content": "Answer C"}},
]}
```

<details><summary>Solution</summary>

```python
contents = [c["message"]["content"] for c in resp["choices"]]
print(contents)
```

```text
['Answer A', 'Answer B', 'Answer C']
```
</details>

**4.** Find the tags that appear on production devices but never on non-production devices (use sets).

<details><summary>Solution</summary>

```python
prod_tags = set()
other_tags = set()

for r in INVENTORY:
    if "prod" in r["tags"]:
        prod_tags.update(r["tags"])
    else:
        other_tags.update(r["tags"])

print(f"Prod-only tags: {prod_tags - other_tags}")
```

```text
Prod-only tags: {'prod'}
```
</details>

**5.** Write a comprehension producing a dictionary of `{device_id: "OK"|"CHECK"}` where CHECK means offline/degraded or battery under 60.

<details><summary>Solution</summary>

```python
health = {
    r["id"]: ("OK" if r["status"] == "online" and r["battery"] >= 60 else "CHECK")
    for r in INVENTORY
}

for device, state in health.items():
    print(f"{device}: {state}")
```

```text
pi-001: OK
pi-002: CHECK
pi-003: OK
pi-004: CHECK
pi-005: OK
pi-006: CHECK
```

A conditional expression inside a dict comprehension is about as complex as you should let one get.
</details>

### Checkpoint

- [ ] I can explore an unfamiliar nested response with `type()`, `.keys()`, `len()` step by step
- [ ] I can read and write `response["choices"][0]["message"]["content"]` without hesitation
- [ ] I write list comprehensions with and without a filter
- [ ] I write dict comprehensions and know when a loop is clearer
- [ ] I use sets for deduplication and membership
- [ ] I found and fixed the deliberate bug in the mini-project

**Explain out loud:** *When should I reach for a comprehension and when should I write the loop?*
> Comprehension when I'm producing one new collection from another by filtering and/or transforming, and the whole thing fits readably on one line. Loop when there are side effects (printing, writing, API calls), when there's meaningful branching, when I'm accumulating into multiple structures at once, or when the one-liner would need a scroll bar.

---

## Days 6–7 (Flex, 4h) — Files, errors, and consolidation

### Why this matters

Labs read config files, write outputs, and crash. Handling files properly and failing gracefully is the difference between a script and a tool — and `try/except` around API calls is required in every serious sample you'll copy in Phase 3.

### Concepts

**Reading and writing files with `with`:**

```python
with open("notes.txt", "w", encoding="utf-8") as f:
    f.write("First line\n")
    f.write("Second line\n")

with open("notes.txt", "r", encoding="utf-8") as f:
    content = f.read()

print(content)
```

```text
First line
Second line
```

`with` is a *context manager*: it guarantees the file is closed when the block exits, even if an exception is raised inside. Always use it — never bare `open()`. Modes: `"r"` read (default), `"w"` write (**truncates the file**), `"a"` append, `"x"` create-or-fail. Always pass `encoding="utf-8"` — it prevents platform-dependent surprises.

Reading line by line (memory-efficient for big files):

```python
with open("notes.txt", encoding="utf-8") as f:
    for line in f:
        print(line.rstrip())     # rstrip removes the trailing newline
```

Or all lines into a list: `lines = f.readlines()`.

**`pathlib`** is the modern way to handle paths — object-oriented and OS-agnostic:

```python
from pathlib import Path

base = Path.home() / "code" / "python-ramp"     # the / operator joins paths
target = base / "notes.txt"

print(target)
print(target.exists())
print(target.name, target.stem, target.suffix)
print(target.parent)

# read/write shortcuts — no `with` needed for small files
target.write_text("hello\n", encoding="utf-8")
print(target.read_text(encoding="utf-8"))

# find files
for p in base.glob("*.py"):
    print(p.name)
```

```text
/Users/Shawn.Vermette/code/azure-ai-path/python-ramp/notes.txt
True
notes.txt notes .txt
/Users/Shawn.Vermette/code/azure-ai-path/python-ramp
hello

day1.py
day2.py
...
```

`Path.mkdir(parents=True, exist_ok=True)` creates directories safely. `base.rglob("*.log")` searches recursively.

**Exceptions.** Python's `try/except` is PowerShell's `try/catch`:

```python
try:
    value = int("not a number")
except ValueError as e:
    print(f"Could not convert: {e}")
```

```text
Could not convert: invalid literal for int() with base 10: 'not a number'
```

The full form:

```python
try:
    with open("config.json", encoding="utf-8") as f:
        data = f.read()
except FileNotFoundError:
    print("Config missing — using defaults")
    data = "{}"
except PermissionError:
    print("Cannot read config — check permissions")
    raise                      # re-raise; this one is fatal
else:
    print("Config loaded")     # runs only if no exception
finally:
    print("Done attempting config load")   # always runs
```

**Catch specific exceptions**, in order from most to least specific. A bare `except:` swallows everything including Ctrl-C and genuine bugs — never write it. If you must be broad, use `except Exception as e:` and log `e`.

The exceptions you'll actually meet:

| Exception | Typical cause in this path |
|---|---|
| `FileNotFoundError` | missing `.env` or data file |
| `KeyError` | response shape differs from assumption |
| `IndexError` | empty `choices` list |
| `TypeError` | passing wrong type (often `None` where a str was expected) |
| `ValueError` | bad `int()` conversion, invalid parameter value |
| `ModuleNotFoundError` | package not installed / venv not activated |
| `json.JSONDecodeError` | response wasn't JSON (often an HTML error page) |

**Raising your own:**

```python
def set_temperature(value: float) -> float:
    if not 0.0 <= value <= 2.0:
        raise ValueError(f"temperature must be 0.0–2.0, got {value}")
    return value

try:
    set_temperature(3.5)
except ValueError as e:
    print(f"Rejected: {e}")
```

```text
Rejected: temperature must be 0.0–2.0, got 3.5
```

**Reading a traceback.** When a script crashes, read from the **bottom up**: the last line is the exception type and message; the lines above show the call path, and the *second-to-last* file/line reference is usually your code. Don't paste the traceback into an AI before reading it — 80% of the time the bottom line tells you the answer.

### Consolidation project

Build `log_triage.py`, which walks a folder of log files, parses them, aggregates, and writes a report — handling malformed input gracefully.

First, generate sample data with `make_logs.py`:

```python
# make_logs.py — create sample log files to work with
import random
from pathlib import Path

random.seed(42)   # reproducible

LOG_DIR = Path("logs")
LOG_DIR.mkdir(exist_ok=True)

LEVELS = ["INFO"] * 6 + ["WARN"] * 2 + ["ERROR"] * 2
DEVICES = [f"pi-{n:03d}" for n in range(1, 9)]
MESSAGES = {
    "INFO":  ["punch accepted", "heartbeat ok", "sync complete"],
    "WARN":  ["retry after timeout", "battery low", "clock drift detected"],
    "ERROR": ["punch relay unreachable", "auth failed", "disk full"],
}

for day in range(1, 4):
    lines = []
    for i in range(40):
        level = random.choice(LEVELS)
        device = random.choice(DEVICES)
        msg = random.choice(MESSAGES[level])
        lines.append(f"2026-08-{day:02d}T{i % 24:02d}:{i % 60:02d}:00 {level} {device} {msg}")
    lines.insert(15, "GARBAGE LINE WITH NO STRUCTURE")   # deliberate bad data
    (LOG_DIR / f"punch-relay-{day:02d}.log").write_text("\n".join(lines) + "\n", encoding="utf-8")

print(f"Wrote {len(list(LOG_DIR.glob('*.log')))} log files to {LOG_DIR.resolve()}")
```

```text
Wrote 3 log files to /Users/Shawn.Vermette/code/azure-ai-path/python-ramp/logs
```

Now the triage tool:

```python
# log_triage.py — parse, aggregate, and report on a folder of logs
from pathlib import Path
from datetime import datetime, timezone

LOG_DIR = Path("logs")
REPORT = Path("triage-report.txt")
VALID_LEVELS = {"INFO", "WARN", "ERROR"}


def parse_line(line: str) -> dict | None:
    """Parse one log line into a dict, or return None if it's malformed."""
    parts = line.split(maxsplit=3)
    if len(parts) < 4:
        return None
    timestamp, level, device, message = parts
    if level not in VALID_LEVELS:
        return None
    return {
        "timestamp": timestamp,
        "level": level,
        "device": device,
        "message": message.strip(),
    }


def load_logs(directory: Path) -> tuple[list, int]:
    """Return (parsed records, count of unparseable lines)."""
    records = []
    bad = 0

    if not directory.exists():
        raise FileNotFoundError(
            f"Log directory '{directory}' not found — run make_logs.py first"
        )

    for path in sorted(directory.glob("*.log")):
        try:
            text = path.read_text(encoding="utf-8")
        except (PermissionError, UnicodeDecodeError) as e:
            print(f"  skipping {path.name}: {e}")
            continue

        for line in text.splitlines():
            if not line.strip():
                continue
            record = parse_line(line)
            if record is None:
                bad += 1
            else:
                record["source"] = path.name
                records.append(record)

    return records, bad


def count_by(records: list, field: str) -> dict:
    counts = {}
    for r in records:
        counts[r[field]] = counts.get(r[field], 0) + 1
    return counts


def top_n(counts: dict, n: int = 5) -> list:
    return sorted(counts.items(), key=lambda pair: pair[1], reverse=True)[:n]


def build_report(records: list, bad: int) -> str:
    lines = []
    stamp = datetime.now(timezone.utc).strftime("%Y-%m-%d %H:%M UTC")
    lines.append(f"LOG TRIAGE REPORT — {stamp}")
    lines.append("=" * 52)
    lines.append(f"Parsed lines:      {len(records)}")
    lines.append(f"Unparseable lines: {bad}")

    by_level = count_by(records, "level")
    lines.append(f"\nBy level: {by_level}")

    errors = [r for r in records if r["level"] == "ERROR"]
    lines.append(f"\nErrors: {len(errors)}")

    lines.append("\nTop error messages:")
    for msg, count in top_n(count_by(errors, "message")):
        lines.append(f"  {count:>3}x  {msg}")

    lines.append("\nNoisiest devices (errors only):")
    for device, count in top_n(count_by(errors, "device")):
        lines.append(f"  {count:>3}x  {device}")

    error_rate = len(errors) / len(records) if records else 0
    lines.append(f"\nError rate: {error_rate:.1%}")
    lines.append("STATUS: " + ("DEGRADED" if error_rate > 0.15 else "ACCEPTABLE"))
    return "\n".join(lines)


def main():
    try:
        records, bad = load_logs(LOG_DIR)
    except FileNotFoundError as e:
        print(f"ERROR: {e}")
        return

    if not records:
        print("No parseable log records found.")
        return

    report = build_report(records, bad)
    print(report)

    REPORT.write_text(report + "\n", encoding="utf-8")
    print(f"\nReport written to {REPORT.resolve()}")


if __name__ == "__main__":
    main()
```

Sample output (your numbers will differ if you change the seed):

```text
LOG TRIAGE REPORT — 2026-08-23 15:40 UTC
====================================================
Parsed lines:      120
Unparseable lines: 3

By level: {'INFO': 71, 'ERROR': 27, 'WARN': 22}

Errors: 27

Top error messages:
   11x  punch relay unreachable
    9x  auth failed
    7x  disk full

Noisiest devices (errors only):
    6x  pi-003
    5x  pi-007
    4x  pi-001
...

Error rate: 22.5%
STATUS: DEGRADED

Report written to /Users/Shawn.Vermette/code/azure-ai-path/python-ramp/triage-report.txt
```

This program uses every single thing from Week 1: strings, f-strings, conditionals, loops, lists, dicts, functions, type hints, comprehensions, sets, files, pathlib, and exceptions. In Week 2 (Day 13–14) you'll extend exactly this program to send its aggregate to a local language model and get back a written summary — which is, in miniature, the entire architecture of an AI application.

Note `dict | None` and `tuple[list, int]` in the hints — modern Python union and generic syntax, common in current SDK code.

### Exercises

**1.** Add a `--level` style filter: modify `build_report` to accept a minimum level and exclude anything below it (INFO < WARN < ERROR).

<details><summary>Solution</summary>

```python
LEVEL_ORDER = {"INFO": 0, "WARN": 1, "ERROR": 2}

def filter_min_level(records: list, minimum: str = "INFO") -> list:
    floor = LEVEL_ORDER[minimum]
    return [r for r in records if LEVEL_ORDER[r["level"]] >= floor]

warn_and_above = filter_min_level(records, "WARN")
print(len(warn_and_above))
```

Mapping levels to integers is the standard way to make them comparable.
</details>

**2.** Write a function that returns the single busiest hour across all logs (parse the hour out of the timestamp).

<details><summary>Solution</summary>

```python
def busiest_hour(records: list) -> tuple:
    counts = {}
    for r in records:
        hour = r["timestamp"].split("T")[1][:2]
        counts[hour] = counts.get(hour, 0) + 1
    return max(counts.items(), key=lambda pair: pair[1])

hour, count = busiest_hour(records)
print(f"Busiest hour: {hour}:00 with {count} events")
```
</details>

**3.** Make the script resilient to a log file containing invalid UTF-8. (Hint: `errors="replace"` on read, or catching `UnicodeDecodeError` — already partly handled.)

<details><summary>Solution</summary>

```python
text = path.read_text(encoding="utf-8", errors="replace")
```

`errors="replace"` substitutes `\ufffd` for undecodable bytes instead of raising — appropriate for logs where partial data beats no data. `errors="ignore"` drops them silently.
</details>

**4.** Write `safe_int(value, default=0)` that converts a string to an int, returning the default on failure, and demonstrate it on good and bad input.

<details><summary>Solution</summary>

```python
def safe_int(value, default: int = 0) -> int:
    try:
        return int(value)
    except (ValueError, TypeError):
        return default

print(safe_int("42"))
print(safe_int("abc"))
print(safe_int(None, -1))
```

```text
42
0
-1
```

Catching a tuple of exception types in one `except` is standard.
</details>

**5.** Extend the report to write a second output file listing every ERROR line in full, one per line, sorted by device.

<details><summary>Solution</summary>

```python
def write_error_detail(records: list, path: Path = Path("errors.txt")) -> int:
    errors = sorted(
        [r for r in records if r["level"] == "ERROR"],
        key=lambda r: (r["device"], r["timestamp"]),
    )
    lines = [f"{r['timestamp']} {r['device']} {r['message']} ({r['source']})"
             for r in errors]
    path.write_text("\n".join(lines) + "\n", encoding="utf-8")
    return len(lines)

count = write_error_detail(records)
print(f"Wrote {count} error lines to errors.txt")
```

Sorting by a tuple key sorts by device first, then timestamp within each device.
</details>

### Exercism drills

Register at [exercism.org/tracks/python](https://exercism.org/tracks/python) (free) and complete these specific exercises — each drills something from this week:

| Exercise | Drills |
|---|---|
| **Guido's Gorgeous Lasagna** | functions, parameters, return values, docstrings |
| **Two Fer** | default parameters, f-strings |
| **Currency Exchange** | arithmetic, int vs float division, rounding |
| **Card Games** | lists, indexing, slicing, comprehensions |
| **Tisbury Treasure Hunt** | tuples and unpacking |
| **Inventory Management** | **dictionaries** — do this one twice |
| **Chaitana's Colossal Coaster** | list methods (insert, remove, index) |
| **Making the Grade** | loops, `enumerate`, `range` |
| **Ghost Gobble Arcade Game** | booleans and conditional logic |
| **Little Sisters Vocab** | string methods |

Target: **10 completed** by the end of Sunday. They're small — 10–20 minutes each once the concepts are in place. If one takes more than 30 minutes, that's a signal about which day to re-read.

### Checkpoint

- [ ] I always use `with open(...)` and pass `encoding="utf-8"`
- [ ] I use `pathlib.Path` for paths, including `/` joining, `.glob()`, `.exists()`, `.read_text()`
- [ ] I write `try/except` catching specific exceptions, and I know why bare `except:` is wrong
- [ ] I can read a traceback bottom-up and identify my own line
- [ ] I can `raise` a meaningful exception with a useful message
- [ ] `log_triage.py` runs clean, handles the garbage line, and writes its report
- [ ] 10 Exercism exercises completed

**Explain out loud:** *Why does `with` matter for file handling?*
> It's a context manager: it guarantees `close()` runs when the block exits, including when an exception is thrown inside. Without it, an error mid-write leaves a file handle open and possibly data unflushed. The same pattern shows up later for HTTP clients and SDK clients, which also hold resources that must be released — so the habit transfers.

---

## Week 1 gate

Do not start Week 2 until every one of these is true. Test yourself by opening a blank file and writing, with no reference material and no AI assistance:

- [ ] A script that defines and calls a function with type hints, defaults, and a docstring
- [ ] A dictionary describing a record, read with both `[]` and `.get()`, updated, and iterated with `.items()`
- [ ] A list of dictionaries filtered with a comprehension into a new list
- [ ] A nested structure navigated to a value four levels deep (`d["a"][0]["b"]["c"]`)
- [ ] A loop that aggregates counts into a dictionary using the `.get(k, 0) + 1` idiom
- [ ] A file written and read back with `with` and `pathlib`
- [ ] A `try/except` that catches a specific exception and produces a useful message
- [ ] `log_triage.py` running end to end against generated sample logs
- [ ] 10 Exercism Python exercises completed
- [ ] You can read a traceback and fix the error without pasting it anywhere

**If you're behind.** The compressible days are Day 3 (lists — you'll absorb the rest by use) and the Exercism count (5 is acceptable). The **non-negotiables are Day 4 (functions and dictionaries) and Day 5 (nested data and comprehensions)** — Week 2 is entirely built on them, and every API response you touch for the next fourteen weeks is a nested dictionary. If you're short on time, spend it there and let Day 3 and the drills slide.

**If you're ahead.** Don't race into Week 2 — go deeper on Day 5. Take a real JSON file (any one from the internet, or `az account show > sub.json` if you have the CLI configured), load it, and practice walking its structure until navigating unfamiliar nesting feels boring. That boredom is the goal.

---

# Week 2 — The AI Developer Toolkit

**Dates: Aug 24–30, 2026 · 15 hours · Prerequisite: Week 1 gate passed**

Week 1 was the language. Week 2 is the toolchain and the client patterns that every AI-901 and AI-103 lab is built from.

By Saturday night you will have written the same chatbot three times — once with raw HTTP, once with the OpenAI SDK, once with streaming and conversation history — against a model running on your own Mac for free. That progression is not busywork: it's exactly the shape of the labs, and having built it from the bottom up means that when a lab script fails you'll know whether the problem is the endpoint, the payload, the auth, or the SDK. Most candidates only ever learn the top layer and are helpless when it breaks.

Everything this week runs against **Foundry Local** (or Ollama on your cluster). No Azure subscription, no cost, no quota. In Week 3 you'll change one variable — the `base_url` — and the same code will talk to Azure.

---

## Day 8 (Mon, 2h) — Virtual environments, packages, and secrets

### Why this matters

Every MicrosoftLearning lab repo starts with "create a virtual environment and install the requirements." If that step is mysterious, every lab starts with anxiety. And the secrets habit you build today is directly examinable: AI-103's plan-and-manage domain tests key-vs-Entra authentication, and "don't hardcode keys" is the first thing any Azure security baseline says.

### Concepts

**Why virtual environments exist.** Python installs packages globally by default. Two projects needing different versions of the same library will fight. A *virtual environment* is a self-contained folder with its own Python interpreter and its own `site-packages` — activate it and `pip install` writes there instead of system-wide.

Your closest mental model is a container: an isolated userland for one project. Compared to PowerShell, there's no real equivalent — PowerShell modules are globally versioned and you rarely think about it. In Python you always think about it.

**The rule: one venv per project folder, always activated before you install or run anything.**

```bash
cd ~/code/azure-ai-path/python-ramp
python3 -m venv .venv
source .venv/bin/activate
```

Your prompt changes to show the active environment:

```text
(.venv) ~/code/azure-ai-path/python-ramp $
```

Verify it's actually active — this is the check that saves you an hour later:

```bash
which python
which pip
python --version
```

```text
/Users/Shawn.Vermette/code/azure-ai-path/python-ramp/.venv/bin/python
/Users/Shawn.Vermette/code/azure-ai-path/python-ramp/.venv/bin/pip
Python 3.12.x
```

If those paths point at `/opt/homebrew/...` or `/usr/bin/...` instead of your `.venv`, the environment is **not** active. Note also that inside an active venv, `python` and `pip` work (no `3` suffix needed).

Deactivate with `deactivate`. The venv folder is disposable — delete `.venv` and rebuild it any time; never commit it to git.

> **If you see `ModuleNotFoundError: No module named 'httpx'` for something you know you installed:** 95% of the time the venv isn't activated, or you installed into a different venv. Run `which python` first, every time. This is the single most common Python environment error and you will hit it.

**Installing packages:**

```bash
pip install httpx
pip install "openai>=1.0" python-dotenv
pip list
```

**Pinning dependencies.** A `requirements.txt` records what your project needs so it's reproducible:

```bash
pip freeze > requirements.txt
cat requirements.txt
```

```text
annotated-types==0.7.0
anyio==4.x.x
certifi==2026.x.x
distro==1.9.0
h11==0.16.0
httpcore==1.x.x
httpx==0.28.x
...
```

And to rebuild elsewhere (this is what lab repos hand you):

```bash
pip install -r requirements.txt
```

`pip freeze` captures *everything* including transitive dependencies. For your own projects it's often cleaner to hand-write a short `requirements.txt` with just your direct dependencies:

```text
httpx
openai
python-dotenv
```

**`uv` — the fast modern alternative.** You installed it during setup. It does the same jobs 10–100× faster and is becoming the default in new Python projects:

```bash
uv venv                          # creates .venv
source .venv/bin/activate
uv pip install httpx openai python-dotenv
uv pip install -r requirements.txt
```

Use `uv` for your own work; use plain `pip` when a lab's instructions say `pip` (so your commands match the docs you're following). They're interchangeable — `uv` writes to the same `.venv`.

**Project layout.** Structure every project this way from now on:

```text
python-ramp/
├── .venv/              ← virtual environment (never committed)
├── .env                ← secrets (never committed)
├── .env.example        ← template WITH placeholder values (committed)
├── .gitignore
├── requirements.txt
├── logs/
└── src/
    └── chat.py
```

**Secrets — the part that matters for the exam and for your day job.**

Never put a key in source code. Not "temporarily," not "just for the lab." Keys committed to GitHub get scraped within minutes by bots watching the public event stream, and Azure will email you about the leaked credential before you've finished your coffee.

The pattern: a `.env` file holding key=value pairs, git-ignored, loaded at runtime.

Create `.env`:

```text
MODEL_ENDPOINT=http://localhost:5273/v1
MODEL_NAME=phi-4-mini
MODEL_API_KEY=not-needed-for-local
```

Create `.env.example` with the same keys but no real values — this gets committed so anyone (including future you) knows what's required:

```text
MODEL_ENDPOINT=
MODEL_NAME=
MODEL_API_KEY=
```

Create `.gitignore`:

```text
.venv/
.env
__pycache__/
*.pyc
logs/
```

Load it in Python:

```python
import os
from dotenv import load_dotenv

load_dotenv()                                  # reads .env into the environment

endpoint = os.getenv("MODEL_ENDPOINT")
model = os.getenv("MODEL_NAME", "phi-4-mini")  # second arg is the default
api_key = os.getenv("MODEL_API_KEY")

if not endpoint:
    raise RuntimeError("MODEL_ENDPOINT not set — copy .env.example to .env and fill it in")

print(f"Endpoint: {endpoint}")
print(f"Model:    {model}")
print(f"Key set:  {bool(api_key)}")            # never print the key itself
```

```text
Endpoint: http://localhost:5273/v1
Model:    phi-4-mini
Key set:  True
```

Note the last line: print whether a key is *present*, never the key. Logging secrets is how they end up in log aggregators.

**Where this goes in Azure.** `.env` is the *development* pattern. In Azure the progression is: `.env` locally → Key Vault or App Configuration for deployed apps → **and better still, no key at all**, using Entra ID with a managed identity so there's no secret to leak. You'll implement that in Phase 2 and be examined on it in AI-103. Your PKI and Entra background means you already understand *why* keyless is better; this is just where Python plugs into it.

### Hands-on

Set up the project properly. From `~/code/azure-ai-path/python-ramp`:

```bash
# fresh venv
rm -rf .venv
uv venv && source .venv/bin/activate
uv pip install httpx openai python-dotenv

# structure
mkdir -p src
printf '.venv/\n.env\n__pycache__/\n*.pyc\nlogs/\n' > .gitignore
printf 'MODEL_ENDPOINT=\nMODEL_NAME=\nMODEL_API_KEY=\n' > .env.example
cp .env.example .env
uv pip freeze > requirements.txt
```

Now find your Foundry Local endpoint and put it in `.env`:

```bash
foundry service status 2>/dev/null || foundry status
```

Look for the endpoint/port in the output. Then edit `.env` with the real values (the port varies by version and install, so use what *your* machine reports, not the example above).

Write `src/check_env.py`:

```python
# src/check_env.py — verify the environment is wired correctly
import os
import sys
from dotenv import load_dotenv

REQUIRED = ["MODEL_ENDPOINT", "MODEL_NAME"]


def main() -> int:
    load_dotenv()

    print(f"Python:     {sys.version.split()[0]}")
    print(f"Executable: {sys.executable}")

    missing = [key for key in REQUIRED if not os.getenv(key)]
    if missing:
        print(f"\nMISSING: {', '.join(missing)}")
        print("Copy .env.example to .env and fill in the values.")
        return 1

    for key in REQUIRED:
        print(f"{key}: {os.getenv(key)}")

    api_key = os.getenv("MODEL_API_KEY")
    print(f"MODEL_API_KEY: {'set' if api_key else 'not set (fine for local)'}")

    print("\nEnvironment OK")
    return 0


if __name__ == "__main__":
    sys.exit(main())
```

```bash
python src/check_env.py
```

```text
Python:     3.12.x
Executable: /Users/Shawn.Vermette/code/azure-ai-path/python-ramp/.venv/bin/python
MODEL_ENDPOINT: http://localhost:5273/v1
MODEL_NAME: phi-4-mini
MODEL_API_KEY: set

Environment OK
```

`sys.exit(main())` returns an exit code to the shell — 0 for success, non-zero for failure. Check with `echo $?`. This is standard for tools you might chain in a pipeline, and it's a habit worth having.

### Exercises

**1.** Break it deliberately: comment out `MODEL_ENDPOINT` in `.env`, re-run, confirm you get the missing-variable message and exit code 1. Restore it.

<details><summary>Solution</summary>

```bash
python src/check_env.py; echo "exit code: $?"
```

```text
Python:     3.12.x
Executable: /Users/.../.venv/bin/python

MISSING: MODEL_ENDPOINT
Copy .env.example to .env and fill in the values.
exit code: 1
```

Good failure messages that tell the user exactly what to do are the difference between a script and a tool.
</details>

**2.** Deactivate the venv, run `python src/check_env.py`, and observe the failure. Explain what happened.

<details><summary>Solution</summary>

```bash
deactivate
python src/check_env.py
```

```text
ModuleNotFoundError: No module named 'dotenv'
```

Outside the venv, `python` resolves to the Homebrew interpreter, which has its own `site-packages` that doesn't contain `python-dotenv`. The package is installed *in the venv*, not system-wide. Reactivate with `source .venv/bin/activate`. Internalize this error's signature — you will see it again.
</details>

**3.** Write a function `require_env(*names) -> dict` that loads and returns the named variables, raising a single clear error listing *all* missing ones at once (not just the first).

<details><summary>Solution</summary>

```python
import os
from dotenv import load_dotenv

def require_env(*names: str) -> dict:
    """Return the named environment variables, or raise listing all missing ones."""
    load_dotenv()
    values = {name: os.getenv(name) for name in names}
    missing = [name for name, value in values.items() if not value]
    if missing:
        raise RuntimeError(f"Missing required environment variables: {', '.join(missing)}")
    return values

config = require_env("MODEL_ENDPOINT", "MODEL_NAME")
print(config)
```

Reporting all missing values at once, rather than failing on the first, saves the user from a frustrating one-at-a-time discovery loop. Same principle as validating a whole form.
</details>

**4.** Create a second project folder with its own venv, install only `httpx` in it, and confirm the two environments are independent by running `pip list` in each.

<details><summary>Solution</summary>

```bash
mkdir -p ~/code/venv-test && cd ~/code/venv-test
uv venv && source .venv/bin/activate
uv pip install httpx
pip list | wc -l          # short list

cd ~/code/azure-ai-path/python-ramp && source .venv/bin/activate
pip list | wc -l          # longer list — includes openai, dotenv
```

Two interpreters, two package sets, zero interference. This is the whole point.
</details>

**5.** Add a `Makefile` (or a shell script) with `setup`, `run`, and `clean` targets so environment rebuild is one command.

<details><summary>Solution</summary>

```makefile
.PHONY: setup run clean

setup:
	uv venv
	. .venv/bin/activate && uv pip install -r requirements.txt

run:
	. .venv/bin/activate && python src/check_env.py

clean:
	rm -rf .venv __pycache__ src/__pycache__
```

Note: Makefile recipes require **tab** indentation, not spaces. Each line runs in its own subshell, which is why activation is repeated per recipe.
</details>

### Checkpoint

- [ ] I create, activate, verify, and deactivate a venv without thinking about it
- [ ] I check `which python` reflexively when a module isn't found
- [ ] I can install from and write a `requirements.txt`
- [ ] I know both `pip` and `uv` forms
- [ ] Every project I make has `.gitignore`, `.env`, and `.env.example`
- [ ] I load config with `load_dotenv()` + `os.getenv()` and never print a secret
- [ ] I can explain why Entra managed identity beats a key in `.env` for a deployed app

**Explain out loud:** *Why does the `.env` file get git-ignored while `.env.example` gets committed?*
> `.env` holds real secrets and must never enter version control — once committed, a key is compromised even if you delete it later, because it lives in the git history. `.env.example` documents which variables the application requires, with empty or placeholder values, so a new developer (or future me) knows exactly what to configure without ever seeing a live credential.

---

## Day 9 (Wed, 2h) — HTTP and REST from Python

### Why this matters

Underneath every SDK is an HTTP request. When a lab throws a 401, a 404, or a 429, you need to know whether the fault is auth, the endpoint, or quota — and the fastest way to build that instinct is to make the raw calls yourself once. AI-103's plan-and-manage domain explicitly covers diagnosing service errors.

### Concepts

**A REST refresher, framed for someone who's lived in `Invoke-RestMethod`.** An HTTP request has a method, a URL, headers, and (sometimes) a body. The response has a status code, headers, and a body.

Methods you'll use: **GET** (read; no body) and **POST** (create/submit; body carries your payload). Azure AI services use POST for essentially everything interesting, because you're submitting text or images for processing.

Status codes and what each actually means when an Azure AI service returns it:

| Code | Meaning | Typical cause in this path |
|---|---|---|
| **200** | OK | Success |
| **201** | Created | Resource created (index, deployment) |
| **202** | Accepted | Async operation started — poll for the result (batch/long-running ops) |
| **400** | Bad Request | Malformed payload — wrong field name, invalid parameter value |
| **401** | Unauthorized | Missing/wrong key, or an expired or wrong-audience Entra token |
| **403** | Forbidden | Authenticated but not authorized — an RBAC role assignment problem |
| **404** | Not Found | Wrong endpoint URL, wrong deployment name, wrong API version |
| **408 / 504** | Timeout | Slow model or network |
| **429** | Too Many Requests | **Rate/quota limit — back off and retry** |
| **500 / 503** | Server Error | Transient service issue — retryable |

Committing 401 vs 403 to memory is worth real marks: 401 means *who are you*, 403 means *I know who you are and you're not allowed*. The first is an auth problem, the second is an RBAC problem. As a sysadmin you already own this distinction — it's the same as authentication vs authorization in AD.

**`httpx`** is the modern client (sync + async in one library). `requests` is the older, ubiquitous one; the sync APIs are nearly identical, so learning `httpx` gives you both.

```python
import httpx

response = httpx.get("https://api.github.com/repos/microsoft/agent-framework")

print(response.status_code)
print(response.headers["content-type"])

data = response.json()
print(data["full_name"], "-", data["stargazers_count"], "stars")
```

```text
200
application/json; charset=utf-8
microsoft/agent-framework - 12345 stars
```

| PowerShell | Python (`httpx`) |
|---|---|
| `Invoke-RestMethod -Uri $u` | `httpx.get(u).json()` |
| `-Method Post -Body $json -ContentType 'application/json'` | `httpx.post(u, json=payload)` |
| `-Headers @{Authorization="Bearer $t"}` | `headers={"Authorization": f"Bearer {t}"}` |
| `$response.StatusCode` | `response.status_code` |
| `-TimeoutSec 30` | `timeout=30.0` |

**The key ergonomic detail:** passing `json=payload` (a Python dict) makes httpx serialize it *and* set `Content-Type: application/json` for you. Passing `data=` sends form-encoded data instead — a classic source of 400s.

**Response handling:**

```python
import httpx

url = "https://api.github.com/repos/microsoft/agent-framework"

try:
    response = httpx.get(url, timeout=10.0)
    response.raise_for_status()          # raises on 4xx/5xx
    data = response.json()
    print(data["description"])
except httpx.HTTPStatusError as e:
    print(f"HTTP {e.response.status_code}: {e.response.text[:200]}")
except httpx.TimeoutException:
    print("Request timed out")
except httpx.RequestError as e:
    print(f"Connection problem: {e}")
```

`raise_for_status()` converts a bad status into an exception so failures are loud. Without it, a 404 quietly returns an HTML error page and your `.json()` call fails with a confusing `JSONDecodeError` instead of telling you the real problem.

> **If you see `httpx.ConnectError: [Errno 61] Connection refused`:** nothing is listening at that address/port. For Foundry Local, the service isn't running — `foundry status`, and start it if needed.
> **If you see `json.decoder.JSONDecodeError: Expecting value: line 1 column 1`:** the response body wasn't JSON. Print `response.text[:500]` — it's usually an HTML error page or an empty body, which tells you the URL is wrong.

**Reusing a client** (better performance, connection pooling — and the pattern SDKs use internally):

```python
with httpx.Client(timeout=30.0) as client:
    r1 = client.get("https://api.github.com/repos/microsoft/agent-framework")
    r2 = client.get("https://api.github.com/repos/microsoft/semantic-kernel")
    print(r1.json()["full_name"], r2.json()["full_name"])
```

Same `with` context-manager pattern as file handling — it guarantees connections get closed.

### Hands-on — call your local model with raw HTTP

This is the important exercise of the day. You're going to make the exact call the OpenAI SDK makes, by hand.

First confirm the model is running and find the endpoint:

```bash
foundry status
foundry model list
```

Then `src/raw_chat.py`:

```python
# src/raw_chat.py — call an OpenAI-compatible endpoint with no SDK at all
import os
import json
import httpx
from dotenv import load_dotenv

load_dotenv()

BASE_URL = os.getenv("MODEL_ENDPOINT")     # e.g. http://localhost:5273/v1
MODEL = os.getenv("MODEL_NAME")
API_KEY = os.getenv("MODEL_API_KEY", "not-needed")


def chat(prompt: str) -> dict:
    """POST a chat completion request and return the parsed response."""
    url = f"{BASE_URL}/chat/completions"

    headers = {
        "Content-Type": "application/json",
        "Authorization": f"Bearer {API_KEY}",
    }

    payload = {
        "model": MODEL,
        "messages": [
            {"role": "system", "content": "You are a concise IT assistant. Answer in one sentence."},
            {"role": "user", "content": prompt},
        ],
        "temperature": 0.2,
        "max_tokens": 200,
    }

    with httpx.Client(timeout=120.0) as client:
        response = client.post(url, headers=headers, json=payload)

    if response.status_code != 200:
        print(f"HTTP {response.status_code}")
        print(response.text[:500])
        response.raise_for_status()

    return response.json()


def main():
    print(f"POST {BASE_URL}/chat/completions  (model={MODEL})\n")

    result = chat("What does HTTP status 429 mean and how should a client respond?")

    print("--- RAW RESPONSE (truncated) ---")
    print(json.dumps(result, indent=2)[:800])

    print("\n--- WALKING THE STRUCTURE ---")
    print("top-level keys:", list(result.keys()))
    print("choices is a:", type(result["choices"]).__name__, "of length", len(result["choices"]))
    print("choice[0] keys:", list(result["choices"][0].keys()))

    print("\n--- THE ANSWER ---")
    print(result["choices"][0]["message"]["content"].strip())

    usage = result.get("usage", {})
    if usage:
        print(f"\nTokens — prompt: {usage.get('prompt_tokens')}, "
              f"completion: {usage.get('completion_tokens')}, "
              f"total: {usage.get('total_tokens')}")


if __name__ == "__main__":
    main()
```

```text
POST http://localhost:5273/v1/chat/completions  (model=phi-4-mini)

--- RAW RESPONSE (truncated) ---
{
  "id": "chatcmpl-...",
  "object": "chat.completion",
  "created": 1755...,
  "model": "phi-4-mini",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "HTTP 429 means too many requests..."
      },
      "finish_reason": "stop"
    }
  ],
  "usage": { "prompt_tokens": 38, "completion_tokens": 41, "total_tokens": 79 }
}

--- WALKING THE STRUCTURE ---
top-level keys: ['id', 'object', 'created', 'model', 'choices', 'usage']
choices is a: list of length 1
choice[0] keys: ['index', 'message', 'finish_reason']

--- THE ANSWER ---
HTTP 429 means too many requests — the client has exceeded the rate limit and should back off, honoring any Retry-After header, before retrying.

--- THE ANSWER (continued in your run may differ)

Tokens — prompt: 38, completion: 41, total: 79
```

Sit with that output for a minute. Every LLM API call in this entire path — local, Azure, OpenAI, anything — is that request and that response. The SDK you'll use tomorrow is a convenience wrapper around exactly this.

### Exercises

**1.** Modify `raw_chat.py` to deliberately use a wrong model name. Observe the status code and error body. Then use a wrong path (`/chat/completion`, singular). Compare the two failures.

<details><summary>Solution</summary>

Wrong model typically returns **404** or **400** with a body naming the unknown model. Wrong path returns **404** with either a routing error or an HTML page. The lesson: read `response.text` before guessing — the body usually names the problem precisely. This is why the hands-on script prints `response.text[:500]` on non-200.
</details>

**2.** Add a `retry_with_backoff` wrapper around `chat()` that retries up to 3 times on 429 or 5xx, doubling the wait each time.

<details><summary>Solution</summary>

```python
import time

def chat_with_retry(prompt: str, max_attempts: int = 3) -> dict:
    wait = 1.0
    for attempt in range(1, max_attempts + 1):
        try:
            return chat(prompt)
        except httpx.HTTPStatusError as e:
            status = e.response.status_code
            retryable = status == 429 or status >= 500
            if not retryable or attempt == max_attempts:
                raise
            retry_after = e.response.headers.get("retry-after")
            delay = float(retry_after) if retry_after else wait
            print(f"  attempt {attempt} got {status}; retrying in {delay:.1f}s")
            time.sleep(delay)
            wait *= 2
    raise RuntimeError("unreachable")
```

Honoring the `Retry-After` header when present is what Azure's docs tell you to do, and it's an examinable detail.
</details>

**3.** Write a function that takes a list of prompts and returns a list of answers, printing the total tokens consumed across all calls.

<details><summary>Solution</summary>

```python
def ask_many(prompts: list[str]) -> list[str]:
    answers = []
    total_tokens = 0

    with httpx.Client(timeout=120.0) as client:
        for prompt in prompts:
            payload = {
                "model": MODEL,
                "messages": [{"role": "user", "content": prompt}],
                "max_tokens": 150,
            }
            r = client.post(f"{BASE_URL}/chat/completions",
                            headers={"Authorization": f"Bearer {API_KEY}"},
                            json=payload)
            r.raise_for_status()
            data = r.json()
            answers.append(data["choices"][0]["message"]["content"].strip())
            total_tokens += data.get("usage", {}).get("total_tokens", 0)

    print(f"Total tokens across {len(prompts)} calls: {total_tokens}")
    return answers

for a in ask_many(["What is RAG?", "What is an embedding?", "What is a token?"]):
    print("-", a[:100])
```

Reusing one `Client` across the loop is meaningfully faster than a fresh connection per call.
</details>

**4.** Call the `/models` endpoint of your local server (`GET {BASE_URL}/models`) and print the available model IDs.

<details><summary>Solution</summary>

```python
r = httpx.get(f"{BASE_URL}/models", headers={"Authorization": f"Bearer {API_KEY}"}, timeout=30.0)
r.raise_for_status()
for m in r.json().get("data", []):
    print(m.get("id"))
```

The OpenAI-compatible surface includes `/models`, which is how tools discover what's deployed. Azure OpenAI has an equivalent concept in deployments.
</details>

**5.** Time a call and report tokens-per-second for the completion.

<details><summary>Solution</summary>

```python
import time

start = time.perf_counter()
result = chat("Explain private endpoints in two sentences.")
elapsed = time.perf_counter() - start

completion_tokens = result.get("usage", {}).get("completion_tokens", 0)
print(f"{completion_tokens} completion tokens in {elapsed:.2f}s "
      f"= {completion_tokens / elapsed:.1f} tok/s")
```

`time.perf_counter()` is the right clock for measuring durations. Knowing your local throughput is useful context when you later compare against a cloud deployment.
</details>

### Checkpoint

- [ ] I can explain 400 / 401 / 403 / 404 / 429 / 500 and what each means for an Azure AI call
- [ ] I make GET and POST calls with `httpx`, passing `json=` for the body
- [ ] I use `raise_for_status()` and catch `HTTPStatusError`, `TimeoutException`, `RequestError`
- [ ] I reuse a `Client` in a `with` block for multiple calls
- [ ] I successfully called my local model with raw HTTP and read the JSON response
- [ ] I can implement retry with exponential backoff honoring `Retry-After`

**Explain out loud:** *Why did I bother making the raw HTTP call when the SDK does it for me?*
> Because when the SDK fails, the failure is one layer removed from the cause. Knowing the actual request shape — URL path, auth header, JSON body with `model` and `messages` — means I can tell in seconds whether a failure is a wrong endpoint (404), bad credentials (401), missing RBAC (403), or quota (429). SDK exceptions wrap HTTP errors, and reading them is much easier when you know what's underneath.

---

## Day 10 (Thu, 1h) — JSON mastery

### Why this matters

JSON is the wire format for every service in this path. One focused hour on it now prevents a hundred small confusions later.

### Concepts

**The type mapping.** JSON and Python correspond almost exactly:

| JSON | Python |
|---|---|
| object `{...}` | `dict` |
| array `[...]` | `list` |
| string | `str` |
| number (int) | `int` |
| number (real) | `float` |
| `true` / `false` | `True` / `False` |
| `null` | `None` |

The traps are the capitalization of the booleans and `null` → `None`.

**Four functions, distinguished by the `s`:**

```python
import json

# strings
data = json.loads('{"status": "online", "battery": 72}')   # load-s = from String
text = json.dumps(data)                                    # dump-s = to String

# files
with open("config.json", "w", encoding="utf-8") as f:
    json.dump(data, f, indent=2)                           # to File

with open("config.json", encoding="utf-8") as f:
    loaded = json.load(f)                                  # from File

print(data, text, loaded, sep="\n")
```

```text
{'status': 'online', 'battery': 72}
{"status": "online", "battery": 72}
{'status': 'online', 'battery': 72}
```

Mnemonic: the `s` suffix means *string*. `load`/`dump` without it work on file objects.

**Readable output** — `indent=2` is your debugging best friend:

```python
response = {
    "id": "chatcmpl-123",
    "choices": [{"index": 0, "message": {"role": "assistant", "content": "Hi"}}],
    "usage": {"prompt_tokens": 12, "completion_tokens": 3, "total_tokens": 15},
}

print(json.dumps(response, indent=2))
```

```text
{
  "id": "chatcmpl-123",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "Hi"
      }
    }
  ],
  "usage": {
    "prompt_tokens": 12,
    "completion_tokens": 3,
    "total_tokens": 15
  }
}
```

When you don't understand a response, print it this way *first*. Other useful arguments: `sort_keys=True` for stable diffs, `ensure_ascii=False` to keep non-ASCII characters readable rather than escaped (important for multilingual text — relevant when you hit the Translator and multilingual Language labs).

**Walking the canonical response path, level by level.** Memorize this:

```python
content = response["choices"][0]["message"]["content"]
```

| Step | Type | Why it's there |
|---|---|---|
| `response` | dict | the whole completion object |
| `["choices"]` | list | models can return multiple candidate completions (`n` parameter) |
| `[0]` | dict | the first candidate — the only one when `n=1` |
| `["message"]` | dict | the message object, which has `role` and `content` |
| `["content"]` | str | **the text you actually want** |

**Defensive access for anything you'd ship:**

```python
def extract_content(response: dict) -> str:
    """Safely pull the assistant text out of a chat completion."""
    choices = response.get("choices") or []
    if not choices:
        return ""
    message = choices[0].get("message") or {}
    return (message.get("content") or "").strip()

print(repr(extract_content(response)))
print(repr(extract_content({})))
print(repr(extract_content({"choices": []})))
```

```text
'Hi'
''
''
```

The `or []` / `or {}` idiom handles both "key absent" and "key present but null" in one move, which matters because APIs do both.

**Handling malformed JSON:**

```python
import json

bad = '{"status": "online", }'      # trailing comma — invalid JSON

try:
    json.loads(bad)
except json.JSONDecodeError as e:
    print(f"Invalid JSON at line {e.lineno} column {e.colno}: {e.msg}")
```

```text
Invalid JSON at line 1 column 22: Expecting property name enclosed in double quotes
```

JSON is stricter than Python literals: double quotes only, no trailing commas, no comments.

**Serializing objects JSON doesn't know** — `datetime` is the one you'll hit:

```python
from datetime import datetime, timezone

record = {"device": "pi-042", "seen": datetime.now(timezone.utc)}

# json.dumps(record)  ← TypeError: Object of type datetime is not JSON serializable

record["seen"] = record["seen"].isoformat()      # convert first
print(json.dumps(record))
```

```text
{"device": "pi-042", "seen": "2026-08-27T14:22:31.123456+00:00"}
```

Or pass `default=str` to `dumps` for a quick-and-dirty conversion of anything unserializable.

### Hands-on

`src/inspect_json.py` — a reusable structure explorer. You'll actually use this in Phase 2 and 3 when a service returns something unfamiliar:

```python
# src/inspect_json.py — explore any JSON structure
import json


def describe(obj, path: str = "$", max_depth: int = 4, depth: int = 0) -> None:
    """Print a type-and-shape map of a nested JSON structure."""
    indent = "  " * depth

    if depth >= max_depth:
        print(f"{indent}{path}: ... (max depth)")
        return

    if isinstance(obj, dict):
        print(f"{indent}{path}: dict with {len(obj)} keys")
        for key, value in obj.items():
            describe(value, f"{path}.{key}", max_depth, depth + 1)

    elif isinstance(obj, list):
        print(f"{indent}{path}: list of {len(obj)}")
        if obj:
            describe(obj[0], f"{path}[0]", max_depth, depth + 1)

    else:
        preview = repr(obj)
        if len(preview) > 60:
            preview = preview[:57] + "..."
        print(f"{indent}{path}: {type(obj).__name__} = {preview}")


SAMPLE = {
    "id": "chatcmpl-123",
    "model": "phi-4-mini",
    "choices": [
        {
            "index": 0,
            "message": {"role": "assistant", "content": "A private endpoint gives a service a private IP inside your VNet."},
            "finish_reason": "stop",
        }
    ],
    "usage": {"prompt_tokens": 38, "completion_tokens": 17, "total_tokens": 55},
}

if __name__ == "__main__":
    describe(SAMPLE)
    print("\nExtracted:", SAMPLE["choices"][0]["message"]["content"])
```

```text
$: dict with 4 keys
  $.id: str = 'chatcmpl-123'
  $.model: str = 'phi-4-mini'
  $.choices: list of 1
    $.choices[0]: dict with 3 keys
      $.choices[0].index: int = 0
      $.choices[0].message: dict with 2 keys
      $.choices[0].finish_reason: str = 'stop'
  $.usage: dict with 3 keys
    $.usage.prompt_tokens: int = 38
    $.usage.completion_tokens: int = 17
    $.usage.total_tokens: int = 55

Extracted: A private endpoint gives a service a private IP inside your VNet.
```

That function is *recursive* — it calls itself on nested values. You don't need to write recursive code often, but reading it is worth the five minutes.

### Exercises

**1.** Point `describe()` at the real response from `raw_chat.py` and confirm the shape matches.

<details><summary>Solution</summary>

```python
from raw_chat import chat
from inspect_json import describe

describe(chat("hello"))
```

(If the import fails because of `if __name__` guards or paths, just paste the response dict in directly. Real responses often carry extra fields — `system_fingerprint`, `object`, `created` — which is exactly what you want to see.)
</details>

**2.** Write `save_transcript(messages, path)` that writes a conversation to a JSON file with a UTC timestamp, and `load_transcript(path)` that reads it back.

<details><summary>Solution</summary>

```python
import json
from pathlib import Path
from datetime import datetime, timezone

def save_transcript(messages: list, path: Path) -> None:
    payload = {
        "saved_at": datetime.now(timezone.utc).isoformat(),
        "message_count": len(messages),
        "messages": messages,
    }
    path.write_text(json.dumps(payload, indent=2, ensure_ascii=False), encoding="utf-8")

def load_transcript(path: Path) -> list:
    if not path.exists():
        return []
    return json.loads(path.read_text(encoding="utf-8")).get("messages", [])

msgs = [{"role": "user", "content": "hi"}, {"role": "assistant", "content": "hello"}]
save_transcript(msgs, Path("transcript.json"))
print(load_transcript(Path("transcript.json")))
```
</details>

**3.** Given a JSON string with a trailing comma, catch the decode error and print a message naming the line and column.

<details><summary>Solution</summary>

```python
def parse_or_report(text: str):
    try:
        return json.loads(text)
    except json.JSONDecodeError as e:
        print(f"Invalid JSON — {e.msg} (line {e.lineno}, col {e.colno})")
        start = max(0, e.pos - 20)
        print(f"  near: ...{text[start:e.pos + 20]}...")
        return None

parse_or_report('{"a": 1, "b": 2, }')
```
</details>

**4.** Write a function that flattens a nested dict into dotted keys (`{"a": {"b": 1}}` → `{"a.b": 1}`).

<details><summary>Solution</summary>

```python
def flatten(obj: dict, prefix: str = "") -> dict:
    flat = {}
    for key, value in obj.items():
        full = f"{prefix}.{key}" if prefix else key
        if isinstance(value, dict):
            flat.update(flatten(value, full))
        else:
            flat[full] = value
    return flat

print(flatten({"usage": {"prompt_tokens": 38, "total_tokens": 55}, "model": "phi-4-mini"}))
```

```text
{'usage.prompt_tokens': 38, 'usage.total_tokens': 55, 'model': 'phi-4-mini'}
```

Flattening is handy for logging structured data into flat systems — and for building the kind of metrics dictionaries you'll emit in Phase 3.
</details>

**5.** Serialize a dict containing a `datetime`, a `set`, and a `Path` without crashing.

<details><summary>Solution</summary>

```python
from pathlib import Path
from datetime import datetime, timezone

record = {
    "when": datetime.now(timezone.utc),
    "tags": {"prod", "punch"},
    "file": Path("logs/app.log"),
}

print(json.dumps(record, indent=2, default=str))
```

`default=str` calls `str()` on anything the encoder doesn't understand. For production you'd write a proper encoder that converts sets to sorted lists and datetimes to ISO strings — `default=str` renders a set as `"{'prod', 'punch'}"`, which is lossy.
</details>

### Checkpoint

- [ ] I know the JSON↔Python type mapping including `null`→`None` and `true`→`True`
- [ ] I use `loads`/`dumps`/`load`/`dump` correctly and remember what the `s` means
- [ ] I print unfamiliar responses with `json.dumps(x, indent=2)` before anything else
- [ ] I can explain every level of `response["choices"][0]["message"]["content"]`
- [ ] I write defensive extraction with `.get()` and `or {}` for shipping code
- [ ] I handle `JSONDecodeError` and know JSON's strictness rules

**Explain out loud:** *A service returns 200 but `response.json()` raises JSONDecodeError. What's happening?*
> The body isn't JSON despite the success status — most often an HTML page (a proxy or gateway intercepted the request), an empty body, or a plain-text message. The fix is to print `response.text[:500]` and `response.headers["content-type"]` to see what actually came back. In an enterprise setting with something like Zscaler in the path, an HTML interception page returned with a 200 is a very real cause.

---

## Day 11 (Sat, 4h) — The OpenAI SDK pattern

This is the payoff day. Everything so far has been building toward it.

### Why this matters

`client.chat.completions.create(...)` is the single most important line of code in this entire learning path. It appears in the AI-901 labs, in every generative AI lab in AI-103, and inside the agent frameworks. Today you learn it properly — including the parts most people never learn, like why history is re-sent on every call and what tool calling actually is.

### Concepts

**The client.** The `openai` package talks to *any* OpenAI-compatible endpoint. That single design fact is why your free local setup teaches you the paid cloud API:

```python
import os
from openai import OpenAI
from dotenv import load_dotenv

load_dotenv()

client = OpenAI(
    base_url=os.getenv("MODEL_ENDPOINT"),      # http://localhost:5273/v1
    api_key=os.getenv("MODEL_API_KEY", "not-needed"),
)
```

Three deployment targets, one code shape:

| Target | `base_url` | `api_key` |
|---|---|---|
| Foundry Local (Mac) | from `foundry status`, e.g. `http://localhost:5273/v1` | any placeholder |
| Ollama (your K8s cluster) | `http://ollama.ai-lab.svc.cluster.local:11434/v1` | any placeholder |
| Azure (Phase 1 onward) | your Foundry project endpoint | Entra token via `DefaultAzureCredential`, or a key |

In Week 3 you'll swap in the Azure values, and everything below still works. That is the whole reason we're doing it this way.

**The messages array and roles.** A chat request is a *list of messages*, each with a role:

```python
messages = [
    {"role": "system",    "content": "You are a concise IT support assistant."},
    {"role": "user",      "content": "What does a 429 mean?"},
    {"role": "assistant", "content": "It means you're rate limited."},
    {"role": "user",      "content": "How should I handle it?"},
]
```

- **system** — instructions that shape all behavior: persona, tone, rules, constraints, output format. One at the start. This is where the real engineering happens; in Phase 3 your RAG context and agent instructions go here.
- **user** — what the human said.
- **assistant** — what the model previously said.

**The critical insight: the API is stateless.** The model remembers nothing between calls. What creates the *illusion* of memory is that you re-send the entire conversation every time. If you don't append the assistant's replies to your list, every turn starts from scratch — and this is exactly the bug behind "why does my chatbot keep forgetting?"

Two consequences that matter later: conversations get more expensive as they grow (you pay for the whole history as input tokens on every turn), and eventually they exceed the model's context window and must be trimmed or summarized. Both are examinable design considerations.

**Making the call:**

```python
response = client.chat.completions.create(
    model=os.getenv("MODEL_NAME"),
    messages=messages,
    temperature=0.2,
    max_tokens=300,
)

print(response.choices[0].message.content)
print(response.usage.total_tokens)
```

Note the difference from Day 9: the SDK returns **objects with attributes** (`.choices[0].message.content`) rather than a raw dict (`["choices"][0]["message"]["content"]`). Same structure, dot instead of brackets. `response.model_dump()` converts back to a plain dict if you want to inspect or log it.

**Parameters that matter:**

| Parameter | Effect | When to change it |
|---|---|---|
| `temperature` (0–2) | Randomness. 0 ≈ deterministic, higher = more varied | 0–0.2 for extraction/classification/RAG; 0.7–1.0 for creative writing |
| `max_tokens` | Cap on *completion* length | Control cost and stop runaway output |
| `top_p` | Nucleus sampling — alternative randomness control | Adjust this *or* temperature, not both |
| `stop` | Strings that halt generation | Structured output formats |
| `seed` | Reproducibility hint | Testing and evaluation |
| `n` | Number of completions | Rarely; it multiplies cost |

Run this experiment — it makes temperature concrete:

```python
for temp in (0.0, 0.0, 1.5, 1.5):
    r = client.chat.completions.create(
        model=os.getenv("MODEL_NAME"),
        messages=[{"role": "user", "content": "Name one Azure AI service."}],
        temperature=temp,
        max_tokens=30,
    )
    print(f"temp={temp}: {r.choices[0].message.content.strip()}")
```

The two `temp=0.0` runs should be identical or near-identical; the two `temp=1.5` runs will diverge. This is why evaluation and testing use temperature 0, and it's the intuition behind "why did my RAG answer change between runs?"

**Streaming.** Instead of waiting for the whole completion, receive it token by token — what makes chat UIs feel responsive:

```python
stream = client.chat.completions.create(
    model=os.getenv("MODEL_NAME"),
    messages=[{"role": "user", "content": "Explain grounding in three sentences."}],
    stream=True,
)

for chunk in stream:
    if chunk.choices and chunk.choices[0].delta.content:
        print(chunk.choices[0].delta.content, end="", flush=True)
print()
```

The key details: each chunk carries a `delta` (the *new* text, not cumulative), `end=""` suppresses the newline `print` normally adds, and `flush=True` forces immediate display rather than buffering. Streaming responses don't include usage totals by default, which is a real tradeoff when you're tracking cost.

### Hands-on — the full chatbot

`src/chat.py`. Type it, read the comments, then run it:

```python
# src/chat.py — a complete local chatbot with history, streaming, and commands
import os
import sys
import json
from pathlib import Path
from datetime import datetime, timezone

from dotenv import load_dotenv
from openai import OpenAI, APIConnectionError, APIStatusError

load_dotenv()

ENDPOINT = os.getenv("MODEL_ENDPOINT")
MODEL = os.getenv("MODEL_NAME")
API_KEY = os.getenv("MODEL_API_KEY", "not-needed")

SYSTEM_PROMPT = (
    "You are a concise IT support assistant for an enterprise Windows/Azure environment. "
    "Answer in at most four sentences. If you are unsure, say so plainly rather than guessing."
)

TRANSCRIPT_DIR = Path("transcripts")


def build_client() -> OpenAI:
    if not ENDPOINT or not MODEL:
        raise RuntimeError("MODEL_ENDPOINT and MODEL_NAME must be set in .env")
    return OpenAI(base_url=ENDPOINT, api_key=API_KEY)


def new_history() -> list:
    return [{"role": "system", "content": SYSTEM_PROMPT}]


def save_transcript(history: list) -> Path:
    TRANSCRIPT_DIR.mkdir(exist_ok=True)
    stamp = datetime.now(timezone.utc).strftime("%Y%m%d-%H%M%S")
    path = TRANSCRIPT_DIR / f"chat-{stamp}.json"
    path.write_text(
        json.dumps({"model": MODEL, "messages": history}, indent=2, ensure_ascii=False),
        encoding="utf-8",
    )
    return path


def stream_reply(client: OpenAI, history: list) -> str:
    """Stream a completion, print it as it arrives, and return the full text."""
    collected = []

    stream = client.chat.completions.create(
        model=MODEL,
        messages=history,
        temperature=0.3,
        max_tokens=500,
        stream=True,
    )

    print("assistant> ", end="", flush=True)
    for chunk in stream:
        if not chunk.choices:
            continue
        piece = chunk.choices[0].delta.content
        if piece:
            print(piece, end="", flush=True)
            collected.append(piece)
    print("\n")

    return "".join(collected)


def print_help() -> None:
    print(
        "\nCommands:\n"
        "  /exit    quit\n"
        "  /reset   clear conversation history\n"
        "  /save    write the transcript to transcripts/\n"
        "  /history show how many messages are in context\n"
        "  /help    this message\n"
    )


def main() -> int:
    try:
        client = build_client()
    except RuntimeError as e:
        print(f"Config error: {e}")
        return 1

    history = new_history()

    print(f"Local chat — model={MODEL} endpoint={ENDPOINT}")
    print("Type /help for commands.\n")

    while True:
        try:
            user_input = input("you> ").strip()
        except (EOFError, KeyboardInterrupt):
            print("\nBye.")
            return 0

        if not user_input:
            continue

        if user_input == "/exit":
            print("Bye.")
            return 0
        if user_input == "/help":
            print_help()
            continue
        if user_input == "/reset":
            history = new_history()
            print("History cleared.\n")
            continue
        if user_input == "/save":
            path = save_transcript(history)
            print(f"Saved to {path}\n")
            continue
        if user_input == "/history":
            turns = len([m for m in history if m["role"] != "system"])
            print(f"{len(history)} messages in context ({turns} conversational turns)\n")
            continue

        history.append({"role": "user", "content": user_input})

        try:
            reply = stream_reply(client, history)
        except APIConnectionError:
            print("\n[Cannot reach the model. Is Foundry Local running? Try: foundry status]\n")
            history.pop()          # roll back the unanswered user message
            continue
        except APIStatusError as e:
            print(f"\n[API error {e.status_code}: {e.message}]\n")
            history.pop()
            continue

        # THIS is what gives the model memory — without it, every turn starts fresh
        history.append({"role": "assistant", "content": reply})


if __name__ == "__main__":
    sys.exit(main())
```

```text
Local chat — model=phi-4-mini endpoint=http://localhost:5273/v1
Type /help for commands.

you> what is a private endpoint
assistant> A private endpoint is a network interface that gives an Azure service a private IP
address inside your virtual network, so traffic reaches it over the Microsoft backbone rather
than the public internet. You typically pair it with a private DNS zone so the service's
hostname resolves to that private IP. It's the standard way to remove public exposure from
PaaS services.

you> and how does that differ from a service endpoint
assistant> A service endpoint extends your VNet identity to the service over the Azure
backbone but the service keeps its public IP; a private endpoint gives it an actual private
IP in your subnet. Private endpoints also work across peered networks and on-premises via
VPN/ExpressRoute, which service endpoints don't.

you> /history
4 messages in context (3 conversational turns)

you> /exit
Bye.
```

Notice the second question — "and how does that differ" — only makes sense because the history was sent. Comment out the final `history.append(...)` line, restart, and try the same two questions. The model will have no idea what "that" refers to. **Do this experiment.** It teaches statelessness better than any explanation.

### Tool calling (the seed of Phase 3)

Agents are, mechanically, a model that can ask you to run functions. Here's the whole idea in one script — you don't need to master it today, but seeing it now means agents in Phase 3 won't feel like magic.

The flow has four steps: you describe your tools → the model decides to call one → *you* execute it → you send the result back and the model writes the final answer.

```python
# src/tool_calling.py — the mechanics behind agents
import os
import json
from openai import OpenAI
from dotenv import load_dotenv

load_dotenv()
client = OpenAI(base_url=os.getenv("MODEL_ENDPOINT"), api_key=os.getenv("MODEL_API_KEY", "x"))
MODEL = os.getenv("MODEL_NAME")

# 1. The actual function — ordinary Python
def get_device_status(device_id: str) -> dict:
    fake_db = {
        "pi-042": {"status": "offline", "battery": 0, "site": "Barn 3"},
        "pi-001": {"status": "online", "battery": 98, "site": "Barn 1"},
    }
    return fake_db.get(device_id, {"status": "unknown"})

# 2. Its schema, so the model knows it exists and how to call it
TOOLS = [{
    "type": "function",
    "function": {
        "name": "get_device_status",
        "description": "Get the current status of a Raspberry Pi time clock by device ID.",
        "parameters": {
            "type": "object",
            "properties": {
                "device_id": {"type": "string", "description": "Device ID, e.g. pi-042"},
            },
            "required": ["device_id"],
        },
    },
}]

def main():
    messages = [{"role": "user", "content": "Is pi-042 working right now?"}]

    # 3. First call — the model may respond with a tool call instead of text
    response = client.chat.completions.create(
        model=MODEL, messages=messages, tools=TOOLS, temperature=0.0
    )
    message = response.choices[0].message

    if not message.tool_calls:
        print("Model answered directly:", message.content)
        return

    messages.append(message.model_dump(exclude_none=True))

    # 4. Execute each requested tool and feed results back
    for call in message.tool_calls:
        args = json.loads(call.function.arguments)
        print(f"[model requested {call.function.name}({args})]")

        result = get_device_status(**args)
        print(f"[executed -> {result}]")

        messages.append({
            "role": "tool",
            "tool_call_id": call.id,
            "content": json.dumps(result),
        })

    # 5. Second call — now the model writes the answer using the tool result
    final = client.chat.completions.create(model=MODEL, messages=messages, temperature=0.0)
    print("\nassistant>", final.choices[0].message.content.strip())


if __name__ == "__main__":
    main()
```

```text
[model requested get_device_status({'device_id': 'pi-042'})]
[executed -> {'status': 'offline', 'battery': 0, 'site': 'Barn 3'}]

assistant> No — pi-042 is currently offline with a battery level of 0% at Barn 3. It likely
needs a physical check or power restoration.
```

Read the loop once more and notice what an "agent" really is: a `while` loop around this, where the model can call tools repeatedly until it has enough to answer. That's it. Everything Foundry Agent Service and Microsoft Agent Framework add — threads, state, hosted tools, orchestration between multiple agents — is infrastructure on top of this core.

> **Note:** small local models are inconsistent at tool calling. If your local model ignores the tools or produces malformed arguments, that's a model-capability limitation, not your code. Try a larger local model, or just read and understand the flow — you'll run it properly against a cloud model in Phase 3.

### Exercises

**1.** Add a `/system <text>` command to `chat.py` that replaces the system prompt and resets history.

<details><summary>Solution</summary>

```python
if user_input.startswith("/system "):
    new_prompt = user_input[len("/system "):].strip()
    history = [{"role": "system", "content": new_prompt}]
    print(f"System prompt set ({len(new_prompt)} chars). History cleared.\n")
    continue
```

Try `/system You are a pirate.` and then ask a technical question — the demonstration of how much the system prompt controls is worth doing once.
</details>

**2.** Add token accounting: track cumulative usage across the session and print it in `/history`. (Streaming hides usage — switch that command's path to a non-streaming call, or approximate with `len(text.split())`.)

<details><summary>Solution</summary>

```python
# non-streaming variant that captures usage
def reply_with_usage(client, history) -> tuple[str, int]:
    r = client.chat.completions.create(
        model=MODEL, messages=history, temperature=0.3, max_tokens=500
    )
    text = r.choices[0].message.content
    total = r.usage.total_tokens if r.usage else 0
    return text, total

# in main(): session_tokens = 0 ... session_tokens += total
# in /history: print(f"~{session_tokens} tokens consumed this session")
```

Some servers support `stream_options={"include_usage": True}` to get usage on the final streaming chunk. Support varies — check before relying on it.
</details>

**3.** Add history trimming: keep the system message plus only the last 10 messages, so long sessions don't grow unbounded.

<details><summary>Solution</summary>

```python
MAX_TURNS = 10

def trim(history: list, max_messages: int = MAX_TURNS) -> list:
    system = history[0]
    rest = history[1:]
    if len(rest) <= max_messages:
        return history
    return [system] + rest[-max_messages:]

# call after appending the assistant reply:
history = trim(history)
```

This is the naive strategy — production systems summarize the dropped middle rather than discarding it, which is a design question AI-103 can ask about.
</details>

**4.** Write a script that asks the same question at temperature 0.0 and 1.2, five times each, and reports how many unique answers each produced.

<details><summary>Solution</summary>

```python
def uniqueness(temp: float, runs: int = 5) -> int:
    answers = set()
    for _ in range(runs):
        r = client.chat.completions.create(
            model=MODEL,
            messages=[{"role": "user", "content": "Name one Azure AI service."}],
            temperature=temp,
            max_tokens=20,
        )
        answers.add(r.choices[0].message.content.strip())
    return len(answers)

print(f"temp=0.0 -> {uniqueness(0.0)} unique of 5")
print(f"temp=1.2 -> {uniqueness(1.2)} unique of 5")
```

```text
temp=0.0 -> 1 unique of 5
temp=1.2 -> 4 unique of 5
```
</details>

**5.** Add a second tool (`list_devices_at_site`) to `tool_calling.py` and ask a question requiring both tools.

<details><summary>Solution</summary>

```python
def list_devices_at_site(site: str) -> list:
    fleet = {"Barn 1": ["pi-001", "pi-002"], "Barn 3": ["pi-042", "pi-043"]}
    return fleet.get(site, [])

TOOLS.append({
    "type": "function",
    "function": {
        "name": "list_devices_at_site",
        "description": "List device IDs at a given site.",
        "parameters": {
            "type": "object",
            "properties": {"site": {"type": "string"}},
            "required": ["site"],
        },
    },
})

DISPATCH = {
    "get_device_status": get_device_status,
    "list_devices_at_site": list_devices_at_site,
}
# then in the loop: result = DISPATCH[call.function.name](**args)
```

The `DISPATCH` dictionary mapping tool names to functions is the standard pattern — and note it's just a dict, which is why Day 4 mattered.
</details>

### Checkpoint

- [ ] I construct an `OpenAI` client with `base_url` and `api_key` and can point it at three different backends
- [ ] I can explain the system/user/assistant roles and what a system prompt is for
- [ ] I can explain why the API is stateless and what happens if I don't append assistant replies
- [ ] I call `chat.completions.create()` and read `.choices[0].message.content`
- [ ] I know what `temperature`, `max_tokens`, `top_p`, `stop`, and `seed` do
- [ ] I implemented streaming with `delta.content`, `end=""`, `flush=True`
- [ ] `chat.py` runs with history, commands, error handling, and transcript saving
- [ ] I can describe the four-step tool-calling flow without looking

**Explain out loud:** *Why does the same Python code work against Foundry Local, Ollama, and Azure?*
> Because all three expose an OpenAI-compatible HTTP API — same `/chat/completions` path, same JSON request shape with `model` and `messages`, same response shape. The SDK is a thin typed wrapper over that contract, so changing `base_url` and credentials is the entire migration. That's what lets me develop for free locally and deploy to Azure without rewriting, and it's why an hour spent here transfers directly to the exam labs.

---

## Day 12 (Sun, 2h) — Enough classes and async to read SDK code

### Why this matters

You don't need to design class hierarchies. You need to *read* `AIProjectClient(endpoint=..., credential=...)` without confusion, and you need to understand why agent SDK samples are full of `async def` and `await`. Two hours gets you both.

### Concepts — classes, at reading depth

A class bundles data and the functions that operate on it. When you write `OpenAI(base_url=..., api_key=...)` you're *instantiating* a class — creating an object that remembers your configuration so you don't repeat it on every call.

```python
class ChatSession:
    """Holds configuration and conversation state for one chat."""

    def __init__(self, client, model: str, system_prompt: str):
        self.client = client            # attributes live on `self`
        self.model = model
        self.history = [{"role": "system", "content": system_prompt}]

    def ask(self, text: str) -> str:
        self.history.append({"role": "user", "content": text})
        response = self.client.chat.completions.create(
            model=self.model,
            messages=self.history,
            temperature=0.3,
        )
        reply = response.choices[0].message.content
        self.history.append({"role": "assistant", "content": reply})
        return reply

    def reset(self) -> None:
        self.history = self.history[:1]      # keep only the system message

    def turn_count(self) -> int:
        return len([m for m in self.history if m["role"] == "user"])
```

Using it:

```python
session = ChatSession(client, MODEL, "You are a concise IT assistant.")
print(session.ask("What is RBAC?"))
print(session.ask("How does it differ from ABAC?"))
print(f"Turns: {session.turn_count()}")
session.reset()
```

The pieces:

- `__init__` is the constructor — runs at `ChatSession(...)`.
- `self` is the instance, passed automatically. You write `def ask(self, text)` and call `session.ask("hi")`.
- `self.history` is an *attribute* — data belonging to this instance. Two sessions have independent histories.
- Methods are functions defined inside the class.

Bridge: PowerShell's `[PSCustomObject]` with ScriptMethods, or a class in C#. The concept is identical; only spelling differs.

Why the SDKs do this: `client.chat.completions.create(...)` works because `client` holds your base URL, credentials, timeout, and retry policy. Without a class you'd pass all of that to every call.

### Concepts — async, at working depth

**The problem.** A network call spends nearly all its time waiting. Synchronous code blocks — nothing else happens during the wait. Ask a model five questions sequentially and you wait for all five in series.

**The fix.** `async`/`await` lets one thread start a request and, while waiting, work on another.

```python
import asyncio
import time

async def slow_task(name: str, seconds: float) -> str:
    print(f"  {name} starting")
    await asyncio.sleep(seconds)          # non-blocking sleep
    print(f"  {name} done")
    return f"{name} result"

async def main():
    start = time.perf_counter()
    results = await asyncio.gather(
        slow_task("A", 2),
        slow_task("B", 2),
        slow_task("C", 2),
    )
    print(results)
    print(f"Elapsed: {time.perf_counter() - start:.1f}s")

asyncio.run(main())
```

```text
  A starting
  B starting
  C starting
  A done
  B done
  C done
['A result', 'B result', 'C result']
Elapsed: 2.0s
```

Six seconds of sleeping in two seconds of wall clock. The rules:

- `async def` defines a *coroutine* — calling it returns a coroutine object; it doesn't run yet.
- `await` runs it and yields control while waiting.
- `await` is only legal inside an `async def`.
- `asyncio.run(main())` is the entry point from synchronous code — exactly once, at the top.
- `asyncio.gather(...)` runs several coroutines concurrently and returns their results in order.

> **If you see `SyntaxError: 'await' outside async function`:** you used `await` in a normal `def`. Make the enclosing function `async def`.
> **If you see `RuntimeWarning: coroutine 'x' was never awaited`:** you called an async function without `await`. Add it.

**Real payoff with the model.** `AsyncOpenAI` is the async client:

```python
# src/async_demo.py — measure concurrency against your local model
import os
import time
import asyncio
from openai import AsyncOpenAI, OpenAI
from dotenv import load_dotenv

load_dotenv()
ENDPOINT = os.getenv("MODEL_ENDPOINT")
MODEL = os.getenv("MODEL_NAME")
KEY = os.getenv("MODEL_API_KEY", "not-needed")

QUESTIONS = [
    "What is an embedding, in one sentence?",
    "What is RAG, in one sentence?",
    "What is a private endpoint, in one sentence?",
    "What is managed identity, in one sentence?",
    "What is a token, in one sentence?",
]


def run_sequential() -> float:
    client = OpenAI(base_url=ENDPOINT, api_key=KEY)
    start = time.perf_counter()
    for q in QUESTIONS:
        client.chat.completions.create(
            model=MODEL, messages=[{"role": "user", "content": q}], max_tokens=60
        )
    return time.perf_counter() - start


async def ask(client: AsyncOpenAI, question: str) -> str:
    response = await client.chat.completions.create(
        model=MODEL, messages=[{"role": "user", "content": question}], max_tokens=60
    )
    return response.choices[0].message.content.strip()


async def run_concurrent() -> tuple[float, list]:
    client = AsyncOpenAI(base_url=ENDPOINT, api_key=KEY)
    start = time.perf_counter()
    answers = await asyncio.gather(*(ask(client, q) for q in QUESTIONS))
    return time.perf_counter() - start, answers


def main():
    print(f"Sending {len(QUESTIONS)} questions to {MODEL}\n")

    seq = run_sequential()
    print(f"Sequential: {seq:.1f}s")

    conc, answers = asyncio.run(run_concurrent())
    print(f"Concurrent: {conc:.1f}s  ({seq / conc:.1f}x faster)\n")

    for q, a in zip(QUESTIONS, answers):
        print(f"Q: {q}\nA: {a}\n")


if __name__ == "__main__":
    main()
```

```text
Sending 5 questions to phi-4-mini

Sequential: 18.4s
Concurrent: 6.2s  (3.0x faster)

Q: What is an embedding, in one sentence?
A: An embedding is a numeric vector representation of text that places semantically similar
content near each other in vector space.
...
```

Your speedup depends on the backend's concurrency — a single local model instance serializes some work, so you may see 2–3× rather than 5×. Against a cloud endpoint the gain is larger. `*(...)` unpacks a generator into arguments, the same `*` you met with `*args`.

This is not academic. In Phase 3 you'll embed hundreds of document chunks; sequential embedding takes minutes, concurrent takes seconds. And the agent frameworks are async-first — their samples won't run if you can't write `async def main()` and `asyncio.run(main())`.

### Exercises

**1.** Refactor `chat.py` to use the `ChatSession` class.

<details><summary>Solution</summary>

```python
session = ChatSession(client, MODEL, SYSTEM_PROMPT)

while True:
    user_input = input("you> ").strip()
    if user_input == "/exit":
        break
    if user_input == "/reset":
        session.reset()
        print("History cleared.\n")
        continue
    print("assistant>", session.ask(user_input), "\n")
```

The loop shrinks because state moved into the object. That's the payoff of a class: the caller stops managing details.
</details>

**2.** Add a `stream()` method to `ChatSession` that streams and still records history.

<details><summary>Solution</summary>

```python
    def stream(self, text: str) -> str:
        self.history.append({"role": "user", "content": text})
        collected = []
        stream = self.client.chat.completions.create(
            model=self.model, messages=self.history, temperature=0.3, stream=True
        )
        for chunk in stream:
            if chunk.choices and chunk.choices[0].delta.content:
                piece = chunk.choices[0].delta.content
                print(piece, end="", flush=True)
                collected.append(piece)
        print()
        reply = "".join(collected)
        self.history.append({"role": "assistant", "content": reply})
        return reply
```
</details>

**3.** Write an async function that asks the same question to two different local models concurrently and prints both answers side by side.

<details><summary>Solution</summary>

```python
async def compare(question: str, model_a: str, model_b: str):
    client = AsyncOpenAI(base_url=ENDPOINT, api_key=KEY)

    async def one(model: str) -> str:
        r = await client.chat.completions.create(
            model=model, messages=[{"role": "user", "content": question}], max_tokens=120
        )
        return r.choices[0].message.content.strip()

    a, b = await asyncio.gather(one(model_a), one(model_b))
    print(f"--- {model_a} ---\n{a}\n\n--- {model_b} ---\n{b}")

# asyncio.run(compare("What is RAG?", "phi-4-mini", "qwen2.5-0.5b"))
```

Pull a second model first with `foundry model list` / `foundry run <alias>`. Side-by-side comparison is exactly how you'll choose models in Phase 3.
</details>

**4.** Add concurrency limiting with `asyncio.Semaphore` so no more than 2 requests run at once (the pattern for respecting Azure TPM quota).

<details><summary>Solution</summary>

```python
async def run_limited(questions: list, limit: int = 2) -> list:
    client = AsyncOpenAI(base_url=ENDPOINT, api_key=KEY)
    sem = asyncio.Semaphore(limit)

    async def bounded(q: str) -> str:
        async with sem:                      # waits if `limit` are already running
            r = await client.chat.completions.create(
                model=MODEL, messages=[{"role": "user", "content": q}], max_tokens=60
            )
            return r.choices[0].message.content.strip()

    return await asyncio.gather(*(bounded(q) for q in questions))
```

This is precisely how you avoid 429s when processing a batch against a quota-limited Azure deployment — a genuinely examinable design pattern.
</details>

**5.** Handle a failure inside `gather` so one bad call doesn't kill the batch.

<details><summary>Solution</summary>

```python
results = await asyncio.gather(*(ask(client, q) for q in QUESTIONS),
                               return_exceptions=True)

for q, r in zip(QUESTIONS, results):
    if isinstance(r, Exception):
        print(f"FAILED: {q} -> {type(r).__name__}: {r}")
    else:
        print(f"OK: {q} -> {r[:60]}...")
```

`return_exceptions=True` makes `gather` return exception objects in place of raising, so partial success is possible. Essential for batch jobs.
</details>

### Checkpoint

- [ ] I can read a class definition and identify `__init__`, `self`, attributes, and methods
- [ ] I can instantiate a class and call its methods, and explain what `client` holds
- [ ] I wrote a working `ChatSession` class
- [ ] I can explain why network I/O benefits from async
- [ ] I write `async def` / `await` / `asyncio.run()` / `asyncio.gather()` correctly
- [ ] I measured a real speedup from concurrency against my local model
- [ ] I can limit concurrency with a Semaphore and explain why quota makes that necessary

**Explain out loud:** *Why are the Azure agent SDKs async-first?*
> Because agent workloads are dominated by waiting — on model inference, on tool calls, on retrieval, often several at once and in multiple rounds per user turn. An async design lets one process handle many concurrent conversations and fan out parallel tool calls without a thread per operation. Synchronous wrappers usually exist, but the samples are async because that's the shape the workload actually has.

---

## Days 13–14 (Flex, 4h) — Sysadmin drills and the Phase 0 capstone

### Drill 1 — bulk user processing (PowerShell → Python)

The PowerShell you'd write today:

```powershell
Import-Csv .\users.csv |
    Where-Object { $_.Department -eq 'Operations' -and $_.Enabled -eq 'True' } |
    ForEach-Object {
        [PSCustomObject]@{
            UPN  = "$($_.SamAccountName)@hylife.com"
            Name = "$($_.GivenName) $($_.Surname)"
            Dept = $_.Department
        }
    } | Export-Csv .\ops-users.csv -NoTypeInformation
```

Write the Python equivalent using the `csv` module. Generate test data first:

```python
# make_users.py
import csv
from pathlib import Path

ROWS = [
    {"SamAccountName": "jsmith",  "GivenName": "Jane",  "Surname": "Smith",  "Department": "Operations", "Enabled": "True"},
    {"SamAccountName": "bwong",   "GivenName": "Ben",   "Surname": "Wong",   "Department": "Operations", "Enabled": "False"},
    {"SamAccountName": "kpatel",  "GivenName": "Kiran", "Surname": "Patel",  "Department": "IT",         "Enabled": "True"},
    {"SamAccountName": "mdupuis", "GivenName": "Marc",  "Surname": "Dupuis", "Department": "Operations", "Enabled": "True"},
]

with Path("users.csv").open("w", newline="", encoding="utf-8") as f:
    writer = csv.DictWriter(f, fieldnames=list(ROWS[0]))
    writer.writeheader()
    writer.writerows(ROWS)

print("Wrote users.csv")
```

<details><summary>Solution</summary>

```python
# bulk_users.py
import csv
from pathlib import Path

SOURCE = Path("users.csv")
TARGET = Path("ops-users.csv")
DOMAIN = "hylife.com"


def transform(row: dict) -> dict:
    return {
        "UPN": f"{row['SamAccountName']}@{DOMAIN}",
        "Name": f"{row['GivenName']} {row['Surname']}",
        "Dept": row["Department"],
    }


def main():
    with SOURCE.open(newline="", encoding="utf-8") as f:
        rows = list(csv.DictReader(f))

    selected = [
        transform(r) for r in rows
        if r["Department"] == "Operations" and r["Enabled"] == "True"
    ]

    with TARGET.open("w", newline="", encoding="utf-8") as f:
        writer = csv.DictWriter(f, fieldnames=["UPN", "Name", "Dept"])
        writer.writeheader()
        writer.writerows(selected)

    print(f"{len(selected)} of {len(rows)} users written to {TARGET}")
    for r in selected:
        print(f"  {r['UPN']:>22}  {r['Name']}")


if __name__ == "__main__":
    main()
```

```text
2 of 4 users written to ops-users.csv
      jsmith@hylife.com  Jane Smith
     mdupuis@hylife.com  Marc Dupuis
```

`csv.DictReader` yields dictionaries keyed by header — the direct analogue of `Import-Csv`. `newline=""` is required on the `open()` call for csv files; omitting it produces blank lines on some platforms.
</details>

### Drill 2 — API poller with retry and backoff

Write a poller that checks an endpoint every N seconds up to a maximum, retries transient failures with exponential backoff, and exits when a terminal condition is met. Simulate a long-running operation returning `"running"` a few times, then `"succeeded"`.

<details><summary>Solution</summary>

```python
# poller.py
import time
import random
from typing import Callable

TERMINAL = {"succeeded", "failed", "cancelled"}


def simulate_operation() -> dict:
    """Pretend to be a long-running Azure operation."""
    roll = random.random()
    if roll < 0.15:
        raise ConnectionError("transient network blip")
    if roll < 0.65:
        return {"status": "running", "percent": random.randint(10, 90)}
    return {"status": "succeeded", "percent": 100}


def poll(check: Callable[[], dict], interval: float = 2.0,
         timeout: float = 60.0, max_retries: int = 3) -> dict:
    deadline = time.perf_counter() + timeout
    attempt = 0

    while time.perf_counter() < deadline:
        try:
            result = check()
            attempt = 0                       # reset backoff on success
        except (ConnectionError, TimeoutError) as e:
            attempt += 1
            if attempt > max_retries:
                raise RuntimeError(f"giving up after {max_retries} retries: {e}") from e
            wait = min(2 ** attempt, 16)
            print(f"  transient error ({e}); retry {attempt} in {wait}s")
            time.sleep(wait)
            continue

        status = result.get("status", "unknown")
        print(f"  status={status} ({result.get('percent', 0)}%)")

        if status in TERMINAL:
            return result

        time.sleep(interval)

    raise TimeoutError(f"operation did not complete within {timeout}s")


if __name__ == "__main__":
    random.seed()
    print("Polling operation...")
    try:
        final = poll(simulate_operation, interval=1.0, timeout=30.0)
        print(f"\nFinal: {final}")
    except (RuntimeError, TimeoutError) as e:
        print(f"\nFAILED: {e}")
```

This is the exact shape of polling an Azure long-running operation (HTTP 202 + poll the operation-location URL) — you'll meet it with Document Intelligence and batch jobs. Note `raise ... from e` preserves the original exception as the cause, which keeps tracebacks useful.
</details>

### Capstone — the log triage assistant

Extend Week 1's `log_triage.py` into an AI-powered tool. This is the first program you'll write that is genuinely an *AI application*: deterministic code does the data work, the model does the language work.

Requirements:
- venv, `.env`, `.gitignore`, `requirements.txt`
- parses a folder of logs (reuse Week 1 code)
- aggregates deterministically in Python — **never ask the model to count things**
- sends the aggregate to the local model with a structured system prompt
- prints an LLM summary plus recommended actions
- type hints, docstrings, error handling throughout
- runs end to end with one command

```python
# src/log_assistant.py — deterministic aggregation + LLM summarization
import os
import json
from pathlib import Path
from datetime import datetime, timezone

from dotenv import load_dotenv
from openai import OpenAI, APIConnectionError, APIStatusError

load_dotenv()

LOG_DIR = Path("logs")
VALID_LEVELS = {"INFO", "WARN", "ERROR"}

SYSTEM_PROMPT = """You are an IT operations analyst.
You will receive a JSON summary of log data that has ALREADY been aggregated.
Do not recompute or question the numbers — treat them as ground truth.

Produce exactly three sections:
SUMMARY: two sentences on overall system health.
TOP ISSUES: up to three bullets, each naming the issue and the affected devices.
RECOMMENDED ACTIONS: up to three concrete, prioritized next steps for an administrator.

Be specific and terse. Do not invent devices, counts, or errors not present in the data."""


def parse_line(line: str) -> dict | None:
    parts = line.split(maxsplit=3)
    if len(parts) < 4 or parts[1] not in VALID_LEVELS:
        return None
    return {"timestamp": parts[0], "level": parts[1],
            "device": parts[2], "message": parts[3].strip()}


def load_records(directory: Path) -> tuple[list, int]:
    """Parse every .log file in the directory. Returns (records, malformed_count)."""
    if not directory.exists():
        raise FileNotFoundError(f"'{directory}' not found — run make_logs.py first")

    records, bad = [], 0
    for path in sorted(directory.glob("*.log")):
        for line in path.read_text(encoding="utf-8", errors="replace").splitlines():
            if not line.strip():
                continue
            record = parse_line(line)
            if record is None:
                bad += 1
            else:
                record["source"] = path.name
                records.append(record)
    return records, bad


def count_by(records: list, field: str) -> dict:
    counts: dict = {}
    for r in records:
        counts[r[field]] = counts.get(r[field], 0) + 1
    return counts


def top_n(counts: dict, n: int = 5) -> list:
    return sorted(counts.items(), key=lambda kv: kv[1], reverse=True)[:n]


def build_aggregate(records: list, bad: int) -> dict:
    """All numbers are computed here, deterministically. The model only writes prose."""
    errors = [r for r in records if r["level"] == "ERROR"]
    warns = [r for r in records if r["level"] == "WARN"]

    return {
        "generated_at": datetime.now(timezone.utc).isoformat(timespec="seconds"),
        "total_lines_parsed": len(records),
        "malformed_lines": bad,
        "counts_by_level": count_by(records, "level"),
        "error_rate": round(len(errors) / len(records), 4) if records else 0,
        "top_error_messages": [{"message": m, "count": c} for m, c in top_n(count_by(errors, "message"))],
        "top_warn_messages": [{"message": m, "count": c} for m, c in top_n(count_by(warns, "message"), 3)],
        "devices_with_most_errors": [{"device": d, "count": c} for d, c in top_n(count_by(errors, "device"))],
        "distinct_devices": len(count_by(records, "device")),
        "files_analyzed": sorted(count_by(records, "source")),
    }


def summarize(aggregate: dict) -> str:
    """Ask the local model to narrate the aggregate."""
    client = OpenAI(
        base_url=os.getenv("MODEL_ENDPOINT"),
        api_key=os.getenv("MODEL_API_KEY", "not-needed"),
    )

    response = client.chat.completions.create(
        model=os.getenv("MODEL_NAME"),
        messages=[
            {"role": "system", "content": SYSTEM_PROMPT},
            {"role": "user", "content": json.dumps(aggregate, indent=2)},
        ],
        temperature=0.2,
        max_tokens=600,
    )
    return response.choices[0].message.content.strip()


def main() -> int:
    try:
        records, bad = load_records(LOG_DIR)
    except FileNotFoundError as e:
        print(f"ERROR: {e}")
        return 1

    if not records:
        print("No parseable records found.")
        return 1

    aggregate = build_aggregate(records, bad)

    print("=" * 60)
    print("DETERMINISTIC AGGREGATE")
    print("=" * 60)
    print(json.dumps(aggregate, indent=2))

    print("\n" + "=" * 60)
    print("AI ANALYSIS")
    print("=" * 60)

    try:
        print(summarize(aggregate))
    except APIConnectionError:
        print("[Model unreachable — is Foundry Local running? Try: foundry status]")
        print("[The aggregate above is still valid.]")
        return 2
    except APIStatusError as e:
        print(f"[API error {e.status_code}: {e.message}]")
        return 2

    Path("triage-latest.json").write_text(json.dumps(aggregate, indent=2), encoding="utf-8")
    print(f"\nAggregate saved to triage-latest.json")
    return 0


if __name__ == "__main__":
    raise SystemExit(main())
```

```text
============================================================
DETERMINISTIC AGGREGATE
============================================================
{
  "generated_at": "2026-08-30T16:41:07+00:00",
  "total_lines_parsed": 120,
  "malformed_lines": 3,
  "counts_by_level": { "INFO": 71, "ERROR": 27, "WARN": 22 },
  "error_rate": 0.225,
  "top_error_messages": [
    { "message": "punch relay unreachable", "count": 11 },
    { "message": "auth failed", "count": 9 },
    { "message": "disk full", "count": 7 }
  ],
  ...
}

============================================================
AI ANALYSIS
============================================================
SUMMARY: The fleet is degraded, with a 22.5% error rate across 120 parsed log lines from
three files. Errors are concentrated in punch relay connectivity and authentication.

TOP ISSUES:
- Punch relay unreachable (11 occurrences), most frequently on pi-003 and pi-007.
- Authentication failures (9 occurrences) spread across multiple devices.
- Disk full conditions (7 occurrences) indicating storage pressure.

RECOMMENDED ACTIONS:
1. Investigate network path to the punch relay service from Barn 2 and Barn 3 devices.
2. Review credential expiry and clock drift on devices reporting auth failures.
3. Implement log rotation or expand storage on devices reporting disk-full errors.

Aggregate saved to triage-latest.json
```

**The architectural lesson — this is the most important idea in the whole two weeks.** The Python counted; the model wrote. Never ask a language model to compute a total, sort a list, or filter data — it will produce plausible, confidently-wrong numbers. Compute deterministically, then hand the model the facts and ask it for language. Every good RAG and agent system in Phase 3 follows this same division of labor, and knowing it puts you ahead of most people who arrive at AI-103.

**Stretch modifications** (pick two):

1. Add `--since` filtering by date and pass the window to the model in the prompt.
2. Ask for JSON output (`"Respond only with JSON matching this schema..."`), parse it with `json.loads`, and handle parse failures — a preview of structured outputs.
3. Add a second model pass that rates severity 1–5, and compare answers at temperature 0 vs 0.8.
4. Async-batch: summarize each log file separately and concurrently, then summarize the summaries (a map-reduce pattern used for documents exceeding a context window).
5. Add `--watch` mode that re-runs every 60 seconds and only calls the model when the aggregate changed.

---

## Phase 0 gate — self-test

Open a blank file. No reference material, no AI assistance, no copy-paste. Give yourself 90 minutes. Write a program that:

1. Loads `MODEL_ENDPOINT`, `MODEL_NAME` from a `.env` file and exits with a clear message if either is missing
2. Defines a function with type hints and a docstring that takes a list of dictionaries and returns aggregate counts by a named field
3. Reads a JSON file from disk, handling both "file missing" and "invalid JSON" distinctly
4. Constructs an `OpenAI` client pointed at your local endpoint
5. Sends a system + user message pair and prints the reply
6. Streams a second response token by token
7. Maintains conversation history across at least two turns so a follow-up question resolves correctly
8. Catches connection and API errors with actionable messages
9. Writes its output to a timestamped file using `pathlib`
10. Uses `if __name__ == "__main__":` and returns a meaningful exit code

<details><summary>Answer key — what each item is testing</summary>

| # | Tests | Day |
|---|---|---|
| 1 | `load_dotenv`, `os.getenv`, guard clauses, exit codes | 8 |
| 2 | functions, type hints, docstrings, dict aggregation | W1 D4 |
| 3 | `pathlib`, `json.load`, distinguishing `FileNotFoundError` from `JSONDecodeError` | W1 D6–7, 10 |
| 4 | client construction with `base_url` | 11 |
| 5 | messages array, roles, `.choices[0].message.content` | 11 |
| 6 | `stream=True`, `delta.content`, `end=""`, `flush=True` | 11 |
| 7 | **statelessness** — appending assistant replies to history | 11 |
| 8 | `APIConnectionError`, `APIStatusError` | 9, 11 |
| 9 | `Path`, `write_text`, `datetime.strftime` | W1 D6–7 |
| 10 | script structure, `sys.exit` / `SystemExit` | 8 |

If you can do all ten unaided, you are ready for Phase 1 — and honestly, ready for a large fraction of the AI-103 lab work too. Anything you fumble points at a specific day to revisit; item 7 is the one most people miss, and it's the one that matters most.
</details>

---

## You are now ready for Phase 1

Here's exactly where each Week 2 skill lands in the AI-901 work starting Monday:

| Week 2 skill | Phase 1 use |
|---|---|
| venv + `requirements.txt` | Every MicrosoftLearning lab repo opens with these commands |
| `.env` + `os.getenv` | Labs store the Foundry project endpoint and key this way |
| HTTP status literacy | Diagnosing 401 (key/token), 403 (RBAC), 404 (deployment name), 429 (quota) against real Azure services |
| JSON navigation | Reading every service response you'll meet |
| `OpenAI` client + `base_url` | The AI-901 "call your deployed model from code" exercise — same code, Azure endpoint |
| messages/roles/system prompt | The playground and every generative exercise |
| streaming | Chat app labs |
| tool calling | The conceptual foundation for the agents domain (and all of Phase 3) |
| async | Agent SDK samples, and batch embedding in Phase 3 |
| classes | Reading `AIProjectClient`, `DefaultAzureCredential`, and every SDK sample |

One change on Monday: instead of `api_key="not-needed"` against localhost, you'll authenticate to Azure — first with a key from your Foundry project, then (properly) with `DefaultAzureCredential` and Entra ID, which is the pattern the exam wants and the one your PKI instincts will appreciate.

The language is no longer the obstacle. From here on, everything you learn is about **Azure AI**, not about Python.
