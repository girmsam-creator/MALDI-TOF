# Test Your Knowledge

## Purpose

This is the last tab: twenty-four questions covering the whole guide, most of them grounded in the real workflow this lab's Bruker UltrafleXtreme MALDI-TOF/TOF actually runs, plus a few general-knowledge questions for variety. Use it as a self-check across every earlier tab. Try answering each question from memory first, then check the answer key at the end. No peeking early.

## Questions

### Section A: Fundamentals, instrument, and sample prep

1. What do the four letters in "MALDI" stand for?
2. Why is near-neighbour calibration recommended, and why does it matter even more on an AnchorChip plate than on a normal ground steel plate?
3. True or false: a LIFT (MS/MS) method should be recalibrated before every sample run, just like a normal MS method.
4. Name three matrices used for ISD (top-down sequencing of intact proteins). Why is 2,5-DHAP, despite being a good general protein matrix, not one of them?
5. Why must salts, buffers, and detergents be removed from a sample before it goes anywhere near the MALDI target plate? Give one real tolerance number.
6. When loading the target plate and frame into the instrument, which corners go in first, and which way do the sample spots face?
7. What does the flexControl method name "RP 700-3500" tell you about that method?

### Section B: Protein identification, reading spectra, and glycopeptides

8. Your automated PMF search at the default 0.1 Da tolerance comes back with no significant hit. What should you check, and in what order, before concluding the protein just isn't identifiable?
9. A peak shows up at m/z 842 in almost every tryptic digest you run. What is it, and what should you do with it?
10. In flexAnalysis, when would you choose Centroid peak picking instead of Snap, and why?
11. Your flexAnalysis calibration comes back with an error of 12 ppm on a peptide calibrant. What should you do before trusting the spectrum?
12. Why can't a glycopeptide be searched with a simple fixed mass offset the way a phosphopeptide can?
13. Name the two real oxonium ions and the three real diagnostic mass distances that ProteinScape's Classification step looks for in a glycopeptide MS/MS spectrum.
14. Why is reflector mode the wrong choice for an acidic, sialylated glycopeptide, and what should you use instead?
15. In GlycoQuest's scoring, what do Fragmentation Coverage and Intensity Coverage each tell you, and why might a match with high Fragmentation Coverage but low Intensity Coverage still deserve a second look?

### Section C: PTMs, intact proteins, pipelines, and data analysis

16. Roughly how many Daltons does a single phosphorylation add to a peptide's mass?
17. In the real FQSEEQQQTEDELQDK example, what is the unmodified peptide's MH+, and what is the phosphorylated form's MH+?
18. What is ISD, and which matrices are recommended for it in this lab?
19. An ISD spectrum of an intact protein shows two separate ion ladders. What do they represent, and which end of the protein does each one read from?
20. What problem does LC-MALDI (with WARP-LC) solve that a direct MALDI measurement of a complex peptide mixture cannot?
21. True or false: a laser power that's too low produces a spectrum with poor baseline separation between isotope peaks.
22. In R's MALDIquant workflow, what does `alignSpectra()` correct for, and why is that necessary before comparing multiple samples?
23. Which Python function would you reach for to detect peaks in an already-smoothed spectrum array?
24. In the time-of-flight equation, which ions reach the detector first: heavy singly-charged ions, or light singly-charged ones?

## Answers

1. **M**atrix-**A**ssisted **L**aser **D**esorption/**I**onization.
2. Near-neighbour calibration works because the closer a calibrant spot sits to the sample spot, the smaller the small plate and acceleration-plate distance differences that cause mass error. On an AnchorChip plate there is a dedicated calibration spot for every four sample spots, versus one shared calibrant spot in the middle of eight sample spots on a normal plate, so the calibration sits physically closer to each sample; that matters more on AnchorChip because its automatic, high-throughput runs rely on that accuracy without anyone checking each spectrum by eye.
3. **False.** LIFT (MS/MS) methods should not be recalibrated routinely; that calibration is considered stable, and recalibrating it takes a long time and needs very well-prepared samples. A normal MS method, by contrast, should be calibrated every time samples are measured.
4. SA (sinapinic acid), SDHB, and 1,5-DAN (which also promotes disulfide reduction, useful for sequencing disulfide-linked proteins). 2,5-DHAP is excluded because it actively prevents the fragmentation that ISD depends on, even though it's a good general matrix for intact proteins.
5. Salts, buffers, and detergents suppress or ruin the MALDI signal. Real example: PEG tolerance is only 0.1% w/v, and detergents such as SDS, CHAPS, and CHAPSO are flatly incompatible with MALDI. Desalt first, for example with C18 ZipTips.
6. Cut corners first, with the sample spots facing the longer side of the machine.
7. Reflector mode, positive ion mode, scanning a mass range of 700 to 3500 Da.
8. First check the calibration error on the calibrant spot (anything over 5 ppm means recalibrate before anything else); then check whether any of the "unidentified" peaks are trypsin autolysis peaks (these appear at m/z 842, 1045, and 2678) and exclude them; only then widen the search tolerance in steps, 0.1 to 0.5 to 1.0 Da; and finally check the taxonomy/database choice and confirm the protease really was trypsin.
9. A trypsin autolysis peak, from the digestion enzyme itself rather than the sample protein. Recognize it and exclude it from the peak list rather than treating it as a real sample peak.
10. Choose Centroid for larger molecules whose isotopic peaks can't be resolved (it gives the whole-peak average mass); choose Snap when the isotopic peaks are resolved, as with peptides, since it gives the more accurate monoisotopic mass.
11. 12 ppm exceeds the under-5-ppm acceptable error for peptides, so don't trust it: go back and repeat the calibration (check which calibrant peaks were assigned and reassign if needed) before reading any mass off that spectrum.
12. A phosphopeptide's modification is a single, fixed mass addition (+80 Da for one phosphate), so a database search can simply look for that one fixed offset. A glycopeptide's attached sugar chain varies hugely in mass from one spectrum to the next, even on the same peptide backbone, so there is no single fixed offset that works; instead, ProteinScape's Classification step looks for glycopeptide-specific fragment evidence rather than a fixed mass shift.
13. Oxonium ions at 204 and 366 Da; diagnostic mass distances of 162 Da (hexose), 203 Da (HexNAc), and 291 Da (sialic acid / NeuAc).
14. MALDI induces metastable decay of sialic acids in flight; reflector mode loses the sialic-acid-containing species to this decay, giving an incorrect, incomplete picture of the real glycan heterogeneity. Linear mode retains them and should be used instead, typically with 2,5-DHB or 2,5-DHAP as the matrix.
15. Fragmentation Coverage reflects how much of the theoretical fragment pattern for the proposed glycan actually showed up in the spectrum; Intensity Coverage reflects how much of the spectrum's real signal intensity that match accounts for. High Fragmentation Coverage with low Intensity Coverage means many of the right fragment types appeared, but most of the spectrum's real signal belongs to something else, so the match may be explaining only a small part of what's really there; it's worth checking the raw spectrum by eye rather than trusting one percentage alone.
16. About 80 Da per phosphorylated residue.
17. Unmodified MH+ 1981.8 Da; phosphorylated MH+ 2061.8 Da.
18. ISD (in-source decay) sequences an intact protein from both ends without digesting it first; sinapinic acid (SA) and SDHB are the matrices used for it in this lab (1,5-DAN can also be used specifically to promote disulfide reduction for ISD sequencing of disulfide-linked proteins).
19. They are fragment-ion ladders reading in from each end of the protein, one from the N-terminus and one from the C-terminus. Comparing each ladder's step-by-step masses against the known sequence can reveal terminal modifications, for example Cytochrome C's N-terminal acetyl group, or an IgG heavy chain's N-terminal pyroGlu and absent C-terminal lysine.
20. Analyzing a complex peptide mixture directly by MALDI causes ion suppression, where strong "winner" peaks drown out weaker "loser" peaks, and some peaks sit too close together to separate for MS/MS. LC-MALDI separates the mixture on a liquid chromatography column first and spots each fraction onto its own MALDI target position, decoupling the LC's fast timescale from MALDI's slower, unhurried measurement.
21. **False.** Too-low laser power shows up as high noise and a weak signal; it's too-high laser power that causes poor baseline separation between isotope peaks.
22. It corrects for small calibration and mass-drift differences between spectra collected in different runs, warping each spectrum's m/z scale onto a common reference so the same biological peak lines up at the same position across all samples, essential before comparing or binning peaks across samples.
23. `scipy.signal.find_peaks`.
24. Light singly-charged ions arrive first: lighter ions accelerate to a higher speed for the same kinetic energy, so they cover the flight tube faster.

## Closing remarks

This guide started with one idea, that flight time reveals mass, and built outward from there: sample prep and instrument setup, reading a spectrum, protein identification by PMF and MS/MS, TOF/TOF and intact-protein sequencing, glycopeptides, proteomics and PTMs, LC-MALDI and automated pipelines, other applications beyond this lab, alternative methods and future trends, and finally the worked examples, code, and references to put it into practice. Every later tab leaned on something explained earlier, so if any answer above felt shaky, the fastest fix is to revisit that specific earlier tab rather than reread the whole guide from the start.

Two honest reminders worth carrying forward. First, on this instrument the limiting factor is almost always calibration and contamination discipline, not the physics itself: when a result looks wrong, check the calibration error and think about what might have contaminated the sample before doubting the method. Second, real instrument documentation is sometimes messy or even contradictory between different sources. This guide's own research ran into a few examples: a calibration standard's stated peptide count not matching its own table, two different PCIS window figures quoted in two different lab documents, and generic Bruker test-instrument model names that aren't the Aalto UltrafleXtreme. Always sanity-check what a document says against the instrument itself and a knowledgeable colleague, rather than trusting any single document blindly.

The Cheat Sheet & Further Reading tab stays useful after this point as a quick lookup; this closing tab is for checking understanding, not for reference lookups.

## Glossary terms introduced

- **Autolysis peak:** a peak in a spectrum that comes from the digestion enzyme (here, trypsin) digesting itself, not from the sample protein; recognized by its fixed m/z values (842, 1045, 2678) and excluded from the real peak list.
- **Ion suppression:** when strong, abundant peaks in a mixed sample drown out the signal from weaker ones, making some components invisible unless the mixture is separated first.
