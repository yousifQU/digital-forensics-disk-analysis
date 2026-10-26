# Case Report 01 — Forensic Acquisition & Hash Verification

[← Back to portfolio overview](https://github.com/yousifQU/digital-forensics-disk-analysis)

> University coursework, anonymized. Not solely my own work; the scenario and lab design belong to the course instructors.

| Field | Detail |
|-------|--------|
| **Case type** | Evidence acquisition exercise |
| **Period** | Spring 2025, late January |
| **Format** | Individual lab |
| **Evidence** | One USB flash drive (~8 GB device, ~50 MB FAT16 volume) |
| **Tools** | FTK Imager, Magnet AXIOM (Process & Examine), WMIC, Windows Disk Management |
| **Hash algorithms** | MD5, SHA-1 |

---

## 1. Objective
Acquire a storage device in several defensible ways, verify every image with hashes, and explain why hash values match or differ between imaging methods.

## 2. Scenario
A USB drive is treated as a piece of evidence. Before analysis, the examiner has to document the device, create forensic images with more than one tool, and prove that each image is an exact copy of what it claims to represent.

## 3. Methodology

| Step | Action | Purpose |
|------|--------|---------|
| 1 | Formatted the drive and loaded four known test files (image, spreadsheet, document, presentation) | Create a controlled, known evidence set |
| 2 | Recorded the drive's model, serial number, size and partitions (`wmic diskdrive get ...`) and checked the letter and file system in Disk Management | Identify the device for the case record |
| 3 | Created a case in Magnet AXIOM, processed the drive, and reviewed the parsed artifacts in AXIOM Examine | Confirm the tool finds the known files |
| 4 | Acquired the drive with Magnet AXIOM (E01, MD5 + SHA-1, image verification on) | First acquisition |
| 5 | Acquired with FTK Imager: logical E01, logical RAW, then a full physical image (no fragmentation, no compression) | Compare formats and scopes |
| 6 | Compared the computed and verification hashes of every image | Prove integrity and validate across tools |

## 4. Findings

| Image | Tool | Scope | Sectors (512 B) | Size | Hash verified |
|-------|------|-------|-----------------|------|---------------|
| A | FTK Imager | Logical, E01 | 102,400 | ~50 MB | ✅ |
| B | FTK Imager | Logical, RAW | 102,400 | ~50 MB | ✅ (same as A) |
| C | FTK Imager | Physical, E01 | 15,728,640 | ~8 GB | ✅ |
| D | Magnet AXIOM | Physical, E01 | n/a | n/a | ✅ (same as C) |

- All four test files were parsed in AXIOM. The tool also surfaced system and browser artifacts, such as a partial download file, that were not deliberately placed on the drive.
- No bad blocks were reported in any acquisition.

## 5. Analysis
- **A = B.** The image format doesn't change the hash. The hash is calculated over the acquired data, not over the E01 or RAW container.
- **A ≠ C.** The logical image holds only the FAT16 volume. The physical image holds the whole device, including partition structures and unallocated space, so both the size and the hash differ.
- **C = D.** Two independent tools produced the same hash for the same device. This cross-validates the acquisition and would hold up if either tool were questioned.

## 6. Conclusion
Every image was verified against its source. Physical acquisition is the preferred method when deleted or unallocated data may matter, and validating with a second tool adds confidence at little cost.

## 7. Skills Demonstrated
Device documentation · logical vs. physical imaging · E01/RAW formats · MD5/SHA-1 verification · cross-tool validation
