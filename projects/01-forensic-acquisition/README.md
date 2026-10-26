# Project 1: Forensic Acquisition & Hash Verification

**Type:** Individual lab · **Tools:** FTK Imager, Magnet AXIOM, WMIC, Windows Disk Management

> Part of a university course. Not solely my own work; see the disclaimer in the main README.

## Situation
Before any evidence can be analyzed it has to be acquired in a way that can be defended. The goal was to image a USB drive several ways, with two different tools, and show with hashes that each image accurately represents its source. The exercise also had to explain why some hashes match and others don't.

## What I Did
1. **Prepared and documented the target drive.**
   - Formatted a USB drive.
   - Recorded its model, serial number, size and partition count with WMIC.
   - Confirmed its drive letter and file system (FAT16) in Disk Management.
2. **Seeded test evidence.** Placed a picture, an Excel workbook, a Word document and a PowerPoint file on the drive.
3. **Processed the drive in Magnet AXIOM.**
   - Created a case and loaded the drive as evidence.
   - Confirmed in AXIOM Examine that all four files were parsed. AXIOM also surfaced extra system and browser artifacts, such as an incomplete download file.
4. **Acquired with Magnet AXIOM** in E01 format, with MD5 and SHA-1 hashing and image verification turned on.
5. **Acquired with FTK Imager, three ways:**
   - Logical image, E01 format (fragmentation and compression set to 0)
   - Logical image, RAW format
   - Physical image of the whole device
6. **Compared the verification results** of all images.

## Results
| Image | Sectors (512 B) | Approx. size | Verification |
|-------|-----------------|--------------|--------------|
| FTK logical, E01 | 102,400 | ~50 MB (volume) | MD5 & SHA-1 match |
| FTK logical, RAW | 102,400 | ~50 MB (volume) | MD5 & SHA-1 match, **identical to the E01 hash** |
| FTK physical | 15,728,640 | ~8 GB (whole device) | MD5 & SHA-1 match |
| AXIOM acquisition | n/a | n/a | MD5 & SHA-1 **identical to the FTK physical hash** |

- **E01 and RAW logical images had the same hash.** The hash is computed over the acquired data, not the image container, so the format doesn't change it.
- **Logical and physical images had different hashes and very different sizes.** The physical image covers the whole device, including partition structures and unallocated space. The logical image covers only the ~50 MB FAT16 volume.
- **Two independent tools produced the same hash** for the same physical device. This cross-validates both acquisitions.
- No bad blocks were reported in any image.

## Takeaways
- A hash is only meaningful when you know exactly what data it covers.
- Validating with a second tool is a cheap way to strengthen confidence in an acquisition.
- Physical acquisition is the default whenever deleted or unallocated data could matter.
