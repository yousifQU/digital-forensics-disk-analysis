# Project 5: Data Hiding Detection

**Type:** Individual lab · **Tools:** Windows Explorer, Microsoft Office, archive tools, S-Tools

> Part of a university course. Not solely my own work; see the disclaimer in the main README. The hidden "keys" themselves are left out on purpose, so this write-up describes techniques, not answers.

## Situation
I was given an evidence archive with 10 folders that contained **13 hidden "keys"**, each a word or short phrase. Each key had been concealed with a different data-hiding technique. The goal was to find at least 10 of them, record where and how each was hidden, and classify each technique against a standard data-hiding reference chart.

## What I Did
I searched each folder by hand and with tools, and logged for every key: its path, how it was hidden, the technique category, and how I found it.

| # | How it was hidden | Technique | How I found it |
|---|-------------------|-----------|----------------|
| 1 | Plain text file at the top level | None (control) | Opened the archive |
| 2 | Text file inside a folder with a blank name | Unlabeled folder | Inspected the folder with no visible name |
| 3 | Inside a file with a spoofed, misspelled executable extension | Extension manipulation | Opened the file contents instead of trusting the extension |
| 4 | Inside the internal XML (`document.xml`) of a Word file | Hidden in Office Open XML | Opened the `.docx` as a ZIP and read the XML parts |
| 5 | Text in a Word file formatted in white on a white background | Visual concealment | Selected all text and changed the font color |
| 6 | Text file placed in a folder named to look like a Windows system directory | Misleading location | Searched the decoy system folder |
| 7 | Text placed among the columns of a spreadsheet | Obscurity | Checked every column and sheet |
| 8 | File deep inside dozens of nested folders, under a parent folder named with a Windows CLSID so Explorer shows it as the Recycle Bin | CLSID junction-folder disguise + deep nesting | Walked the full path; recognized the CLSID trick |
| 9 | Text file buried in a chain of folders named "Recycle Bin" | Misleading location | Followed every nested folder |
| 10 | Embedded in a bitmap image | Steganography | Extracted with S-Tools |
| 11 | Inside a password-protected Word document | Password protection | Found the password elsewhere in the evidence set and opened the document |

## Results
- **I found 11 of the 13 keys**, beating the 10-key requirement.
- I catalogued about ten different concealment methods. They range from trivial (a blank folder name) to tool-dependent (image steganography).
- One hidden key was itself a password, a reminder that evidence should be read as a whole, not one item at a time.

## Takeaways
- Most hiding techniques beat casual browsing, not forensic tools. Checking file signatures, unpacking Office files and walking the full directory tree defeats most of them.
- Windows shell tricks such as CLSID-named folders can make data look like system objects. An investigator should check the real path, not what Explorer displays.
- Steganography needs specialized tools, so an investigator should check images when other evidence suggests hidden data.
