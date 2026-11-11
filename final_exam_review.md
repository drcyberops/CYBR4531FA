# CSCI 4531 Final Practical — Student Review

## What to expect

This is a **case-based malware-analysis practical**. You will examine supplied
artifacts, use the assigned tools, and report findings supported by evidence.
Each case provides a briefing, evidence list, analyst objective, required tools,
and reporting fields.

- **120 minutes total** with one overall timer.
- **Seven independent cases** containing **44 separate written-response questions**.
- **100 points total**; most responses are short observations or explanations.
- **Forward-only navigation:** finish the current case before moving on.
- Instructor-provided **pocket references are allowed**.
- Use the assigned VM and tools. **No AI, MCP, outside assistance, online analyzers,
  unapproved scripts, or substitute analysis tools.**

> **Before selecting Next:** review every answer and attachment in the current case.
> Once you advance, you cannot return to that case or revise its answers. A case
> does not depend on answers or files from an earlier case. Do not revisit earlier
> samples after advancing.

## Cases and suggested timing

| Case | Main area | Suggested time | Points |
|---|---|---:|---:|
| 1 — Library Triage | PE inspection, packing, hashes, address mapping, DLL execution | 18 min | 15 |
| 2 — Host Activity Reconstruction | Procmon evidence and Regedit verification | 12 min | 10 |
| 3 — Remote Loading Evidence Review | Interpret a supplied API worksheet | 12 min | 15 |
| 4 — Unknown Artifact and Network Findings | Identify an artifact and analyze its application data | 15 min | 15 |
| 5 — Packed Code and Debugger Behavior | Unpacking, debugger checks, and controlled execution | 23 min | 20 |
| 6 — Code-Supported Behavior Assessment | Strings, code references, and branch reasoning | 20 min | 15 |
| 7 — Scoped Detection and Record Recovery | Complete and test a YARA rule against a directory | 15 min | 10 |
| Operational buffer | Tool, evidence, and submission overhead | 5 min | — |
| **Total** | | **120 min** | **100** |

The case estimates are guidance, **not separate timers**. Use the buffer as needed;
it does not allow you to reopen earlier cases. Follow D2L for the official schedule,
availability, accommodations, and final announcements.

## What to review and practice

### Case 1 — Library Triage

**Tools:** CFF Explorer, Detect It Easy, UPX, PowerShell Get-FileHash, the course hex
editor, Process Hacker/System Informer, and Windows rundll32.

- Read PE file type, architecture, header fields, and section information.
- Recognize packing and preserve an original while analyzing a working copy.
- Record complete hashes with the correct filenames.
- Distinguish an RVA, preferred VA, runtime VA, and raw file offset.
- Understand compatible DLL hosts and support execution claims with observations.

### Case 2 — Host Activity Reconstruction

**Tools:** Procmon and Regedit.

- Use the **preinstalled Procmon filter presets**; filter creation is not assessed.
- Read process, operation, path, result, timestamp, and event-detail fields.
- Distinguish file-opening/creation activity from a data write.
- Distinguish a registry **key**, **value name**, **value type**, and **value data**.
- Compare timestamped registry-write evidence with the current state in Regedit.
- Identify parent/child processes and support event ordering with timestamps.

### Case 3 — Remote Loading Evidence Review

**Tools:** the course text viewer/editor and supplied worksheet.

- Follow how handles, addresses, sizes, data, and arguments connect across API calls.
- Explain an API sequence in a few technically accurate sentences.
- Consider how a failure or partial operation affects later conclusions.
- Distinguish a synthetic worksheet from proof of an actual runtime event.

### Case 4 — Unknown Artifact and Network Findings

**Tools:** TrID, the course hex editor, Wireshark, and the approved offline CyberChef.

- Identify a file using tool output and signature evidence before choosing how to handle it.
- Locate endpoints, protocols, request fields, and packet/stream references.
- Recognize common data transformations and document a reproducible decoding recipe.
- Separate recovered content from claims about malicious intent or compromise.

### Case 5 — Packed Code and Debugger Behavior

**Tools:** Detect It Easy, CFF Explorer, UPX, and x32dbg.

- Identify a packer and compare packed/unpacked representations.
- Explain the relationship between an unpacking entry point and original program behavior.
- Step through calls and conditional branches; record the values and addresses you observe.
- Distinguish a runtime change from a change saved to the file on disk.
- Be prepared for a controlled debugger demonstration with a requested MessageBox.

### Case 6 — Code-Supported Behavior Assessment

**Tools:** Ghidra and the course-installed **GNU Strings**.

- Select appropriate string-extraction options using your approved references.
- Locate functions, API calls, strings, and code references in Ghidra.
- Support behavior claims with the way data is actually used by the code.
- Explain branch conditions and predict a specific change that would take another path.
- Separate observations, predictions, and unsupported assumptions.

### Case 7 — Scoped Detection and Record Recovery

**Tools:** YARA, GNU Strings, the course hex editor/text editor, and offline CyberChef.

- Expect a **200-file collection**, a separate reference, and a starter rule framework.
- Modify a supplied rule framework using a separate reference artifact.
- Review YARA string definitions, hex patterns, conditions, and location constraints.
- Scan the requested directory **and its subfolders**, rather than one selected file.
- Check successful execution, match count, and matched paths; valid syntax alone is not enough.
- Inspect the matched record and support recovered-content findings with the source data.

## How to report your findings

Each question has its own answer area and blank labeled lines. Enter the requested
value or explanation after each label. For example, a registry response may request:

```text
Registry key:
Value name:
Value type:
Value data:
Write operation:
Observed result:
Observed timestamp:
Relevant observed event row/detail:
```

- Use **actual observed values**. PIDs and loaded addresses can differ between runs.
- Include only relevant output or event details and identify their source.
- A conclusion needs support; a tool name or an unsupported statement is not evidence.
- Enter your answers, commands, event details, and YARA rules **directly in the D2L
  answer fields**. Do not replace your responses with uploaded answer documents,
  raw log files, or separate rule files.
- Use screenshots only when they help support a finding. The image and attachment
  controls remain available, but you are not expected to upload separate answer files.
- One screenshot is required for the Case 5 debugger success demonstration, showing
  the MessageBox together with x32dbg identifying the supplied file. Other
  screenshots are optional unless the instructor announces otherwise.
- Retain required text such as a rule or command when the question requests it;
  an optional screenshot does not replace that text.

### Screenshots: be selective and explain them

**Screenshots may be included, but you do not need to screenshot everything.**
Choose a screenshot only when it helps support a specific finding. Keep the
relevant tool, filename, field, or output readable; avoid unnecessary full-desktop
captures and repeated images of the same result.

**Every screenshot must have a short explanation**—usually one or two sentences
stating what it shows and why it supports your answer. Identify the question or
finding it relates to. A screenshot by itself is not a complete answer.

#### Standard screenshot caption

Copy this template beneath each screenshot or into the answer beside its attachment.
Keep the finding and explanation brief and specific to the evidence shown.

```text
Question:
Finding:
Relevant address/value:
Why this evidence supports the finding:
```

Use the question identifier to connect the image to your answer. Report the actual
address or value visible in the image; if neither applies, write `Not applicable`.
Complete the final line with a short explanation, not just a repeated tool name.

**For debugging screenshots, show the details you discuss.** Include the relevant
instruction/call or branch address and enough surrounding code to establish
context. If your explanation relies on a register, return value, branch outcome,
memory location, or argument, make that value and its address/location visible
and readable. Identify the relevant address(es) in your written explanation or
clearly annotate the screenshot.

**Partial credit can only be awarded for work supported by visible evidence and
your explanation.** If a detail is cropped out, unreadable, or not identified and
discussed, the instructor cannot verify that part of your work. Do not expect
credit for a claim about code or a value that the submitted evidence does not show.

The Case 5 debugger screenshot is still required. For other questions, concise
written observations and relevant text output are sufficient unless the question
specifically requests an image. Focus on clear evidence, not the number of images.

## Before exam day

- Open the required tools on the assigned VM and report missing tools early.
- Have the approved pocket references available in the permitted form.
- Practice with instructor-approved class artifacts in the isolated VM.
- Know where you can save working copies and capture relevant screenshots.
- Be comfortable making a short, labeled report rather than a long narrative.

Download the final-exam package from the instructor's D2L area before starting,
as directed. **Each case's extraction password appears on its own D2L page.**
Do not assume the repository's general lab-sample password applies to final-exam
archives. Contact the instructor about technical problems before advancing.
