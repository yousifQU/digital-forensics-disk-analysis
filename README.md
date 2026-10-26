# Case Report 04 — Contraband Image Investigation

[← Back to portfolio overview](https://github.com/yousifQU/digital-forensics-disk-analysis)

> University coursework, anonymized. Not solely my own work; the case and disk image were provided by the course instructors. The "crime" is a deliberately absurd training scenario.

| Field | Detail |
|-------|--------|
| **Case type** | Contraband search and hidden-file recovery on a seized disk |
| **Period** | Spring 2025, mid-semester |
| **Format** | Individual lab |
| **Evidence** | One raw (`.dd`) disk image of a seized computer |
| **Tools** | Magnet AXIOM, Autopsy, TinEye |
| **Hash algorithm** | MD5 |

---

## 1. Objective
Determine whether contraband was present on a seized computer, document every chargeable item with its full path, and recover a hidden questionnaire to answer its forensic questions.

## 2. Scenario
In a fictional jurisdiction, knowingly possessing digital images of money is a felony. A visitor reported that the homeowner had shown him such images and printed a sample. That statement gave probable cause for a search warrant. The computer was seized and imaged, and the owner declined to answer questions and retained an attorney.

## 3. Methodology

**Part A: Contraband search (Magnet AXIOM)**

| Step | Action |
|------|--------|
| 1 | Loaded the disk image into AXIOM and processed all files |
| 2 | Located the specific image described in the probable-cause statement |
| 3 | Reviewed media, document and other artifact categories for currency or coin content |
| 4 | Logged each item's name and full path in an artifact table |

**Part B: Hidden questionnaire (Autopsy)**

| Step | Action |
|------|--------|
| 1 | Opened the image in Autopsy and recorded the image's MD5 hash |
| 2 | Found a password file disguised with a system-library (`.dll`) style name, and a separate password-protected ZIP |
| 3 | Used the password to open the ZIP and extract the questionnaire |
| 4 | Found a picture whose extension had been changed from `.gif` to `.fig`, and confirmed by its file header that it is really a GIF |
| 5 | Recorded the picture's MD5 hash, sector location, size, attributes and MAC times |
| 6 | Identified the person in the picture with a reverse image search (TinEye) |

## 4. Findings

| # | Finding | Result |
|---|---------|--------|
| 1 | Image named in the probable-cause statement | ✅ Located on the disk |
| 2 | Contraband items (case total: 64; required: 55) | ✅ **61 documented** with names and full paths |
| 3 | Contraband types | Images and other file types depicting paper currency and coins |
| 4 | Protected archive | ✅ Unlocked with a password stored on the same disk |
| 5 | Disguised picture | ✅ GIF renamed to `.fig`, ~11 KB, in the user's documents folder |
| 6 | Questionnaire author | ⚠️ Could not be determined from the available metadata |

## 5. Analysis
- **Possession is supported.** The specific image from the witness statement was found, along with a large collection of similar files.
- **Several files were deliberately concealed:**
  - a renamed extension, which hides the picture from searches that filter on image extensions
  - a misleadingly named password file
  - an encrypted archive

  Concealment like this can support the "knowingly" element of the offense.
- **Questions for legal clarification:**
  - Do references to payment-card companies count as "money"? These were excluded, as the case instructions directed.
  - Do partial or embedded depictions count as possession?

## 6. Conclusion
The disk contained the image described in the warrant affidavit and at least 61 contraband items, several of them deliberately hidden. Where something could not be established, such as the questionnaire's author, it is stated plainly rather than assumed.

## 7. Skills Demonstrated
Large-scale artifact review in AXIOM · Autopsy metadata analysis · file signature analysis · password and archive recovery · reverse image search · evidence documentation
