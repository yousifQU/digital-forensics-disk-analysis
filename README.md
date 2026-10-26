# Digital Forensics Case Studies

Hands-on digital forensics work completed during a university Digital Forensics course (Spring 2025). It covers evidence acquisition, integrity verification, crime-scene handling, file-system analysis and data-hiding detection, done on training images and mock cases in a lab environment.

> **Disclaimer:** I am not the sole owner of this work. These projects come from university lab assignments. Some were done in pairs or groups, and all of them were built on scenarios, evidence images and instructions designed by the course instructors. The write-ups here are my own summaries of that work. All names, institutions, course identifiers, case numbers, passwords and other identifying details have been removed or replaced with generic descriptions. Every case is a fictional training scenario.

---

## Executive Summary

Across one semester I worked through the core digital forensics workflow, from seizing a device at a mock crime scene to presenting findings that would hold up to review:

- **Acquire.** I created logical and physical forensic images in E01 and RAW formats, using FTK Imager, Magnet AXIOM and `dd`, with and without hardware write blockers.
- **Verify.** I used MD5 and SHA-1 hashing to prove each image matched its source. In one exercise this exposed a forensic image whose hash did not match the original examiner's report.
- **Handle.** I took part in a mock seizure: assigning team roles, keeping a crime-scene entry log and a chain-of-custody form, and bagging and tagging the evidence.
- **Analyze.** I recovered evidence from allocated space, encrypted archives, renamed files and hidden locations, using Magnet AXIOM, Autopsy and FTK Imager.
- **Detect concealment.** I identified more than ten data-hiding techniques, including steganography, extension spoofing, Windows folder tricks, Office-file internals and password protection.
- **Report.** I wrote findings for both technical and non-technical readers, and acted as the team's report writer in the group seizure case.

## Projects

Each project has its own branch, which opens on a short case report: objective, scenario, methodology, findings, analysis and conclusion. Click a branch link below to read it.

| # | Project | Focus | Branch |
|---|---------|-------|--------|
| 1 | Forensic Acquisition & Hash Verification | Logical vs. physical imaging, E01 vs. RAW, cross-tool hash validation | [`project/01-forensic-acquisition`](https://github.com/yousifQU/digital-forensics-disk-analysis/tree/project/01-forensic-acquisition) |
| 2 | Evidence Integrity Review (Expert Witness) | Reviewing another examiner's report, `dd` imaging, `certutil` hashing, Autopsy | [`project/02-evidence-integrity-review`](https://github.com/yousifQU/digital-forensics-disk-analysis/tree/project/02-evidence-integrity-review) |
| 3 | Crime Scene Seizure: Bag & Tag | Team seizure, chain of custody, write-blocked physical imaging, case analysis | [`project/03-crime-scene-seizure`](https://github.com/yousifQU/digital-forensics-disk-analysis/tree/project/03-crime-scene-seizure) |
| 4 | Contraband Image Investigation | Large-scale artifact identification, hidden image recovery, file signature analysis | [`project/04-contraband-image-investigation`](https://github.com/yousifQU/digital-forensics-disk-analysis/tree/project/04-contraband-image-investigation) |
| 5 | Data Hiding Detection | Finding keys hidden with 10+ concealment techniques | [`project/05-data-hiding-analysis`](https://github.com/yousifQU/digital-forensics-disk-analysis/tree/project/05-data-hiding-analysis) |

See [TOOLS_AND_SKILLS.md](TOOLS_AND_SKILLS.md) for the full tool list and skill breakdown.

## Timeline

All work was completed in a single spring semester, in this order:

| When | Work | Status |
|------|------|--------|
| Late January | Project 1: Forensic acquisition with FTK Imager & Magnet AXIOM | Written up |
| Late January | Project 2: Evidence integrity review (paired lab) | Written up |
| Early February | Project 3: Crime scene seizure (team of four) | Written up |
| Mid-semester | Project 4: Contraband image investigation | Written up |
| Early April | Project 5: Data hiding detection | Written up |
| April | Linux image analysis with Kali Linux and legacy Autopsy/Sleuth Kit | Exposure only (not written up) |
| May | Mobile forensics: Android with Cellebrite UFED Reader, iOS backup with Magnet AXIOM | Exposure only (not written up) |

The last two exercises are listed for completeness. They are not written up as projects because I don't have complete records of the results.

## Core Tools at a Glance

`FTK Imager` · `Magnet AXIOM` · `Autopsy / The Sleuth Kit` · `dd` · `certutil` · `Hardware write blocker` · `S-Tools` · `TinEye` · `Kali Linux` · `Oracle VirtualBox` · `Cellebrite UFED Reader` · `Windows Disk Management` · `WMIC`

## Repository Layout

```
main
├── README.md               ← portfolio overview (you are here)
└── TOOLS_AND_SKILLS.md     ← tools, skills and concepts

project/0X-* branches
└── README.md               ← the case report for that project
```
