# Practice Scenarios: Real Studies to Work Through

## Purpose

Every other tab in this guide explains a method. This tab is for practicing one: each scenario below is built from a real, published source, a university teaching page, a peer-reviewed paper, or a vendor application note, with real instrument data, not an invented textbook example. You are given the same kind of numbers a real analysis hands you, asked to work through them the way this lab's workflow does, and then shown a worked solution to check against. Treat these as practice problems, not as facts to memorize: the point is applying the methods from the other sixteen tabs to data nobody rounded off for you.

## Key ideas

Ten scenarios are included here, one for each major method covered elsewhere in this guide: PMF and MS/MS protein identification, MALDI in-source decay (ISD) of an intact protein, glycopeptide composition analysis, phosphorylation site mapping, whole-cell bacterial identification, a contamination troubleshooting case, an LC-MALDI pipeline, locating a protease cut site in an intact protein from mass balance alone, top-down CID fragmentation of a whole intact protein ion, and mapping a single O-GlcNAc site on a transcription factor from a peptide mass shift. The last three give the full-protein, protein-fragment, and single-residue-modification side of this guide's core skills and case-study tabs its own worked practice, alongside the peptide-level scenarios above. Each scenario gives its source in full so you can go look at the original data yourself, states exactly what was reported versus what is calculated from it, and ends with a worked solution. Work the task first before reading the worked solution. A short note on honesty: three of the ten sources did not report every number a complete exercise would want (an ISD source whose full fragment ladder exists only as a spectrum figure, a glycopeptide source that does not name its matrix, and an O-GlcNAc source whose own figure caption mislabels its numbers), and those gaps and inconsistencies are stated rather than filled in with a guess.

## Scenario 1: Identifying a protein by PMF (the "is this really BSA" check)

**Source.** Biomolecular Analysis Laboratory, Institute for Protein Research, Osaka University, worked example "Peptide Mass Fingerprinting and Protein Identification (Reflector Mode)" (public core-facility teaching page, 2023), using an in-gel tryptic digest of bovine serum albumin (BSA) measured on a Bruker Autoflex maX and searched with MASCOT.

**The data you are given.** A MASCOT search of the peptide mass list returned albumin, *Bos taurus* (ALBU_BOVIN), with a MASCOT score of 106 (Expect 1.7 x 10^-6), 40 masses searched and 13 matched, giving 22% sequence coverage. The 13 matched peptides, with their observed mass (Da, MH+) and calculated mass (Da, MH+):

| Residues | Observed | Calculated | Peptide |
| --- | --- | --- | --- |
| 161-167 | 927.5143 | 926.4861 | YLYEIAR |
| 161-168 | 1083.6220 | 1082.5872 | YLYEIARR |
| 223-232 | 1209.6341 | 1208.5972 | CASIQKFGER |
| 233-241 | 1001.6147 | 1000.5818 | ALKAWSVAR |
| 298-309 | 1560.8159 | 1559.8051 | LKECCDKPLLEK |
| 347-359 | 1567.7611 | 1566.7354 | DAFLGSFLYEYSR |
| 360-371 | 1439.8313 | 1438.8045 | HPEYAVSVLLR |
| 402-412 | 1305.7225 | 1304.7088 | HLVDEPQNLIK |
| 413-433 | 2543.2746 | 2542.2274 | QNCDQFEKLGEYGFQNALIVR |
| 421-433 | 1479.8203 | 1478.7881 | LGEYGFQNALIVR |
| 437-451 | 1639.9582 | 1638.9305 | KVPQVSTPTLVEVSR |
| 508-523 | 1894.9556 | 1893.9295 | RPCFSALTPDETYVPK |
| 549-557 | 1014.6032 | 1013.6121 | QTALVELLK |

**Task.**

1. Two of these peptides, residues 161-167 and 161-168, share the same start position and almost the same sequence. What does that tell you about trypsin's cut after residue 168, and what is this phenomenon called elsewhere in this guide?
2. Residues 413-433 (QNCDQFEKLGEYGFQNALIVR) and 421-433 (LGEYGFQNALIVR) overlap the same way. Using the cheat sheet's rule that trypsin cuts after K or R (except before P), find the missed cleavage site in the longer peptide.
3. Calculate the mass error, in ppm, for the peptide HLVDEPQNLIK (residues 402-412): ppm = (observed - calculated) / calculated x 10^6.
4. With only 22% sequence coverage and 13 of 40 searched masses matched, would you call this a confident identification? Use the common-errors tab's "how to tell if a result is good" table to justify your answer with the actual Expect value above.

### Answers

1. Trypsin normally cuts after every K or R. A peptide ending at residue 167 (...IAR) and one ending at 168 (...IARR) sharing the same start means the enzyme cut after residue 167 in some copies of the protein and read through to the next R at 168 in others. This is a missed cleavage, the same phenomenon the case-study tab flags when a tryptic peptide contains an internal K or R that was not cut.
2. QNCDQFEKLGEYGFQNALIVR contains an internal K (the "EK" in the middle of the sequence) that was not cut, which is why the shorter peptide LGEYGFQNALIVR (starting right after that K) is also present in the list as the fully-cleaved version of the same region.
3. (1305.7225 - 1304.7088) / 1304.7088 x 10^6 = 1.0137 / 1304.7088 x 10^6, which is about 777 ppm. That is far looser than the under-5-ppm peptide calibration standard this lab targets, which fits a teaching-page example run without a tightly optimized calibration rather than a production identification.
4. The Expect value of 1.7 x 10^-6 is extremely small, meaning a match this good happening by chance is very unlikely, so the identification itself is statistically confident even though the sequence coverage (22%) and matched-mass fraction (13 of 40) are both modest. Coverage and match fraction describe how much of the protein you can see, not how sure you are of what you found; a low Expect value is what the common-errors tab's "trust it" column is really pointing at.

## Scenario 2: Reading an in-source decay (ISD) ladder on an intact protein

**Source.** K. Shima, "MALDI-TOF Mass Spectrometry: Protein Sequence Analysis by In-Source Decay Using a Benchtop MALDI-TOF Mass Spectrometer," Shimadzu Application News No. B69 (LAAN-A-TM-E042), Shimadzu Corporation, October 2017, using a Shimadzu MALDI-8020 benchtop instrument.

**The data you are given.** Intact BSA (bovine serum albumin) was first measured in linear mode with sinapinic acid (SA) matrix, giving an intact protonated mass of m/z 66430. A separate 5 pmol BSA sample was then prepared with 1,5-diaminonaphthalene (1,5-DAN) matrix and run in ISD mode. The resulting c-ion series spanned c9 to c44, with c34, c39 and c42 absent from the series. One specific fragment, c33, was reported at m/z 3886 and used as a pseudo-precursor mass for a MASCOT search that confirmed the protein's identity.

**Task.**

1. Why was sinapinic acid used for the intact-mass measurement but 1,5-DAN used for the ISD run? Check this guide's matrix table (mechanism tab) for what each matrix is suited to.
2. The c-ion series runs from c9 to c44 with three gaps. What does a gap in an ISD ladder mean about that particular backbone bond, in plain terms?
3. If this lab were running this same ISD experiment, which flexControl setting from the sample-prep tab would need to change from a typical peptide PMF method, and why?
4. The c33 fragment at m/z 3886 was used as a "pseudo-precursor" for a database search rather than the intact 66430 mass. What does that suggest about how ISD fragments are used for confirmation, compared to using the whole intact mass alone?

### Answers

1. Sinapinic acid is listed in this guide's matrix table as suited to larger proteins (roughly 10 to 150 kDa), which fits a simple intact-mass check of a ~66 kDa protein. 1,5-DAN is listed specifically as helping top-down ISD sequencing of intact proteins, which is exactly the fragmentation behavior this second step needed; SA does not reliably drive the same in-source fragmentation chemistry.
2. A gap means no usable amount of that particular c-ion was detected, most likely because that backbone bond fragments poorly under ISD conditions or the resulting fragment's intensity fell below the detection threshold; it does not necessarily mean the protein has a different sequence there, only that the ladder has a missing rung at that position.
3. Because this is an intact, large protein being analyzed without digestion, the sample-prep tab's logic flips to linear mode (not reflector) and a lower sample rate (around 1.00 rather than 2.00), the same combination the sample-prep tab gives for large proteins, since reflector mode and a high sample rate are tuned for small, robust peptides instead.
4. Using a single fragment mass (c33) as a pseudo-precursor for a database search shows that one well-resolved ISD fragment, treated like a short peptide's own mass, can be searched on its own to confirm identity, without needing to assemble the entire c-ion ladder into a full sequence first. This is a faster confirmation step than reading out the whole ladder by hand, at the cost of depending on just one fragment being correctly assigned.

## Scenario 3: Working out a glycan composition from a mass difference

**Source.** Song X, Lasanajak Y, Rivera-Marrero C, Luyai A, Willard M, Smith DF, Cummings RD, "Generation of a Natural Glycan Microarray Using 9-Fluorenylmethyl Chloroformate (FmocCl) as a Cleavable Fluorescent Tag," *Analytical Biochemistry*, 2009, 395(2):151-160, using a Bruker Ultraflex-II MALDI-TOF/TOF. Glycopeptides were derived from horseradish peroxidase, a plant glycoprotein, and separated into fractions by 2D-HPLC before MALDI analysis. The matrix used is not stated in the accessible text of this source.

**The data you are given.** Four fractions, reported as [M+Na]+, with the glycan composition the paper assigned to each:

| Fraction | Observed m/z | Composition |
| --- | --- | --- |
| 6 | 1415.59 | Hex3HexNAc2Fuc1 |
| 11 | 1547.63 | Hex3HexNAc2Fuc1Xyl1 |
| 25 | 1842.63 | Hex6HexNAc2 |
| 27 | 2004.70 | Hex7HexNAc2 |

Standard monosaccharide residue masses (the mass a sugar adds once it is linked into a glycan, after losing water): hexose (Hex) 162.0528 Da, N-acetylhexosamine (HexNAc) 203.0794 Da, fucose/deoxyhexose (Fuc) 146.0579 Da, xylose (Xyl) 132.0423 Da.

**Task.**

1. Subtract fraction 6's mass from fraction 11's mass. Which residue mass from the table above does that difference match, and does that agree with the two compositions given?
2. Subtract fraction 25's mass from fraction 27's mass. Which residue does that match?
3. Across the 28 fractions this paper reported in total (not all shown here), the authors found that 86.1% of HRP's N-glycans were both fucosylated and xylosylated. Why would a plant glycoprotein commonly carry xylose, when the glycosylation examples elsewhere in this guide (tied to human or mammalian systems) never mention it?
4. If you only had the fraction 11 mass (1547.63) and no composition label, could you have worked out "Hex3HexNAc2Fuc1Xyl1" from the mass alone? What else would you need?

### Answers

1. 1547.63 - 1415.59 = 132.04, which matches the xylose residue mass (132.0423 Da) almost exactly. This agrees with the compositions given: fraction 11 has exactly one more xylose (Xyl1) than fraction 6, and nothing else differs between them.
2. 2004.70 - 1842.63 = 162.07, which matches the hexose residue mass (162.0528 Da). This agrees with the compositions: fraction 27 (Hex7HexNAc2) has exactly one more hexose than fraction 25 (Hex6HexNAc2).
3. Xylose on N-glycans (beta1,2-xylosylation) is a modification typical of plant and invertebrate glycoproteins, not of mammalian glycosylation pathways, which is why none of this guide's other glycosylation discussion, grounded in mammalian or bacterial systems, mentions it; horseradish peroxidase, as a plant enzyme, is exactly the kind of source where it shows up.
4. Not uniquely. A single mass can usually be explained by more than one combination of residues (for example, a different mix of hexose, HexNAc, fucose and xylose counts could sum to a very similar mass), so composition is normally assigned using a mix of the measured mass, knowledge of the organism's typical glycan patterns, and sometimes additional fragmentation (MS/MS) data, not from the intact mass in isolation.

## Scenario 4: Localizing a phosphorylation site from a fragment ladder

**Source.** Jagannadham MV, Nagaraj R, "Detecting the Site of Phosphorylation in Phosphopeptides Without Loss of Phosphate Group Using MALDI TOF Mass Spectrometry," *Analytical Chemistry Insights*, 2008, 3:21-29, using an Applied Biosystems 4800 MALDI-TOF/TOF. The peptide is a synthetic 8-residue construct derived from caveolin-1, Ac-EGTHSFDG-amide, with a phosphoserine form ("E8Gp") made for comparison against the unmodified form ("E8G").

**The data you are given.** Precursor (MH+) masses: E8G (unmodified) observed at m/z 890.37; E8Gp (phosphorylated) observed at m/z 970.33. For E8Gp, a set of MS/MS fragment ions was reported, each alongside its "minus 98" counterpart (the loss of H3PO4, 98 Da, a classic sign of a phosphate group leaving during fragmentation):

| Ion | Mass (with phosphate) | Mass (-98, phosphate lost) |
| --- | --- | --- |
| b5 | 634.13 | 536.18 |
| b6 | 781.18 | 683.23 |
| b7 | 896.19 | 798.24 |
| y4 | 641.16 | 543.20 |
| y5 (contains pS) | 504.14 | 406.15 |

**Task.**

1. Calculate the mass shift between E8G and E8Gp. Does it match the +80 Da (HPO3) addition this guide's PTM tab describes for phosphorylation?
2. The peptide sequence is EGTHSFDG, with the phosphate on the serine (S, position 5 counting from the N-terminus). The b-ion series (b5, b6, b7) all show a "-98" counterpart. What does that tell you about where the phosphate sits relative to b5?
3. Using the y-ion series, y5 (which, counting from the C-terminus, includes the phosphoserine) shows a "-98" loss, but would you expect y4 (one residue shorter, not reaching the phosphoserine) to show the same loss? Check against the table.
4. Put the b-ion and y-ion evidence together. Which single residue do both series point to as carrying the phosphate?

### Answers

1. 970.33 - 890.37 = 79.96, which rounds to 80 Da, matching the +80 Da (HPO3) mass addition this guide's PTM tab describes for phosphorylation.
2. Because b5, b6 and b7 all carry the phosphate and can all lose it (each shows a "-98" counterpart), the phosphate must sit at or before position 5 from the N-terminus, since every one of those longer fragments still contains it.
3. The table shows y4 does have a "-98" counterpart (543.20) alongside its full mass (641.16), and y5 also shows a "-98" counterpart (406.15) alongside 504.14 (contains pS). Both the fragments spanning the phosphoserine lose 98 Da, which is expected; a fragment that did not reach the phosphoserine at all would show no such pair.
4. Both series agree on position 5 (serine) counting from the N-terminus, which is also the fifth residue from the start of EGTHSFDG: the S in EGTH-S-FDG. The b-ion series localizes it between b4 (not given, would lack the phosphate) and b5 (has it), and the y-ion series confirms the same residue from the other end, which is exactly the kind of two-sided confirmation the PMF case-study tab describes for localizing a modification from a fragment ladder.

## Scenario 5: Reading a Biotyper confidence score

**Source.** Neville SA, LeCordier A, Ziochos H, Chater MJ, Gosbell IB, Maley MW, van Hal SJ, "Utility of Matrix-Assisted Laser Desorption Ionization-Time of Flight Mass Spectrometry following Introduction for Routine Laboratory Bacterial Identification," *Journal of Clinical Microbiology*, 2011, 49(8):2980-2984, a routine clinical-laboratory validation of the Bruker Biotyper covering 2,781 bacterial identifications.

**The data you are given.** The paper's own score bands: a score of 2.0 or above means a reliable species-level identification; 1.7 to 1.9 means a reliable genus-level identification (the paper notes all 330 tests in this band were, in fact, correct to species level when checked); and the paper's table footnote gives 1.7 or below as unreliable (a small inconsistency with the body text, which says "below 1.7"). Real results from the study:

| Organism | Tests | Score >=2.0 | Score 1.7-1.9 | Unreliable |
| --- | --- | --- | --- | --- |
| Escherichia coli | 348 | 341 | 6 | 1 |
| Staphylococcus aureus | 438 | 411 | 22 | 5 |
| Streptococcus pneumoniae | 75 | 61 | 12 | 2 |
| Salmonella Typhimurium | 60 | 0 | 60 | 0 |
| Streptococcus mitis group | 18 | misidentified, mostly as S. pneumoniae | | |
| Shigella sonnei | 12 | misidentified as Escherichia coli | | |

**Task.**

1. Every single Salmonella Typhimurium test (60 of 60) landed in the 1.7 to 1.9 band, none at 2.0 or above. Is that a failure of the method, given what the 1.7-1.9 band means?
2. All 12 Shigella sonnei isolates were identified by the Biotyper as Escherichia coli. Would a high confidence score (2.0+) on this misidentification be caught by the score alone? What would actually catch it?
3. Out of 2,781 total tests in the study, 48 (1.7%) scored below 1.7. Using this guide's "how to tell if a result is good" framing from the common-errors tab, is a 1.7% unreliable rate itself evidence that the method is unreliable overall?
4. If you measured an isolate at a score of 1.85, what would you report, and what would you NOT claim about it?

### Answers

1. Not necessarily. Salmonella is genetically very close across its serovars, so a method based on whole-cell protein mass patterns may reliably separate it from other genera (worth the 1.7-1.9 band) without reliably separating Typhimurium from other Salmonella serovars at the stricter 2.0+ species level; the paper reports this as expected biology, not as the method failing.
2. No, a high score alone would not catch it, because the mass-spectral protein pattern of Shigella sonnei and Escherichia coli is similar enough that the Biotyper confidently calls it E. coli regardless of score. This is exactly the kind of case where a result can be numerically confident yet biologically wrong, which is why the paper flags it as a case needing a confirmatory phenotypic or serological test rather than trusting the score in isolation.
3. No. A 1.7% rate of scores below the reliable thresholds, across 2,781 real clinical isolates, is consistent with a generally reliable method that still has edge cases; the common-errors tab's framing is that a result needing a second look is not automatically wrong, only unconfirmed, and this paper explicitly says 23 of the 48 unreliable results were later resolved to species level on repeat testing.
4. A score of 1.85 falls in the 1.7-1.9 band, so you would report a reliable genus-level identification. You would not claim species-level confidence from that score alone, even though this particular paper found that band to be correct to species level in every one of its 330 cases; the score itself only supports the genus-level claim.

## Scenario 6: Untangling a PEG-contaminated spectrum

**Source.** Lou X, van Dongen JLJ, Peeters JW, Janssen HM, "Disentangle a Complex MALDI-TOF Mass Spectrum of Polyethylene Glycols into Three Separate Spectra via Selective Formation of Protonated Ions and Sodium or Potassium Adducts," *Journal of the American Society for Mass Spectrometry*, 2022, 33(12):2333-2337, using a Bruker Autoflex Speed, CHCA matrix, reflector positive mode.

**The data you are given.** PEG and related polymers produce a regular repeating peak series with a spacing of 44 Da (the mass of one ethylene oxide, C2H4O, repeat unit). For one amino-terminated PEG oligomer, the paper reports three peaks for the same molecule: m/z 1409.9, 1431.9 and 1447.9, corresponding respectively to the protonated ion [M+H]+, the sodium adduct [M+Na]+, and the potassium adduct [M+K]+.

**Task.**

1. This guide's mechanism tab gives a hard contamination limit for PEG in a MALDI sample: 0.1% w/v. Using the 44 Da repeat spacing, how would you recognize PEG contamination in an unrelated sample's spectrum, even without knowing its exact concentration?
2. Calculate the mass difference between 1431.9 and 1409.9, and between 1447.9 and 1409.9. What do these two differences correspond to?
3. If you saw all three peaks (1409.9, 1431.9, 1447.9) in a spectrum and did not know about Na/K adducts, what mistake might you make about how many distinct molecules are present?
4. The paper's fix uses matrix chemistry, not instrument settings: CHCA with octadecylamine (ODA) favors protonation only, while CHCA with sodium or potassium trifluoroacetate (NaTFAc or KTFAc) favors a single, specific adduct. Why would changing the sample prep, rather than turning up laser power, be the right fix here?

### Answers

1. A series of peaks spaced exactly 44 Da apart, regardless of their absolute mass, is the signature of PEG's repeating ethylene oxide unit; spotting that regular spacing anywhere in a spectrum is a strong clue of PEG contamination even before checking concentration.
2. 1431.9 - 1409.9 = 22.0 Da, matching the mass added by a sodium adduct replacing a proton. 1447.9 - 1409.9 = 38.0 Da, matching the mass added by a potassium adduct replacing a proton. (Both values are differences between the paper's own reported peak masses, not numbers stated directly in the source.)
3. Without recognizing the Na/K adduct pattern, someone might mistake these three peaks for three different molecules of similar but distinct mass, when they are in fact the same molecule carrying a proton, a sodium ion, or a potassium ion.
4. Laser power affects how much energy goes into desorbing and ionizing the sample overall (as the mechanism tab explains for mass discrimination), but it does not control which cation a molecule picks up during ionization; that choice is driven by what is chemically available to bind, which is why changing the matrix or adding a specific salt additive, not the laser, is what selects for one adduct type over another.

## Scenario 7: Checking an LC-MALDI fraction pipeline against its own numbers

**Source.** Vitorino R, Guedes S, Tomer K, Domingues P, Duarte J, Amado F, "On-plate digestion using a commercial micro-fraction collector for nano-HPLC MALDI-TOF/TOF protein analysis," *Analytical Biochemistry*, 2008, 380(1):128-130, analyzing the human acquired enamel pellicle (a salivary protein film on tooth surfaces).

**The data you are given.** A commercial nano-fraction collector deposited LC eluate directly onto the MALDI target: 156 fractions collected per run, at 20-second intervals, 100 nL per fraction. The LC gradient ran 5% to 50% buffer B over 35 minutes, then 50% to 85% B over 5 minutes, then held at 85% B for 5 minutes; fraction collection started 5 minutes into the run. On-plate digestion identified 12 salivary proteins from more than 100 distinct tryptic peptides, compared with 11 proteins from standard in-solution digestion of the same sample; on-plate digestion added 40 extra peptides and 2 extra proteins (MMP-20 and cystatin S) that the standard method missed.

**Task.**

1. Using 156 fractions at 20-second intervals, how much total run time does fraction collection span? Does that roughly match the stated gradient length?
2. The gradient is 35 + 5 + 5 = 45 minutes long, and fraction collection "started 5 min into the run." Reconcile this with your answer to question 1.
3. On-plate digestion found 2 more proteins and 40 more peptides than standard in-solution digestion of the same sample. Based on what this guide's LC-MALDI tab says about why this coupling is used, suggest one reason on-plate digestion might catch peptides that in-solution digestion misses.
4. If you were assigned one MALDI spot from this run and told it corresponded to minute 20 of the gradient, roughly what fraction number would that be, given fractions are collected at a constant 20-second interval starting at minute 5?

### Answers

1. 156 fractions x 20 seconds = 3,120 seconds, which is 52 minutes. That is close to, though a little longer than, the 45-minute gradient length, which fits fraction collection continuing briefly past the gradient's end (for example during the final hold or column wash) rather than stopping the instant the gradient itself ends.
2. If collection starts at minute 5 and runs for the roughly 52 minutes calculated above, it would extend to about minute 57, which is beyond the 45-minute gradient; this is consistent with collection continuing through the 85% B hold and reequilibration period that typically follows a gradient like this, which the paper's total run description allows for even though it is not spelled out minute-by-minute.
3. The LC-MALDI tab notes that this coupling lets a complex sample be separated before each simpler fraction is analyzed; on-plate digestion adds the trypsin directly into each already-separated micro-fraction, so proteins or peptides that might be lost to the tube walls, or diluted below detection, during a separate in-solution digestion and cleanup step have less handling and less opportunity to be lost, which plausibly explains the extra peptides and proteins recovered.
4. Collection starts at minute 5, so minute 20 is 15 minutes (900 seconds) into collection. At one fraction every 20 seconds, that is roughly the 45th fraction (900 / 20 = 45) after collection began, so approximately fraction 45.

## Scenario 8: Locating a protease cut site in an intact protein from mass balance alone

**Source.** Liu Z, Zhu H, Fang GG, Walsh K, Mwamburi M, Wolozin B, Abdul-Hay SO, Ikezu T, Leissring MA, Qiu WQ, "Characterization of Insulin Degrading Enzyme and Other Amyloid-beta Degrading Proteases in Human Serum: A Role in Alzheimer's Disease?", *Journal of Alzheimer's Disease*, 2012, 29(2):329-340, measuring synthetic human amyloid-beta peptide by MALDI-TOF before and after treatment with insulin-degrading enzyme (IDE), a serum protease.

**The data you are given.** The intact synthetic peptide Abeta(1-40) (40 residues) was measured at a calculated mass of 4327.2 Da and an observed mass of 4328.4 Da (a doubly charged ion was also observed at m/2z 2164.5, calculated 2163.6). After treatment with IDE, the paper reports: "The m/z ratio of this peak corresponds to Abeta(1-14), indicating cleavage between amino acids 14 and 15." The two resulting fragments were measured at: Abeta(1-14), calculated 1697.7 Da, observed 1697.1 Da; and Abeta(15-40), calculated 2647.4 Da, observed 2646.8 Da.

**Task.**

1. Add the two observed fragment masses together, then add 18 Da (one water molecule) to the observed intact mass. How close are these two totals, and what does that closeness tell you about whether Abeta(1-14) and Abeta(15-40) are truly two complementary pieces of one single cleavage of the same intact peptide, rather than two unrelated or partly missing fragments?
2. Why must one water molecule (18 Da) be added to the intact mass before comparing it to the fragment sum, rather than comparing the fragment sum directly to the intact mass with no correction?
3. The intact peptide was also observed as a doubly charged ion at m/2z 2164.5. For a doubly charged ion, m/z is approximately (M + 2) / 2, where M is the singly charged mass and the 2 accounts for the two added protons at about 1 Da each. Using this, estimate M from 2164.5, and check whether it is consistent with the reported calculated intact mass of 4327.2 Da.
4. If IDE had instead cut Abeta between two different residues further along the chain, would you still expect the two resulting fragment masses to add up to about 4346.4 Da (the intact mass plus water)? Why or why not?

### Answers

1. 1697.1 + 2646.8 = 4343.9 Da. The intact mass plus one water is 4328.4 + 18 = 4346.4 Da. The two totals differ by only about 2.5 Da, roughly 0.06% of the intact mass, which is well within typical MALDI-TOF linear-mode accuracy for peptides this size. That closeness confirms Abeta(1-14) and Abeta(15-40) really are two complementary pieces of a single clean cleavage of the same intact peptide.
2. Hydrolysis, the reaction that breaks a peptide bond, adds one water molecule across the cut: each new fragment end gains an atom that was shared as part of a single peptide bond in the intact chain, so the two fragment masses together are always about 18 Da heavier than the intact peptide alone. Skipping this correction would make a genuine, clean cut look like it was off by 18 Da when it was not.
3. M is approximately 2 x 2164.5 - 2 = 4327.0 Da. This is close to the reported calculated intact mass of 4327.2 Da (within about 0.2 Da), and within about 1.4 Da of the reported observed mass of 4328.4 Da, confirming the doubly charged peak is the same intact peptide carrying two protons rather than a different species.
4. Yes. The fragment-sum-plus-water relationship holds regardless of where along the chain the single cut falls, because it reflects the conservation of mass across one hydrolysis reaction, not the specific residues on either side of the cut. Moving the cut site would change how the total mass is split between the two fragments, but not the total itself.

## Scenario 9: Reading a top-down fragmentation spectrum of a whole intact protein ion

**Source.** Liu Z, Schey KL, "Fragmentation of Multiply-Charged Intact Protein Ions Using MALDI TOF-TOF Mass Spectrometry," *Journal of the American Society for Mass Spectrometry*, 2007, 19(2):231-238, fragmenting intact bovine ubiquitin ions directly (not a tryptic digest) by collision-induced dissociation (CID) on an Applied Biosystems 4700 MALDI TOF/TOF.

**The data you are given.** Bovine ubiquitin is a 76-residue protein, intact mass about 8.6 kDa. CID of the doubly charged intact precursor ion (1 keV collision energy, air collision gas) produced a b32 ion at m/z 3573.3, with its complementary y-ion reported explicitly by the paper as y44. A doubly charged y58 ion cluster was also observed, at an apparent m/z of 3265.7. The paper reports that cleavage occurred preferentially on the C-terminal side of acidic residues (aspartate and glutamate) in the ubiquitin sequence, rather than at random positions along the backbone.

**Task.**

1. A b32 ion means the backbone broke between residue 32 and residue 33, counting from the N-terminus. Ubiquitin has 76 residues total. What length should the complementary C-terminal fragment be, and does that match the y44 ion the paper reports?
2. Why would CID preferentially break the backbone on the C-terminal side of an acidic (Asp or Glu) residue, rather than at a random bond along the chain?
3. This is top-down fragmentation of the whole intact protein ion. What is the key practical difference between this approach and the PMF workflow this guide's case-study tab describes, in terms of what actually goes into the mass spectrometer?
4. The y58 cluster is reported as a doubly charged ion near m/z 3265.7. Using m/z is approximately (M + z) / z for z protons at about 1 Da each, estimate the underlying mass M, then estimate roughly where a singly charged version of the same ion (z=1) would be expected to appear.

### Answers

1. The complementary C-terminal fragment should contain 76 - 32 = 44 residues, exactly matching the y44 ion the paper reports as the complementary partner to b32.
2. The side chain of an acidic residue carries a carboxylic acid group that can participate directly in breaking the adjacent backbone bond during collisional activation, which stabilizes the fragment ions formed at that position; this is consistent with the paper's own observation that cleavage occurred preferentially on the C-terminal side of Asp and Glu residues rather than at random positions.
3. In the PMF workflow, trypsin first cuts the protein into many small peptides in solution, and the mass spectrometer measures that mixture of pre-digested fragments. In top-down fragmentation, the whole intact protein ion goes into the mass spectrometer essentially as is, and the instrument's own collision cell breaks it apart, so the sequence information comes directly from fragmenting the intact ion rather than from a pre-digested peptide mixture.
4. For z=2, M is approximately 2 x 3265.7 - 2 = 6529.4 Da. For the same mass at z=1, m/z is approximately M + 1, so a singly charged version of this ion would be expected to appear near m/z 6530, roughly double the doubly charged value, as expected when the charge state is halved for the same ion mass.

## Scenario 10: Mapping an O-GlcNAc site on a transcription factor, and its reciprocal phosphate

**Why this fits.** O-GlcNAcylation (a single N-acetylglucosamine sugar attached directly to a serine or threonine, written O-GlcNAc) is one of the hardest real post-translational modifications to find. It sits at low stoichiometry, often falls off during ionization or fragmentation before it can be measured, and has no fixed consensus sequence an antibody or a gene search can rely on. A direct mass-shift measurement, exactly the kind of arithmetic used for the amyloid-beta and ubiquitin scenarios above, is one of the few ways to catch it directly and pin it to one residue. O-GlcNAc also tends to sit on, or right next to, the same serines and threonines that kinases phosphorylate, so it shows up again and again on the two protein families this scenario focuses on: kinases and transcription factors, where it can compete with phosphorylation for the same regulatory site, an idea often called the Yin-Yang hypothesis.

**Source.** Chalkley RJ, Burlingame AL, "Identification of novel sites of O-GlcNAc modification of serum response factor using quadrupole time-of-flight mass spectrometry," *Molecular & Cellular Proteomics*, 2003, 2(3):182-190, studying serum response factor (SRF), a transcription factor that binds the serum response element (the CArG box) and switches on genes such as c-fos. A limit stated up front: the paper's main sequencing instrument is a Q-TOF, not a MALDI-TOF/TOF. MALDI-TOF (a Bruker Reflex III, DHB matrix) plays a real but smaller role here, screening HPLC fractions of the digest for a telltale GlcNAc signal before the flagged fractions go on to Q-TOF CID MS/MS for sequencing. This is itself a common, honest division of labor in a real proteomics lab, and worth seeing even though MALDI is not the instrument that does the final sequencing in this particular paper.

**Aim and research question.** The paper's own stated aim is to find where, specifically, O-GlcNAc sits on SRF. Pinpointing the exact modified residues is the necessary first step before anyone can test what that modification does to SRF's activity as a transcription factor; this paper is a site-mapping study, not a functional one, and it is worth being clear about that distinction rather than assuming the sites found here have already been shown to change SRF's behavior.

**Workflow.**

1. Purified SRF is reduced, alkylated, and run on SDS-PAGE.
2. The protein band is digested in-gel, separately with trypsin and with chymotrypsin, giving two different sets of peptides covering overlapping parts of the sequence.
3. Each digest is separated by HPLC into many fractions.
4. Every fraction is screened by MALDI-TOF for a sugar-specific signal (the same kind of oxonium-ion signature this guide's glycopeptide tab introduces for N-linked sugars); flagged fractions are the candidates most likely to carry an O-GlcNAc-modified peptide.
5. Flagged fractions go on to nanoLC-ESI-Q-TOF CID MS/MS, which sequences the peptide and localizes the exact modified residue from the fragment ion ladder.

<figure class="fig"><div class="fig-svg"><svg viewBox="0 0 320 540" xmlns="http://www.w3.org/2000/svg" role="img" aria-labelledby="figo1title">
<title id="figo1title">Workflow for mapping an O-GlcNAc site on the transcription factor SRF</title>
<defs>
<marker id="arrowo1" viewBox="0 0 10 10" refX="5" refY="5" markerWidth="6" markerHeight="6" orient="auto-start-reverse">
<path d="M0,0 L10,5 L0,10 z" fill="#4a7c7c"/>
</marker>
</defs>
<rect x="0" y="0" width="320" height="540" fill="none"/>
<rect x="20" y="20" width="280" height="60" rx="8" fill="#eef3f3" stroke="#2b3a42" stroke-width="1.5"/>
<text x="160" y="44" text-anchor="middle" font-size="13" fill="#2b3a42" font-weight="bold">SRF (transcription factor)</text>
<text x="160" y="62" text-anchor="middle" font-size="12" fill="#2b3a42">purified protein, reduced and alkylated</text>
<line x1="160" y1="80" x2="160" y2="98" stroke="#4a7c7c" stroke-width="2" marker-end="url(#arrowo1)"/>
<rect x="20" y="100" width="280" height="60" rx="8" fill="#eef3f3" stroke="#2b3a42" stroke-width="1.5"/>
<text x="160" y="124" text-anchor="middle" font-size="13" fill="#2b3a42" font-weight="bold">In-gel digestion</text>
<text x="160" y="142" text-anchor="middle" font-size="12" fill="#2b3a42">trypsin or chymotrypsin, separately</text>
<line x1="160" y1="160" x2="160" y2="178" stroke="#4a7c7c" stroke-width="2" marker-end="url(#arrowo1)"/>
<rect x="20" y="180" width="280" height="60" rx="8" fill="#eef3f3" stroke="#2b3a42" stroke-width="1.5"/>
<text x="160" y="204" text-anchor="middle" font-size="13" fill="#2b3a42" font-weight="bold">HPLC fractionation</text>
<text x="160" y="222" text-anchor="middle" font-size="12" fill="#2b3a42">spreads the digest into many fractions</text>
<line x1="160" y1="240" x2="160" y2="258" stroke="#4a7c7c" stroke-width="2" marker-end="url(#arrowo1)"/>
<rect x="20" y="260" width="280" height="60" rx="8" fill="#eef3f3" stroke="#2b3a42" stroke-width="1.5"/>
<text x="160" y="284" text-anchor="middle" font-size="13" fill="#2b3a42" font-weight="bold">MALDI-TOF screening</text>
<text x="160" y="302" text-anchor="middle" font-size="12" fill="#2b3a42">flags fractions carrying a GlcNAc signature</text>
<line x1="160" y1="320" x2="160" y2="338" stroke="#4a7c7c" stroke-width="2" marker-end="url(#arrowo1)"/>
<rect x="20" y="340" width="280" height="60" rx="8" fill="#eef3f3" stroke="#2b3a42" stroke-width="1.5"/>
<text x="160" y="364" text-anchor="middle" font-size="13" fill="#2b3a42" font-weight="bold">Q-TOF CID MS/MS</text>
<text x="160" y="382" text-anchor="middle" font-size="12" fill="#2b3a42">sequences the flagged, modified peptide</text>
<line x1="160" y1="400" x2="160" y2="418" stroke="#c45b39" stroke-width="2" marker-end="url(#arrowo1)"/>
<rect x="20" y="420" width="280" height="100" rx="8" fill="#eef3f3" stroke="#c45b39" stroke-width="1.5"/>
<text x="160" y="444" text-anchor="middle" font-size="13" fill="#2b3a42" font-weight="bold">Site located</text>
<text x="160" y="462" text-anchor="middle" font-size="12" fill="#2b3a42">O-GlcNAc at Ser-313</text>
<text x="160" y="480" text-anchor="middle" font-size="12" fill="#2b3a42">phosphate at Ser-224, a separate serine</text>
<text x="160" y="500" text-anchor="middle" font-size="11" fill="#5c6e72">(same protein, two regulatory sites)</text>
</svg></div><figcaption><span class="sr-only">A vertical flow diagram showing six steps: purified SRF protein, in-gel digestion with trypsin or chymotrypsin, HPLC fractionation, MALDI-TOF screening for a GlcNAc signature, Q-TOF CID MS/MS sequencing of the flagged peptide, and finally the two located sites, O-GlcNAc at serine 313 and phosphate at serine 224.</span><span class="cap">The real workflow used to map SRF's O-GlcNAc and phosphorylation sites, based on Chalkley and Burlingame, Molecular &amp; Cellular Proteomics, 2003. MALDI-TOF here plays a screening role, flagging candidate fractions before a separate Q-TOF instrument sequences them.</span></figcaption></figure>

**The data you are given.**

A chymotryptic peptide spanning residues 396 to 417 of SRF was observed, by MALDI, in both an unmodified and a GlcNAc-modified form, each appearing at several methionine-oxidation states (methionine side chains pick up an extra oxygen during handling, adding about 16 Da each time, independently of the GlcNAc question). The source's own figure caption labels these as "m/z" values, but, as the task below asks you to check, the numbers only make sense as fully charge-deconvoluted masses.

| Met-oxidation state | Unmodified mass (Da) | GlcNAc-modified mass (Da) |
| --- | --- | --- |
| 0 | 2350.24 | 2553.45 |
| 1 | 2366.20 | 2569.38 |
| 2 | 2382.20 | 2585.42 |
| 3 | 2398.13 | not observed |

A separate peptide, spanning residues 213 to 235, was sequenced by CID in both an unmodified form and a form carrying a phosphate group on Ser-224 (a different serine from the O-GlcNAc site above). The precursor ions were both reported as triply charged, and two of the resulting fragment ions, y11 and y12, are given below exactly as reported, with no charge state stated in the source for these two ions.

| Fragment ion | Covers residues | Unmodified m/z | Phosphorylated m/z |
| --- | --- | --- | --- |
| Precursor [M+3H]3+ | 213-235 (23 residues) | 861.77 | 888.39 |
| y11 | 225-235 (11 residues) | 635.35 | 635.35 |
| y12 | 224-235 (12 residues) | 678.88 | 718.84 |

**Interpretation.** Three distinct scales of analysis now sit side by side in this guide: identifying a whole protein from its digest fragments (Scenario 1), reconciling an intact protein's mass against proteolytic fragments (Scenario 8), fragmenting a whole intact protein ion directly (Scenario 9), and now mapping a single, small chemical modification onto one residue of a peptide from a much larger protein (this scenario). The underlying skill is the same throughout: a mass difference, worked out carefully and checked against what it should mean, is what turns a number on a spectrum into a biological fact. Here, that fact is that SRF carries O-GlcNAc at Ser-313 and a phosphate at Ser-224, two different serines on the same transcription factor, which is exactly the pattern researchers look for when asking whether the two modifications compete for influence over the same regulatory protein.

**Task.**

1. Using the first table, compute the mass difference between the unmodified and GlcNAc-modified mass at each methionine-oxidation level. Do all three differences point to the same modification, and how does its size compare with the HexNAc mass gap this guide's glycopeptide tab already introduced?
2. The unmodified series in the first table rises by about 16 Da at each successive oxidation state. What does a 16 Da addition on a methionine residue correspond to, and why would you expect to see it in almost any real peptide sample rather than something unique to SRF?
3. The source's own figure caption calls the first table's numbers "m/z," yet the 16 Da and 203 Da differences only make sense as fully charge-deconvoluted masses, not as raw triply-charged m/z values (dividing either gap by 3 would not match any real modification). What does this tell you about trusting a label on a spectrum or figure without checking the numbers it reports against known mass increments?
4. Using the second table's precursor row, convert both m/z values to neutral monoisotopic mass with M = z x m/z - z x 1.007, for z = 3. What is the mass difference between the two forms, and which modification does it match?
5. The second table's y11 ion is identical, at m/z 635.35, in both the unmodified and phosphorylated spectra, but y12 is not. Given that y11 covers only the last 11 residues (225 to 235) and y12 covers the last 12 (224 to 235), what does this tell you about where the modification must sit?
6. Try computing y12 minus y11 for each spectrum assuming these are singly charged ions. Does either result match a real amino acid residue mass? Now multiply each difference by 2 instead, as if the ions were doubly charged. Do the results now match known residue masses, and if so, which ones?
7. SRF's O-GlcNAc site (Ser-313) and its phosphorylation site (Ser-224) are two different serines on the same transcription factor. Given that phosphate and O-GlcNAc often compete for the same hydroxyl groups across a protein (the Yin-Yang hypothesis), why would mapping both modifications on the same molecule be more informative than studying either one in isolation?

### Answers

1. 2553.45 - 2350.24 = 203.21 Da; 2569.38 - 2366.20 = 203.18 Da; 2585.42 - 2382.20 = 203.22 Da. All three cluster tightly around 203.2 Da, matching the HexNAc mass gap already introduced in the glycopeptide tab (there, 203 Da marked a hexose-N-acetylglucosamine unit within a larger N-linked glycan; here, the same unit sits on its own, directly on the peptide, as O-GlcNAc).
2. A 16 Da addition corresponds to one extra oxygen atom, the signature of methionine oxidizing to methionine sulfoxide. This is a routine, spontaneous artifact of sample handling and storage for any methionine-containing peptide, which is exactly why this guide's case-study tab treats Oxidation (M) as a standard variable modification in a MASCOT search rather than something specific to one protein.
3. It shows that a figure caption's own label is not automatically trustworthy: here, the stated "m/z" values only behave like fully charge-deconvoluted masses (a 203 Da gap, not a roughly 68 Da gap that dividing by 3 would give), so the source itself mislabels these numbers. Checking a label against the arithmetic the numbers actually support, rather than accepting it at face value, is the same lesson this guide's troubleshooting tab teaches about judging a result by its numbers, not by a readout alone.
4. M = 3 x 861.77 - 3 x 1.007 = 2582.29 Da for the unmodified form; M = 3 x 888.39 - 3 x 1.007 = 2662.15 Da for the phosphorylated form. The difference is 2662.15 - 2582.29 = 79.86 Da, matching the mass of a phosphate group, the same roughly 80 Da shift used for phosphorylation elsewhere in this guide.
5. Because y11 covers only residues 225 to 235 and is identical in both spectra, the modification cannot sit anywhere in those 11 residues. It must sit in the one additional residue y12 adds beyond y11, which is residue 224, matching the paper's own identification of Ser-224 as the phosphorylation site.
6. At charge 1+: 678.88 - 635.35 = 43.53 Da for the unmodified pair, and 718.84 - 635.35 = 83.49 Da for the phosphorylated pair. Neither matches a real amino acid residue (the smallest, glycine, is about 57 Da), so these cannot be singly charged ions. Doubling each difference instead gives 43.53 x 2 = 87.06 Da for the unmodified pair, matching serine's residue mass (about 87.03 Da) closely, and 83.49 x 2 = 166.98 Da for the phosphorylated pair, matching a phosphorylated serine residue (serine's 87.03 Da plus a phosphate group's roughly 80 Da, about 167.0 Da) closely. Both results only make sense at charge 2+, so y11 and y12 here must be doubly charged fragment ions.
7. Because the two modifications can occupy the same kind of hydroxyl group and may substitute for one another at a given site, seeing both on the same molecule, even at different serines, lets researchers ask whether gaining or losing one modification anywhere on the protein shifts the balance toward or away from the other elsewhere, a question that studying either modification alone on a different sample could never answer.

## What to take forward

Real data rarely arrives as clean as a textbook table: it has missed cleavages, gaps in a fragment ladder, a matrix the authors forgot to name, or a score that needs a second test to confirm. Working through these ten scenarios is practice for exactly that: using the same reasoning this guide's other sixteen tabs teach, on numbers you did not generate yourself, whether that data comes from digested peptides, whole intact protein ions, or a single modified residue buried in a much larger protein.

## Glossary terms introduced

- Expect value: the statistic a MASCOT search reports alongside its score, estimating how likely a match this good would occur by chance; a very small Expect value (such as 1.7 x 10^-6) indicates high confidence even when sequence coverage is modest.
- Residue mass: the mass a monosaccharide or amino acid adds once it is linked into a chain, after the water lost during bond formation; used to work out composition from a mass difference.
- Pseudo-precursor ion: a fragment ion (such as one c-ion from an ISD ladder) used as if it were its own precursor mass for a database search, rather than searching the intact protein's full mass.
- Score band: a range of confidence scores (such as the Biotyper's 2.0+, 1.7-1.9, and below-1.7 bands) that the software or the analyst uses to decide how much to trust an identification.
- Mass balance check: adding a set of fragment masses together, correcting for the water gained or lost during the reaction that produced them, and comparing the result to the original intact mass to confirm the fragments really came from that one molecule.
- Top-down fragmentation: breaking apart a whole intact protein ion directly inside the mass spectrometer, instead of digesting the protein into peptides first; contrasted with the bottom-up PMF workflow used elsewhere in this guide.
- Complementary ion pair: two fragment ions (such as a b-ion and a y-ion) produced from the same single backbone cleavage, whose residue counts or masses together account for the whole precursor ion.
- O-GlcNAc (O-GlcNAcylation): a single N-acetylglucosamine sugar attached directly to a serine or threonine side chain, adding about 203 Da, the same HexNAc mass gap used for N-linked glycans elsewhere in this guide.
- Yin-Yang hypothesis: the idea that phosphorylation and O-GlcNAcylation often compete for the same serine or threonine hydroxyl groups across a protein, so gaining one modification can mean losing the other at a nearby or the same site.
