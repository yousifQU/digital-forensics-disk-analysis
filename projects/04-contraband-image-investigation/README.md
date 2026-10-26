# Project 4: Contraband Image Investigation

**Type:** Individual lab · **Tools:** Magnet AXIOM, Autopsy, TinEye

> Part of a university course. Not solely my own work; see the disclaimer in the main README. The "crime" is a deliberately absurd training scenario.

## Situation
In a fictional jurisdiction, knowingly possessing digital images of money is a felony. A visitor to a suspect's home reported being shown such images, and that report gave probable cause for a search warrant. The suspect's computer was seized and imaged, and the suspect declined to answer questions.

I was given the disk image and asked to:
1. Confirm whether the specific image described in the probable-cause affidavit was on the disk.
2. Find and document **all** contraband (anything showing paper currency or coins) with names and full paths. The case contained 64 items; the lab required at least 55.
3. Recover a hidden, password-protected questionnaire and answer its forensic questions.

## What I Did
**Part 1: Contraband search (Magnet AXIOM)**
- Loaded the disk image into Magnet AXIOM and processed all files.
- Located the specific image referenced in the affidavit.
- Reviewed media and document artifacts across the whole image. Contraband was not limited to pictures, so I checked other artifact types too.
- Recorded every contraband item with its file name and full path in an artifact table.

**Part 2: Hidden form recovery (Autopsy)**
- Opened the image in Autopsy and recorded the forensic image's MD5 hash.
- Found a file holding a password and a separate password-protected ZIP. The password file used a name that looked like a system file (`.dll`).
- Used the recovered password to open the ZIP and extract the questionnaire.
- Found an image file whose extension had been changed from `.gif` to `.fig`. This keeps it out of searches that filter by image extension, but the file header still identifies it as a GIF.
- Recorded the image's MD5 hash, sector location, size and MAC timestamps.
- Identified the public figure in the photo with a reverse image search.

## Results
- **The probable-cause image was confirmed** on the disk.
- **I documented 61 of the 64 contraband items**, above the 55-item threshold, each with name and full path.
- The hidden questionnaire was recovered.
- The disguised GIF (about 11 KB, in the user's documents folder) was found and fully documented.
- The questionnaire's author could not be determined from the available metadata, and I reported this as a finding rather than guessing.

## Takeaways
- Never rely on file extensions. File signature (header) analysis is what reveals a renamed file's real type.
- Passwords are often stored on the same system as the files they protect, frequently under misleading names.
- When something can't be determined, the report should say so. That is better than over-stating a conclusion.
