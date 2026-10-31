# Forensics v2 Lab-Companion Reconciliation Report

Reconciled the 22 student HTML companions (Labs 01–21 + Cyber Range) in the
`forensics` repo against the official NDG **Forensics v2** lab PDFs. Each PDF
was extracted and read in full, start to finish — not from snippets — and each
companion was checked command-by-command against it.

## What was verified for every lab

- **Every numbered step and command** — exact flags, syntax, and punctuation. All
  en-dashes (`–`) and curly quotes (`" " ' '`) were converted to straight
  hyphens/quotes so commands copy-paste cleanly. **Result: 0 en-dash/curly-quote
  characters remain in any command block.**
- **Machine attribution** — every command carries the correct terminal prompt, and
  the full-steps section now opens each run of steps with a **machine band**
  (icon + "On <machine>" + per-VM colour/left-accent). **Result: 0 band-vs-prompt
  conflicts across all 21 labs.**
- **VM / credentials table** — each lab's Environment table now lists **only the VMs
  that lab actually uses** (previously every lab listed all four).
- **Screenshot cues** — each required capture appears as a 📸 marker at the correct
  step, in document order, matching the three evidence deliverables.
- **Evidence checklist** — preserved (3 items per lab, already accurate).
- **Pod topology** — the credential table + bands make the per-lab layout clear.
- **HTML integrity** — balanced tags, **0 inline event handlers**, **0 broken
  internal links**, lab mode still works, no horizontal overflow at 390 px.
- **Design preserved** — palette, fonts, lab mode, screenshot-marker styling, page
  structure all unchanged; content-only edits.

## Verification results — commands

"PDF cmds" counts every terminal command in the PDF. "Real cmds" excludes lines the
PDF formats as commands but that are *not* terminal input (a URL typed into a
browser bar, credentials shown in a shaded box, free-text typed into a PDF form).
"Matched" = present in the companion.

| Lab | Title | VM(s) | PDF cmds | Real terminal cmds | Matched | Status |
|-----|-------|-------|:-------:|:-----:|:-----:|--------|
| 00 | Launch Cyber Range | all four | 0 | 0 | — | GUI-only (band CSS added) |
| 01 | Creating a Forensic Image | WinOS | 0 | 0 | — | GUI-only ✓ |
| 02 | Live Acquisition | WinOS | 0 | 0 | — | GUI-only ✓ |
| 03 | Live Forensics (DART) | WinOS | 0 | 0 | — | GUI-only ✓ |
| 04 | Registry Forensics | WinOS | 0 | 0 | — | GUI-only ✓ |
| 05 | File Systems | WinOS | 0 | 0 | — | GUI-only ✓ |
| 06 | Keyword Search & Analysis | CSI-Linux | 0 | 0 | — | GUI-only ✓ |
| 07 | Data Carving | WinOS | 0 | 0 | — | GUI-only ✓ |
| 08 | Metadata & Link File Analysis | WinOS | 0 | 0 | — | GUI-only ✓ |
| 09 | Recycle Bin Forensics | CSI-Linux | 11 | 11 | 11 | **all matched** ✓ |
| 10 | Steganography & ADS | WinOS | 6 | 6 | 6 | **all matched** ✓ |
| 11 | Picture File Analysis | DEFT → WinOS | 5 | 5 | 5 | **all matched** ✓ |
| 12 | Email Analysis | CAINE | 6 | 3 | 3 | **all matched** ✓ (3 non-terminal dropped) |
| 13 | Internet Browser Forensics | CAINE | 0 | 0 | — | GUI-only ✓ |
| 14 | Timeline Analysis | WinOS | 0 | 0 | — | GUI-only ✓ |
| 15 | IoT Forensics | WinOS | 0 | 0 | — | GUI-only ✓ |
| 16 | Mobile Forensic Analysis | CSI-Linux | 0 | 0 | — | GUI-only ✓ |
| 17 | Log Capturing & Interpretation | WinOS | 0 | 0 | — | GUI-only ✓ |
| 18 | Pagefile Analysis | CSI-Linux | 0 | 0 | — | GUI-only ✓ |
| 19 | Password Cracking | CSI-Linux | 7 | 7 | 7 | **all matched** ✓ |
| 20 | File Hashing & Hash Analysis | WinOS | 0 | 0 | — | GUI-only ✓ |
| 21 | Chain of Custody | WinOS | 2 | 0 | — | 2 "commands" are PDF-form text, not terminal ✓ |

**Totals:** 37 terminal commands across the command-bearing labs; **37 matched, 0 real
gaps.** The 15 GUI-only labs are driven entirely through FTK Imager / Autopsy / HxD /
DB Browser / forms — there is no terminal command to type, so "no command block" is
correct, not a gap.

Note on "non-terminal" lines:
- **Lab 12** — `caine Train1ng$` (login credentials in a shaded box), `FOR_LAB_012`
  (folder name typed in a Save dialog), and `http://127.0.0.1:8080` (URL typed in the
  browser) are formatted like commands in the PDF but are not terminal input. They are
  shown in the companion in their correct UI context, not as fake terminal commands.
  The 3 real CAINE terminal commands (`cd …/mha/`, `ls`, `python3 server.py -d`) are
  all present.
- **Lab 21** — the two monospace blocks in the PDF are the evidence-item description
  and the service-request text the student types into PDF form fields, not terminal
  commands. They appear in the walkthrough as form content.

## Per-lab machine layout (now reflected in the credential tables + bands)

- **WinOS only:** 01, 02, 03*, 04, 05, 07, 08*, 10, 14, 15, 17, 20, 21
- **CSI-Linux only:** 06, 09, 16, 18, 19
- **CAINE only:** 12, 13
- **DEFT → WinOS (the only multi-VM lab):** 11
- **All four (reference pod):** 00 Cyber Range

\* Labs 03 and 08 run the **DART** toolkit (a DEFT-project tool) and Lnk Examiner as
portable tools **on WinOS** — the DEFT VM is never booted. A note on each page makes
this explicit so students don't try to switch VMs.
