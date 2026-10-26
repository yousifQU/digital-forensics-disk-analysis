# Tools & Skills

## Tools

| Tool | What I used it for | Projects |
|------|--------------------|----------|
| **FTK Imager** | Logical and physical acquisitions in E01 and RAW; image verification; browsing evidence trees including unallocated space | 1, 2, 3 |
| **Magnet AXIOM (Process / Examine)** | Case creation, evidence parsing and carving, E01 acquisition with MD5/SHA-1 verification, artifact review across a full disk image; iOS backup analysis | 1, 4, mobile exercise |
| **Autopsy / The Sleuth Kit** | Opening an existing case, keyword search, file metadata (MAC times, hashes, MIME type, location); legacy web-based Autopsy on Kali Linux | 2, 4, Linux exercise |
| **dd (Windows port)** | Block-level copies of raw evidence images | 2 |
| **certutil** | MD5 hashing of image files from the Windows command line | 2 |
| **Hardware write blocker** | Read-only connection of a seized drive to the forensic workstation | 3 |
| **S-Tools** | Extracting data hidden in a bitmap image by steganography | 5 |
| **TinEye** | Reverse image search to identify a person in a recovered photo | 4 |
| **WMIC / Disk Management** | Recording drive serial number, model, size and partitions; confirming drive letter and file system | 1 |
| **Kali Linux on VirtualBox** | Building a forensic VM (updates, Guest Additions, shared folders) to analyze a segmented Linux image | Linux exercise |
| **Cellebrite UFED Reader** | Reviewing a processed Android extraction (device info, acquisition type, Wi-Fi history, apps) | Mobile exercise |

> **Note:** WMIC is deprecated in current Windows releases. The PowerShell equivalents are `Get-PhysicalDisk` and `Get-Disk`.

## Skills

### Evidence acquisition
- Logical vs. physical imaging, and when each one is the right choice. A physical image captures unallocated space and partition structures; a logical image captures only the volume's file system.
- E01 and RAW image creation with fragmentation and compression controlled.
- Acquiring through a hardware write blocker so the original evidence is never modified.
- Targeted (sparse) collection of a user's home folder alongside a full physical image.

### Integrity & verification
- MD5 and SHA-1 hashing at acquisition, then re-verifying against the stored hash.
- Cross-tool validation: the same physical device produced identical hashes in FTK Imager and Magnet AXIOM.
- Comparing my own hashes with a third-party examiner's report to detect evidence that may have been altered.

### Evidence handling & documentation
- Defining team roles: investigator, event recorder, photographer, imager, analyst and report writer.
- Crime-scene entry log, chain-of-custody form, and evidence bagging and labeling with case and evidence IDs.
- Writing reports for both technical and legal or administrative readers.

### Analysis
- Keyword searching across allocated and unallocated space.
- File metadata review: MAC timestamps, sector location, file attributes, MIME type.
- File signature analysis to catch files whose extension has been changed to hide their real type.
- Recovering passwords from evidence and using them to open protected archives.
- Building a case narrative (motive, timeline, key evidence) from recovered artifacts.

### Anti-forensics / data-hiding awareness
- Hidden attributes and unlabeled folders, deep or misleading directory nesting.
- Folders disguised as system folders (e.g., a CLSID-named folder that Windows displays as the Recycle Bin).
- Content hidden inside Office Open XML (`.docx` / `.xlsx` are ZIP archives of XML parts).
- White-on-white text, extension spoofing, image steganography, password-protected documents.

## Reference: Forensic Image Formats

| Format | Pros | Cons |
|--------|------|------|
| **RAW (dd)** | Exact bit-for-bit copy; readable by almost every tool; simple | No compression; no built-in case metadata or stored hash (kept separately) |
| **E01 (Expert Witness / EnCase)** | Compression; embedded case metadata; built-in checksums and stored hash for verification | Proprietary origin (though widely supported via libewf); must be converted for some raw-only tools |
| **SMART** | Compression and metadata support | Limited support in modern tools |
| **AFF / AFF4** | Open, documented format; compression and extensible metadata | Less widespread tool support than RAW or E01; original AFF superseded by AFF4 |

**Why the same evidence can give the same or different hashes:**
- The *same source* imaged as E01 and as RAW gives the **same** acquisition hash. The hash is calculated over the source data, not the container format.
- A *logical* image and a *physical* image of the same drive give **different** hashes. They cover different data: a single volume versus the entire device.
