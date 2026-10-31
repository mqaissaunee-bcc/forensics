# Lab-by-lab fix summary

Changes are **content-only**. The design system (palette, Merriweather/Source Sans/
JetBrains Mono fonts, light/dark, lab mode, screenshot markers, progress tracking,
evidence checklists, cheat sheets) is untouched except for one additive CSS block
(machine-band + source-note styling) added to every page.

## Changes applied to all 21 lab pages

1. **Machine bands added** to the "Full lab steps" section. Each run of steps on a VM
   is introduced by a labelled band — 🪟 **On WinOS**, 🐧 **On CAINE**,
   🔎 **On CSI-Linux**, 🧰 **On DEFT** — with a per-VM colour and left-accent that
   persists down the step cards until the next band. The band also shows that VM's
   login + IP inline, so the student always knows where they are.
2. **Credential (Lab Settings) table scoped to the VMs the lab actually uses.**
   Previously every page listed all four pod VMs; now e.g. Lab 19 lists only
   CSI-Linux, Lab 12 only CAINE, Lab 11 only DEFT + WinOS.
3. **Screenshot 📸 markers re-anchored** to the exact step where each evidence
   artifact is produced, in document order (a few were previously out of sequence —
   e.g. Lab 10's "carved PNG" marker had landed in the ADS task; Lab 11's EXIF/GPS
   markers were reversed).
4. **Command punctuation normalised** — en-dashes and curly quotes converted to
   straight hyphens/quotes in every command block.
5. **Full-steps text re-derived from a full-document parse** of each PDF, so no step is
   dropped or merged across a page break.

## Lab-specific fixes and flags

### Lab 03 — Live Forensics
- Added a note: the whole lab runs on **WinOS**; DART is launched as a portable tool,
  the DEFT VM is never booted. Credential table now lists **WinOS only**.

### Lab 08 — Metadata & Link File Analysis
- Same DART-on-WinOS note; credential table **WinOS only**.

### Lab 10 — Steganography & ADS
- ADS commands now carry the correct working-directory prompts
  (`C:\Users\Administrator>` → `E:\>` → `E:\FOR_LAB_010\ADS\Exercise1>`) instead of a
  generic `C:\>`, matching the three `cd`/`dir`/`type`/`notepad`/`dir /r` steps.
- Capitalised command verbs (`Type`, `Notepad`, `Dir /r`) lowercased for clean
  copy-paste (`type`, `notepad`, `dir /r`) — Windows is case-insensitive, but this
  matches the walkthrough and avoids confusion.
- Credential table **WinOS only**.

### Lab 11 — Picture File Analysis (the only multi-VM lab)
- **Two bands:** 🧰 On DEFT (ExifTool steps) → 🪟 On WinOS (Thumbs.db carving in HxD),
  with the switch at the exact PDF step where the lab says "switching to the Windows
  VM." Credential table lists **DEFT + WinOS** only.
- Walkthrough already carried correct "On DEFT"/"On WinOS" inline labels — preserved.

### Lab 12 — Email Analysis
- The three monospace lines that are **not** terminal commands
  (`caine Train1ng$` login, `FOR_LAB_012` folder name, `http://127.0.0.1:8080` URL)
  are no longer rendered as terminal commands. The 3 real CAINE commands
  (`cd …/email-header-analyzer-master/mha/`, `ls`, `python3 server.py -d`) carry the
  `caine@caine:~$` prompt.
- Added a currency note: Email Header Analyzer (the `mha` Flask app) is unmaintained
  upstream and targets Python 3; kept as the lab ships. Credential table **CAINE only**.

### Lab 19 — Password Cracking  *(flagged divergence)*
- Fixed two source typos that break copy-paste: the stray space in
  `FOR_LAB_019/ pdf_file` and `FOR_LAB_019/ zip_file` → `/pdf_file`, `/zip_file`; and
  capitalised `Unzip` → `unzip`.
- **Safety decision (flagged on the page):** this lab is analysis-side — it detects and
  opens password-protected *evidence* using the exact tools and wordlist NDG ships
  (`pdfcrack`, `fcrackzip`, VeraCrypt, `/usr/share/john/password.lst`). It is not an
  AV-evasion or exploit recipe, so the commands and the passwords the lab recovers are
  kept intact. A source-note states this explicitly and the Overview keeps its
  "authorized evidence only, isolated lab" framing. Credential table **CSI-Linux only**.

### Lab 21 — Chain of Custody
- The two monospace PDF blocks are the evidence-item description and service-request
  text typed into **PDF form fields**, not terminal commands — they are shown as form
  content, not fake terminal input.
- Added a note on two inconsistencies in the original NDG forms: the chain-of-custody
  step reuses the filename `NDG Evidence Intake form.pdf`, and the signature block
  names the receiver *Det. Jane Brown* while the submitter is *Det. John Brown*. Values
  follow the PDF field-by-field. Credential table **WinOS only**.

## No other safety divergences were required

The rest of the Forensics v2 set is analysis/examiner-side (imaging, carving, registry,
timeline, hashing, documentation). Nothing hands over a working weapon, so no other
content was held back. Lab 19 is the only page with a flagged safety decision.
