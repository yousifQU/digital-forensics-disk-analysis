# Case Report 03 — Crime Scene Seizure: Bag & Tag

[← Back to portfolio overview](https://github.com/yousifQU/digital-forensics-disk-analysis)

> University coursework, anonymized. Completed as a team of four. Not solely my own work; the scenario was designed by the course instructors and is entirely fictional. All names and locations are generalized.

| Field | Detail |
|-------|--------|
| **Case type** | Physical seizure, acquisition and analysis of a suspect's workstation |
| **Period** | Spring 2025, early February |
| **Format** | Team lab (4 members) |
| **My role** | Report Writer |
| **Legal basis** | Search and seizure authorized by a judge on probable cause (mock affidavit and warrant) |
| **Evidence** | Suspect workstation and its internal SSD |
| **Tools** | Hardware write blocker, FTK Imager, Windows Explorer |

---

## 1. Objective
Seize a suspect's computer from a controlled crime scene following proper evidence-handling procedure, acquire its drive forensically, and determine how a planned attack was meant to be carried out.

## 2. Scenario
An anonymous tip reported that a group of students planned two actions:
- break into several campus computer labs and push propaganda posters to the machines
- run an executable on those machines to launch a **denial-of-service (DoS) attack against the department's network routers**

One member's workstation was seized under a warrant. The scene was taped off to simulate an active investigation.

## 3. Team Roles

| Role | Responsibility |
|------|----------------|
| Investigator / Digital Evidence Analyst | Directed the scene, analyzed the drive (allocated and unallocated space), signed the chain-of-custody form |
| Photographer / Event Recorder | Photographed the scene and evidence, maintained the crime-scene entry log |
| Imager / Acquisition Expert | Imaged the seized SSD with FTK Imager |
| **Report Writer (me)** | Compiled findings into a report readable by technical and non-technical (legal/administrative) audiences |

## 4. Methodology

| Phase | Action |
|-------|--------|
| Scene control | Logged every person entering and leaving the scene with times; photographed the scene before anything was touched |
| Seizure | Identified the workstation and its SSD as evidence; assigned each item a case number and evidence ID |
| Preservation | Bagged and tagged each item; recorded each transfer on a chain-of-custody form (released by / received by, date, time) |
| Acquisition | Connected the SSD through a hardware write blocker; copied the user's home folder for quick triage; created a **physical E01 image** in FTK Imager and recorded its hash values |
| Analysis | Examined the user profile and archives for files related to the planned attack; opened encrypted archives with passwords found during the investigation |
| Reporting | Documented findings, case assessment and the evidence linking the suspect to the plan |

## 5. Findings

| ID | Item (generalized) | Location | Significance |
|----|--------------------|----------|--------------|
| F1 | Executable named after the planned operation | Desktop | Matches the program described for the DoS attack |
| F2 | Unencrypted spreadsheet message log | Documents | Coded log used to coordinate the group; references the start of the operation |
| F3 | Encrypted member list (ZIP) | Documents | Lists members and their roles; names the suspect as leader |
| F4 | Encrypted personal notes (ZIP) | Rarely used profile folder | Meeting dates, recruitment, and the attack method (flooding the routers with traffic) |
| F5 | Poster archive (ZIP) | Custom folder in the profile | Propaganda intended for the lab computers |

## 6. Case Assessment
**Reconstructed timeline (from the notes and logs):**
1. The group formed and the suspect took the leader role.
2. Members were recruited and regular meetings were held.
3. The posters and the attack executable were prepared.
4. The operation was scheduled to start: push the posters to lab machines and run the executable to flood the routers.

**Motive:**
- spread the group's message across campus
- show off the group's technical capability

**Potential offenses:**
- conspiracy to violate the **Computer Fraud and Abuse Act (18 U.S.C. § 1030)**
- violations of the institution's acceptable-use policy

**Strongest evidence:**
- F4, the notes describing the attack plan
- F3, the member list naming the suspect as leader
- F1, the executable itself

Together these show both intent and preparation.

## 7. Conclusion
The evidence was seized, documented and acquired without altering the original drive. The recovered files support the conclusion that the suspect led the planned attack. The documentation (entry log, photographs, chain of custody and hash values) supports the evidence's admissibility.

## 8. Skills Demonstrated
Crime-scene procedure · chain of custody · evidence bagging and tagging · write-blocked physical imaging · encrypted-archive analysis · case reconstruction · report writing for legal audiences
