# Case Report 05 — Data Hiding Detection

[← Back to portfolio overview](https://github.com/yousifQU/digital-forensics-disk-analysis)

> University coursework, anonymized. Not solely my own work; the evidence set was built by the course instructors. The hidden "keys" are left out on purpose, so this report covers techniques, not answers.

| Field | Detail |
|-------|--------|
| **Case type** | Detection of concealed data in an evidence set |
| **Period** | Spring 2025, early April |
| **Format** | Individual lab |
| **Evidence** | Compressed archive with 10 folders and 13 hidden "keys" |
| **Tools** | Windows Explorer (hidden items view), Microsoft Word & Excel, archive tools (7-Zip/WinRAR), S-Tools |
| **Reference** | A standard data-hiding technique chart (provided in the evidence set) |

---

## 1. Objective
Find at least 10 of the 13 hidden keys. For each one, document its location, how it was hidden, the technique category and how it was found.

## 2. Scenario
An investigator gets a collection of files that a suspect is believed to have used to hide information. Each folder uses a different concealment method, ranging from simple obscurity to steganography. The investigator has to find the hidden content and explain each method so the findings can be reproduced.

## 3. Methodology
1. Extracted the archive into a working directory, keeping the original archive untouched.
2. Turned on the display of hidden items and file extensions in Windows Explorer.
3. Searched each folder in turn, checking:
   - names, extensions and file headers
   - the internals of Office documents, which are ZIP archives of XML files
   - text formatting and spreadsheet contents
   - nested and disguised directories
   - images, with steganography tools
4. Logged each key against the technique chart.

## 4. Findings

| # | Concealment method | Technique category | Detection method |
|---|--------------------|--------------------|------------------|
| 1 | None: plain text at top level | Control | Opened the archive |
| 2 | Folder with a blank name | Unlabeled folder | Inspected the nameless folder |
| 3 | Misspelled, spoofed executable extension | Extension manipulation | Inspected contents, ignored extension |
| 4 | Text inside a Word file's internal `document.xml` | Office Open XML hiding | Unzipped the `.docx`, read the XML |
| 5 | White text on a white background | Visual concealment | Selected all text and recolored it |
| 6 | File in a folder disguised as a Windows system directory | Misleading location | Searched the decoy folder |
| 7 | Text among spreadsheet columns | Obscurity | Reviewed every column and sheet |
| 8 | File under dozens of nested folders inside a CLSID-named folder that Explorer displays as the Recycle Bin | CLSID disguise + deep nesting | Walked the real path |
| 9 | File inside a chain of fake "Recycle Bin" folders | Misleading location | Followed every nested folder |
| 10 | Data embedded in a bitmap | Steganography | Extracted with S-Tools |
| 11 | Password-protected Word document | Password protection | Located the password in the evidence set |

**Score: 11 of 13 keys found** (10 required).

## 5. Analysis
- **Seven of the eleven methods** (2, 3, 5, 6, 7, 8, 9) only defeat casual browsing. They fall to a systematic search: show hidden items, ignore extensions and walk every directory.
- **Methods 4 and 10** need knowledge of the file format or a specialized tool: Office files are ZIP archives, and steganography requires extraction software.
- **Method 8** uses a Windows shell feature: naming a folder with a CLSID makes Explorer show it as a system object. Examiners should check the raw path, not the Explorer display.
- **Method 11** shows why evidence must be read as a whole: one hidden item held what was needed to open another.
- **Two keys were not found.** A follow-up pass with a hex editor and a file-carving tool would be the next step.

## 6. Conclusion
A methodical, tool-assisted search defeated almost every concealment technique in the set. The investigation produced a reusable checklist: hidden items, extensions vs. headers, Office internals, formatting, directory depth and disguises, steganography, and password-protected content.

## 7. Skills Demonstrated
Anti-forensics awareness · file signature vs. extension analysis · Office Open XML inspection · steganography detection · systematic evidence search · technique classification
