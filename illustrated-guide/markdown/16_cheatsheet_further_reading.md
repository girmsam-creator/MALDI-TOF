# Cheat Sheet & Further Reading

## Purpose

This tab is a reference appendix, not a new topic. It gathers quick lookup tables for the real matrices, calibration standards, target plates, tolerances, software commands, and diagnostic ions used on this lab's own Bruker UltrafleXtreme MALDI-TOF/TOF (Matrix-Assisted Laser Desorption/Ionization, Time-Of-Flight instrument), plus the full list of sources behind this guide. Come back here once the concepts from earlier tabs are familiar and you just need to look something up fast.

## Quick-reference tables

### Matrices

| Matrix | Best for | Notes |
| --- | --- | --- |
| HCCA (alpha-cyano-4-hydroxycinnamic acid) | Peptides and proteins, 0.7 to 20 kDa | The default matrix for most work in this lab; can suppress larger glycopeptides above about 5 kDa |
| 2,5-DHB | A wide variety including phosphopeptides and glycoproteins | Milder than HCCA; used for acidic, sialylated glycopeptides in linear mode |
| 2,5-DHAP | Proteins, 8 to 100 kDa | Prevents ISD fragmentation (so not used for ISD itself); good for glycoproteins and acidic glycopeptides in linear mode |
| SA (sinapinic acid) | Larger proteins, 10 to 150 kDa | Also used for ISD spectra of intact proteins; weak for small peptides under 3 kDa, use HCCA instead |
| SDHB | Very large proteins and glycoproteins | Also suitable for ISD spectra of intact proteins |
| 3-HPA | Oligonucleotides, 1 to 30 kDa | Not part of this lab's peptide/glycopeptide workflow, included for completeness |
| 1,5-DAN | Top-down (ISD) sequencing of intact proteins | Promotes disulfide reduction in the gas phase; hazardous, make a fresh solution immediately before use |

### Calibration standards used in this lab

| Standard | Contents | Exact masses |
| --- | --- | --- |
| Peptide Calibration Standard II | 8 peptides, about 700 to 3500 Da (the Instructions for Use state nine peptides, but only eight are listed with masses; this guide uses the eight given) | Bradykinin 1 to 7: 757.3992, Angiotensin II: 1046.5418, Angiotensin I: 1296.6848, Substance P: 1347.7354, Bombesin: 1619.8223, ACTH clip 1 to 17: 2093.0862, ACTH clip 18 to 39: 2465.1983, Somatostatin 28: 3147.4710 ([M+H]+ monoisotopic) |
| Protein Calibration Standard I | 4 proteins, about 4000 to 20,000 Da | Insulin 5734.51, Ubiquitin I 8565.76, Cytochrome C 12360.97, Myoglobin 16952.30 ([M+H]+ average) |
| Protein Standard II | 3 proteins, roughly 10,000 to 50,000+ Da | Trypsinogen 23982, Protein A 44613, BSA approx. 66.5 kDa ([M+H]+ average); BSA itself is not recommended as a calibrant because of its mass heterogeneity |

Always match the calibrant's matrix to the sample's matrix, and store calibrants frozen; never refreeze a thawed aliquot.

### Target plates

| Plate | Anchor size | Used for |
| --- | --- | --- |
| Ground steel | None (flat surface) | The default plate for most manual work |
| AnchorChip | 800 micron | High-throughput or automatic runs; concentrates dilute samples; one calibration spot per four sample spots |
| BigAnchor | 2000 micron | Matrices that don't crystallize well on the narrower AnchorChip, for example 2,5-DHAP |
| SmallAnchor | 400 micron | Oligonucleotides prepared with 3-HPA |
| Polished steel | None | Samples with low surface tension; wash immediately after use |

Plate layout: 384 spots, 16 rows (A to P) by 24 columns (1 to 24).

### Tolerance quick-reference

| Check | Acceptable value |
| --- | --- |
| Calibration error, peptides | Under 5 ppm |
| Calibration error, intact proteins | Under 100 ppm |
| Detector check | Run monthly and before important projects; adjust detector gain if the recommended voltage differs from the current one by more than 30 V |
| PMF search tolerance | Strict default 0.1 Da (needs excellent calibration); widen to 0.5 Da, then 1.0 Da, if no hit |
| MASCOT MS tolerance | Commonly around 40 ppm |
| MASCOT MS/MS tolerance | Up to 1000 ppm |

### Software quick-reference

flexControl method names spell out the method: LIFT = MS/MS mode, L = linear, R = reflector, P = positive ion mode, N = negative ion mode, and the numbers give the mass range. For example, "RP 700-3500" means reflector, positive, 700 to 3500 Da.

flexAnalysis peak picking: Centroid (the whole-peak average, for large molecules whose isotopes can't be resolved) versus Snap (the monoisotopic peak, for peptides and other molecules small enough to resolve isotopes).

flexAnalysis calibration command sequence: Calibrate > Internal > Automatic assign > Calibrate, then Calibrate > Copy calibration, then select the sample spectra and Calibrate > Replace calibration.

### Glycopeptide diagnostic numbers

Oxonium ions: 204 Da and 366 Da.

Diagnostic mass distances: 162 Da (hexose), 203 Da (HexNAc), 291 Da (sialic acid / NeuAc).

MALDI-TOF/TOF-specific terminal HexNAc fragmentation pattern: a set of four signals spaced 17, 83, and 120 Da apart, from cross-ring cleavage of the terminal HexNAc. This is a distinct, smaller-mass pattern from the oxonium ions and mass distances above, not another way of writing the same numbers.

Fucose is sometimes quoted elsewhere as a 146 Da diagnostic mass step, but that number does not appear anywhere in this lab's own instrument documentation, so treat it as general glycobiology knowledge rather than something confirmed for this setup.

## Figure

A figure (The five-step MALDI-TOF/TOF workflow from sample and matrix to final identification, based on the "Cheat Sheet & Further Reading" tab of the MALDI-TOF Study Guide.) appears in the illustrated HTML version of this guide. Alt text: A left to right box and arrow diagram showing a sample loaded on the target plate with matrix, going into the MALDI-TOF/TOF instrument for ionization and flight, producing a mass spectrum of m/z peaks, which flexAnalysis calibrates and picks peaks from, ending in a protein or glycopeptide identification.

## Further reading and sources

**Sources used in this guide**

All drawn from the lab's own "Equipment literature/MALDI" folder:

- "03 Glyco MS Detection and Fragmentation techniques" and "05 Classification ID Glycopeptides Introduction" (Bruker Daltonics training material), the source for fragmentation techniques (LID, heCID, ESI-CID, ETD/ECD), oxonium ion values, and the peptide/glycan classification workflow, including the real EEQFNSTFR mouse IgG1 glycopeptide example.
- "04 GlycoQuest Introduction" (Bruker Daltonics training material), the source for the GlycoQuest search workflow, scoring metrics, and search parameters.
- In-gel digestion.docx (Shevchenko-style protocol, citing Shevchenko et al., *Anal. Chem.* 1996 / *Nature Protocols* 2006), the source for the trypsin digestion protocol and its controls.
- Lopez & Hummon (2026). MALDI spatial proteomics: a mini review of approaches and techniques. *Analytical Methods*, 18, 963 to 972 (file: d5ay01341k.pdf), the source for the MALDI imaging ("site mapping") workflow, matrix application methods and resolution figures, and tumor-mapping examples.
- Hermann, Schurgers & Jankowski (2022). Identification and characterization of post-translational modifications: Clinical implications. *Molecular Aspects of Medicine*, 86, 101066 (file: 1-s2.0-S0098299722000036-main.pdf), the source for PTM-analysis clinical context, digestion-depth trade-offs, multiplexed PTM quantification (iTRAQ/TMT), and the MALDI-TOF serum N-glycan breast-cancer biomarker example.
- Kostidis, Mork, Rabelink, Giera & Ogrinc (2026). Mapping metabolism using stable isotope tracers in combination with mass spectrometry imaging. *Trends in Analytical Chemistry*, 196, 118679 (file: 1-s2.0-S0165993626000348-main.pdf), the source for MALDI-2 post-ionization mechanism, t-MALDI, and spatial-resolution comparisons across imaging-MS platforms.
- The phosphorylation and O-GlcNAcylation analysis explanations, and the 2023 to 2026 trends list, draw on general proteomics knowledge and live web sources cited inline in those sections, rather than on files in the lab's folder.

**Further reading for other applications (not this lab's current workflow)**

The bacterial-identification literature this guide drew on earlier is still worth knowing about if you ever use MALDI-TOF for microbial identification elsewhere, even though it isn't what this particular lab's instrument is set up for:

- Koskinen, E. (2015). *MALDI-TOF MS -menetelman soveltuvuus Pasteurellaceae-heimon bakteerien tunnistuksessa* (B.Eng. thesis, Metropolia UAS / Evira).
- Lay, J.O. (2001). MALDI-TOF mass spectrometry of bacteria. *Mass Spectrometry Reviews*.
- microorganisms-12-00322 (2024 journal article), on Biotyper/VITEK MS/ASTA MicroIDSys scoring systems.
- Harju & Gronroos (2020). MALDI-TOF-massaspektrometria kliinisessa mikrobiologiassa. *Duodecim* (file: duo15709.pdf).
- s41597-025-04504-z (2025). Dataset descriptor for a public Robert Koch Institute MALDI-TOF spectral database. *Scientific Data*.

**Real Aalto instrument documentation added for this overhaul**

This overhaul is built on real documentation for the actual Bruker UltrafleXtreme MALDI-TOF/TOF and its software at Aalto's Molecular Biotechnology lab:

- "Bruker MALDI-TOFF" instrument specification sheet, and "BRUKER MALDI-TOF/TOF INSTRUCTIONS" (Mari Piirainen, 2017, updated by Kiia Malinen, 2025), covering the physical instrument, target plates, and calibration standards in everyday lab use.
- "MALDI software essentials" (Mari Piirainen, 2017), the flexControl and flexAnalysis software walkthrough.
- "MALDI lab instructions" (Mari Piirainen, 2018), the glassware, solvent, and contamination rules behind the lab discipline section.
- "Bruker Guide to MALDI Sample Preparation" and "MALDI prep protocols lifescience 160301", the source for the exact dried-droplet recipes and target plate types.
- The Instructions for Use for Peptide Calibration Standard II, Protein Calibration Standard I, and Protein Standard II (Bruker, Revision C, May 2021), the source for the exact calibrant masses used throughout this guide.
- "Detector check" and "Tolerances of MALDI TOF MS" (citing *J. Chromatography A* 894 (2000) 345 to 355), the source for the detector voltage and buffer/detergent tolerance figures.
- "How to choose a matrix" and "MALDI matrices", the source for the matrix guidance and the table above.
- "Automated MALDI and MASCOT search" (Mari Piirainen, 2017), "Maldi instructions for PMF and MS-MS of protein digests" (Teemu Valisalmi, 2025), and "MSMS and peptide identification" (Mari Piirainen, 2017), the source for the automated and manual protein-identification pipeline.
- "Intact proteins and ISD" (Mari Piirainen, 2017) and "Introduction MALDI-TOFTOF 150120" (a Bruker Daltonik training deck), the source for the TOF/TOF physics and ISD top-down sequencing workflow.
- "Introduction LCMALDI WLC14 PS40 160615" (a Bruker training deck), the source for the LC-MALDI and WARP-LC workflow.
- "Glycopeptide identification with ProteinScape" (the Aalto lab's own SOP, Mari Piirainen, 2017), alongside the Bruker training decks already listed above, the source for the real Aalto Classification and GlycoQuest operating parameters.

Quoted numbers throughout this guide come from these documents; a few worked-example intensities and simulated "observed" values are explicitly labeled illustrative, built on real reference masses to demonstrate the reasoning.

**Real videos worth watching**

These are real, existing videos on the open web (not generated for this guide), picked for how well they match a topic in this guide:

- MALDI-TOF Mass Spectrometry Explained, a plain-language walkthrough of ionization, flight, and detection.
- MALDI-TOF Mass Spectrometry (ScienceSketch), a whiteboard-style animation of the same core mechanism.
- Theory of MALDI-TOF Mass Spectrometry, a more technical treatment of the physics behind ionization and time-of-flight separation.
- MALDI Explained For Beginners, a slower-paced introduction for students seeing the technique for the first time.
- MALDI Mass Spectrometry Imaging for the Masses: An Introduction to MALDI MSI, a dedicated introduction to how imaging builds a molecular map pixel by pixel.
- Introduction to Mass Spectrometry Imaging, broader context on imaging-MS approaches, MALDI included.
- Mass Spectrometry Imaging of Metabolites and Lipids in Tissue Sections, closest match to the metabolomics example in this guide.
- Spatial Awareness with MALDI Imaging, a practical perspective on setting up an imaging experiment.
- MALDI Mass Spectrometry, a general-purpose overview video.

## What to take forward

Treat this tab as a lookup, not new material: every number here was already introduced with its reasoning earlier in the guide, and quoted figures come from real instrument documentation and cited papers rather than invented values. When in doubt about a mass, tolerance, or matrix choice, check back here first before searching further afield.

## Glossary terms introduced

- **ppm (parts per million):** a way of expressing a small measurement error as a fraction of the measured mass, used here for calibration error and search tolerances.
- **Oxonium ion:** a small, positively charged sugar fragment (here at 204 Da or 366 Da) that signals the presence of a glycan in a glycopeptide spectrum.
- **Dalton (Da):** the unit of mass used throughout this guide for peptides, proteins, and mass differences; one Dalton is about the mass of one hydrogen atom.
