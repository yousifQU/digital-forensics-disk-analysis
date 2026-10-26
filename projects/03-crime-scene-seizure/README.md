# Project 3: Crime Scene Seizure — Bag & Tag

**Type:** Team lab (4 members) · **My role:** Report Writer · **Tools:** Hardware write blocker, FTK Imager, Windows Explorer

> Part of a university course and completed as a team. Not solely my own work; see the disclaimer in the main README. The scenario was entirely fictional, and all names and locations have been generalized.

## Situation
A judge had authorized the seizure of a suspect's workstation in a staged investigation, based on probable cause. The fictional suspect, a student, was believed to belong to a group planning two things on campus:
- spreading propaganda posters to computers in several campus labs
- running an executable on those machines to launch a **denial-of-service attack against the department's network routers**

Our team was assigned to seize the computer at a taped-off mock crime scene, preserve the evidence, image it, and work out how the attack was meant to be carried out.

## What I Did (as a Team)
1. **Assigned roles:**
   - Investigator and digital evidence analyst
   - Photographer and event recorder
   - Imager / acquisition expert
   - Report writer (my role): compiling the findings into a report readable by both technical and non-technical audiences, such as legal or administrative reviewers
2. **Documented the scene.**
   - Photographed the full scene and each item of evidence from several angles.
   - Kept a crime-scene entry log of everyone entering and leaving, with times.
3. **Preserved and tracked evidence.**
   - Completed a chain-of-custody form recording who released and who received each seized item.
   - Bagged and tagged every item with the case number and an evidence ID.
4. **Acquired the drive forensically.**
   - Connected the seized SSD through a hardware write blocker.
   - Copied the suspect's home folder to the forensic workstation for quick triage.
   - Created a **physical** E01 image with FTK Imager, so unallocated space would be included, and recorded its hash values.
5. **Analyzed the evidence** for files relevant to the planned attack.

## Results
Five files of interest were identified on the drive:

| Evidence | Location (generalized) | Relevance |
|----------|------------------------|-----------|
| Executable named after the planned operation | Desktop | Matches the description of the program intended to run the DoS attack |
| Unencrypted spreadsheet log | Documents | Appears to be a coded message log used to coordinate the group; one entry references starting the operation |
| Encrypted member list (ZIP) | Documents | After the password was recovered, it listed group members and named the suspect as the leader |
| Encrypted personal notes (ZIP) | Hidden in a rarely used profile folder | Described meeting dates, recruitment, and the attack method: flooding the network routers |
| Propaganda poster archive (ZIP) | Custom folder in the user profile | Posters meant to be pushed to lab computers |

**Case assessment:**
- Taken together, the notes, the member list and the executable show both **intent and preparation**.
- The team concluded the suspect could face a charge of **conspiracy to violate the Computer Fraud and Abuse Act (18 U.S.C. § 1030)**, plus violations of the institution's acceptable-use policy.
- The strongest evidence: the personal notes describing the router-flooding plan, the member list naming the suspect as leader, and the attack executable itself.

## Takeaways
- Defining roles clearly stopped steps from being duplicated or missed.
- Paperwork such as the entry log and chain of custody is what makes digital evidence admissible. It matters as much as the technical analysis.
- A quick logical copy is useful for triage, but the physical image is what preserves deleted and unallocated data.
