# Project 2: Evidence Integrity Review (Expert Witness)

**Type:** Paired lab · **Tools:** dd (Windows port), certutil, Autopsy

> Part of a university course and completed with a lab partner. Not solely my own work; see the disclaimer in the main README.

## Situation
In a mock criminal case, we were hired as **expert witnesses** to review an investigation already done by another digital forensic examiner. We received:
- the examiner's written report
- two raw disk images: a suspect's home drive and a removable storage device
- the Autopsy case file used to produce the report

Our job was to independently check whether the evidence and the report's claims hold up.

## What I Did
1. **Copied both evidence images with `dd`** to working files, so the provided originals were never analyzed directly:
   ```
   dd if=<evidence>.001 of=<working_copy>.img
   ```
   The Windows port of `dd` is run without `sudo`, and it shows progress with `--progress` rather than GNU `dd`'s `status=progress`.
2. **Hashed both copies** and compared them with the hashes in the examiner's report:
   ```
   certutil -hashfile <working_copy>.img MD5
   ```
3. **Opened the original Autopsy case** and used keyword search to locate the three files of interest named in the report: a customer document, a suspicious executable and a confidential document.
4. **Reviewed file metadata** for each hit: location, size, MAC times, MD5 hash, MIME type and allocation status.

## Results
| Check | Finding |
|-------|---------|
| Hash of home-drive image | **Matched** the examiner's report |
| Hash of removable-storage image | **Did not match** the examiner's report |
| Customer document (`.rtf`) | Found, allocated, in the user's `Documents` folder on the home-drive image |
| Suspicious executable (`.exe`) | Found, allocated, at the root of the removable-storage image (identified as a Windows/DOS executable) |
| Confidential document (`.docx`) | **Not found.** Keyword search returned no results |

## Conclusions (Expert Review)
- **The integrity of the removable-storage image can't be confirmed.** Its hash differs from the one the examiner reported, so it may have been altered or mislabeled after acquisition. Anything derived from it, including the suspicious executable, should be treated as unreliable until the image is re-acquired or the discrepancy is explained.
- **The report cites a file that could not be corroborated.** The confidential document did not appear in the case data. This doesn't prove the file never existed, since keyword search can miss renamed or overwritten files. It does mean the report's claim isn't supported by the evidence provided.
- The home-drive evidence held up: its hash verified and the customer document was where the report said it would be.

## Takeaways
- An expert witness checks the evidence independently and doesn't take the original examiner's word for it.
- A single hash mismatch can undermine every finding that depends on that image.
- On FAT-formatted media, empty "change time" fields are normal. FAT does not record a metadata change time, so this is not evidence of tampering.
