# Case Report 02 — Evidence Integrity Review (Expert Witness)

[← Back to portfolio overview](https://github.com/yousifQU/digital-forensics-disk-analysis)

> University coursework, anonymized. Completed with a lab partner. Not solely my own work; the mock case and examiner report were provided by the course instructors.

| Field | Detail |
|-------|--------|
| **Case type** | Independent review of another examiner's findings |
| **Period** | Spring 2025, late January |
| **Format** | Paired lab |
| **Evidence** | Two raw disk images (suspect home drive, removable storage), the original examiner's report, the original Autopsy case file |
| **Tools** | dd (Windows port), certutil, Autopsy |
| **Hash algorithm** | MD5 |

---

## 1. Objective
Act as an expert witness. Independently verify the integrity of the evidence and the accuracy of a digital forensic examiner's report before it is relied on in court.

## 2. Scenario
In a mock criminal case, a digital forensic examiner had already analyzed two disk images and named three files of interest:
- a customer document (`.rtf`)
- a suspicious executable (`.exe`)
- a confidential document (`.docx`)

The defense needed an independent opinion on whether the evidence and the conclusions could be trusted.

## 3. Methodology

| Step | Action | Purpose |
|------|--------|---------|
| 1 | Made working copies of both images with `dd if=<image>.001 of=<copy>.img` | Never work on the provided originals |
| 2 | Hashed each copy with `certutil -hashfile <copy>.img MD5` | Get independent hash values |
| 3 | Compared the hashes with those in the examiner's report | Test evidence integrity |
| 4 | Opened the original Autopsy case and keyword-searched for the three named files | Test the report's specific claims |
| 5 | Reviewed metadata for each hit (path, size, MAC times, MD5, MIME type, allocation) | Corroborate the details |

## 4. Findings

| # | Check | Result | Status |
|---|-------|--------|--------|
| 1 | Home-drive image hash vs. report | Match | ✅ Verified |
| 2 | Removable-storage image hash vs. report | **Mismatch** | ❌ Not verified |
| 3 | Customer document | Found, allocated, in the user's `Documents` folder on the home-drive image | ✅ Corroborated |
| 4 | Suspicious executable | Found, allocated, at the root of the removable-storage image (Windows executable) | ⚠️ Found, but on an unverified image |
| 5 | Confidential document | No keyword search results in either image | ❌ Not corroborated |

## 5. Analysis
- **Finding 2 is the most serious.** A hash mismatch means the removable-storage image is not provably the same data the examiner analyzed. It may have been altered, corrupted or mislabeled.
- **That weakens Finding 4.** The executable is there, but it lives on the image whose integrity failed, so it can't be relied on as it stands.
- **Finding 5 is a gap in the report.** Keyword search can miss renamed, deleted or overwritten files, so this doesn't prove the document never existed. It does mean the report's claim isn't supported by the evidence as provided.
- Empty "change time" values on these FAT-formatted images are normal, because FAT doesn't record that timestamp. They were not treated as signs of tampering.

## 6. Conclusion & Recommendations
- The home-drive evidence and its finding **are reliable**.
- The removable-storage evidence **should not be relied on** until the original media is re-imaged and re-hashed, or the discrepancy is documented and explained.
- The examiner should be asked to show where the confidential document was found, with a path, hash and the method used to recover it.

## 7. Skills Demonstrated
Expert-witness review · `dd` imaging · command-line hashing with `certutil` · Autopsy keyword search and metadata review · assessing evidence reliability
