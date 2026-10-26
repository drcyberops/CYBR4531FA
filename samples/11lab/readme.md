# Lab 11 — YARA Rules Student Lab

This lab supports the **YARA Fundamentals** and **Developing and Testing Reliable
YARA Rules** lessons in CSCI 4531 Malware Analysis. Use it to practice writing rules,
explaining matches, and testing detection logic against positive cases, variants,
and benign look-alikes.

## Download and password

Download [`yara-student-lab-r1.zip`](yara-student-lab-r1.zip) using **Download raw**
on the ZIP's GitHub page.

**ZIP extraction password: `infected`**

The password follows the course's lab-archive convention. The contents are harmless
teaching material: the generator creates inert synthetic byte files, not real malware
or working executables. No network access is needed to run the exercises after download.

## What is inside?

The archive extracts into a `yara_lab/` directory:

| File | Purpose |
| --- | --- |
| `README.txt` | Setup instructions, fixture labels, and the Lesson 2 target specification |
| `make_fixtures.py` | Creates 15 deterministic, harmless practice files in `fixtures/` |
| `rules/lesson1.yar` | A two-marker starter rule for learning rule structure and scan output |
| `rules/baseline.yar` | An intentionally broad baseline to evaluate and improve |
| `rules/optional_pe.yar` | An optional parsed-PE check for comparing header bytes with format recognition |

The practice files are generated when you run the script; they are not prepackaged
malware samples. The archive contains student starter material, not instructor solution
rules or assessment answer keys.

## Requirements

- The course analysis VM or another instructor-approved environment.
- **Python 3**.
- Classic **YARA** and **yarac**, tested with **YARA 4.5.0 on Linux**.
- A ZIP extractor supporting password-protected ZIP files.

YARA-X and other runtimes were not used to validate this package.

## Quick start

1. Extract the ZIP using password **`infected`**.
2. Open a terminal in the extracted `yara_lab` folder.
3. Create the fixtures and check your runtime:

   ```bash
   python3 make_fixtures.py
   yara --version
   yarac --version
   ```

4. Compile the Lesson 1 rule and inspect two scan outcomes:

   ```bash
   yarac rules/lesson1.yar lesson1.yarc
   yara -s rules/lesson1.yar fixtures/l1_both.txt
   yara -s rules/lesson1.yar fixtures/l1_single.txt
   ```

   The first scan reports the two-marker teaching rule. The second successfully
   scans without matching it. A syntax or file-access error is a separate outcome.

On Linux, `unzip yara-student-lab-r1.zip` prompts for the extraction password.
Enter `infected` at that prompt.

## How to use it with the lessons

### Lesson 1 — YARA Fundamentals

Use `fixtures/l1_*` to practice rule anatomy, text encodings, case modifiers,
Boolean conditions, and explaining matched strings and offsets. Follow the D2L
lesson for the prediction-and-scan exercise.

### Lesson 2 — Rule Development and Testing

Read the synthetic container specification in `README.txt`. Use `dev_*` fixtures
to evaluate the baseline and develop your candidate rule. Freeze your candidate
before scanning `holdout_*`. Record per-file outcomes and calculate true/false
positive/negative counts, precision, and recall.

The inspectable classroom holdout illustrates a workflow; it is not a blind benchmark
or evidence of real-world malware coverage. A match does not prove maliciousness,
and a nonmatch does not establish that a file is safe.

## Work to retain

Keep your rule source, tool version, exact commands, prediction/result table, matched
evidence, metric calculations, and a short explanation of scope and limitations.
Your D2L lessons and instructor determine any assessed submission, deadline, or grade.

**Revision:** r1. The student ZIP was checked for password enforcement and exact
agreement with the five allowlisted student source files.
