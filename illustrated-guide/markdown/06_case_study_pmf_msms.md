# Case Study: Protein Identification by PMF and MS/MS

## Purpose

This tab brings everything together into one real, complete task: starting from a digested protein on the target plate and ending with a confirmed identification. It is worked through using the actual automated and manual workflows this lab's Bruker UltrafleXtreme instrument runs, so you can see how calibration, measurement, and database searching combine into a real result, not just separate skills.

## Key ideas

### The real identification pipeline

Identifying a protein from a digest on this instrument uses two techniques in sequence: peptide mass fingerprinting (PMF), which matches a list of measured peptide masses against a protein database, followed by MS/MS confirmation, which measures the actual fragment sequence of a few chosen peptides to confirm the match. Both searches run through the MASCOT database, usually via a program called ProteinScape.

The real pipeline runs through four pieces of software, with flexControl and flexAnalysis each used twice:

1. flexControl measures MS spectra of the sample spots and the calibrant spots side by side.
2. flexAnalysis detects the peaks and calibrates the sample spectra using near-neighbour calibration (borrowing the calibration fit from the nearest calibrant spot).
3. The resulting peak list goes back to flexControl, which measures MS/MS spectra, using the LIFT cell, on a chosen set of peaks.
4. flexAnalysis detects the MS/MS peaks.
5. Both the MS and MS/MS peak lists are sent to ProteinScape, which hands them to the MASCOT database for the actual search.

### Running it automatically: ProteinScape and AutoXecute

The automated version of this pipeline starts in ProteinScape, not at the instrument itself. In condensed form:

1. In ProteinScape, create a new project and a new sample to hold your digest (a sample can hold one or several spectra).
2. Load the target plate in flexControl and shoot one spot manually first to check the method and laser power look right.
3. Shoot the calibration spot into the sum buffer and calibrate before going further.
4. In flexControl's AutoXecute tab, start the run wizard: pick the plate type, choose which spots to measure, and link the run to the matching ProteinScape sample. The number of plate spots and ProteinScape samples must match exactly, or automatic processing fails.
5. Pick or edit the AutoXecute and flexAnalysis methods for calibration, MS, and MS/MS (these methods carry the real shot counts and tolerances below).
6. In ProteinScape, configure Automatic MS searches, then Automatic MS/MS searches, with the chosen search parameters.
7. Click Start automatic run in flexControl. The instrument now runs the whole pipeline on its own.
8. Results land back in ProteinScape, with MASCOT hits appearing under the Proteins and Peptides tab, ready to inspect.

The automated run has real, concrete shot counts behind it:

- Calibration: roughly **1,500 satisfactory shots**.
- MS measurement: roughly **2,000 satisfactory shots**.
- MS/MS parent mode: **800 satisfactory shots**, collected in steps of 50 at a time.
- MS/MS fragment mode: **4,000 satisfactory shots**, collected in steps of 100 at a time.

Fragment mode needs far more shots than parent mode because the fragment signal is much weaker than the parent peak it came from, so more shots are needed to build a clean, readable fragment spectrum.

### Setting the tolerances

The PMF search's default mass tolerance is a strict **0.1 Da**, which only works if the calibration was excellent. If a search comes back with no hits, the usual fix is to widen the tolerance in steps, first to **0.5 Da**, then if needed **1.0 Da** (tab 5 covers the full troubleshooting checklist for this).

Once peak lists reach MASCOT itself, tolerances are expressed differently: the MS tolerance is commonly set around **40 ppm**, while the MS/MS tolerance is looser, up to **1,000 ppm**, since fragment peaks are weaker and less precisely measured than the parent peaks they came from.

Two modifications are used by default on every search here:

- Global modification **Carbamidomethyl (C)**: accounts for the alkylation step in sample preparation, which permanently and uniformly modifies every cysteine, so it is set as a fixed rule rather than something the search has to guess at.
- Variable modification **Oxidation (M)**: methionine oxidizes spontaneously during sample handling and storage, so the search allows for it, but only as an optional possibility, since not every methionine will actually be oxidized.

### The manual route: BioTools and MASCOT

This lab also runs a manual alternative using BioTools instead of ProteinScape: measure and calibrate the MS spectrum as usual, send the peak list to BioTools, then open its MASCOT search window and set the real parameters (missed cleavages Partial, typically allowing 1; database NCBI or Swissprot; MS tolerance around 40 ppm; the same two modifications as above). Peaks chosen for confirmation are sent back to flexControl as an MS/MS list, where a LIFT method is opened and the PCIS window (the mass window around the parent ion) is widened if needed, typically to roughly 0.43% of the parent mass. Parent mode is shot with PLMS (Post-LIFT Metastable Suppression) switched off, then fragment mode is shot and summed until the fragment ladder is clean.

## Worked example

Start with a protein digest spotted with HCCA matrix on a ground steel target, with a Peptide Calibration Standard II spot alongside it. flexControl measures the MS spectrum of both spots, and flexAnalysis finds the peaks and calibrates the sample spectrum against the calibrant spot.

1. **Pick candidate peaks.** The resulting peak list usually has dozens of peaks, but only a handful, typically **4 to 8 of the highest-intensity, well-separated peaks**, get chosen for MS/MS confirmation.
2. **Exclude the trypsin peaks.** One strong peak sits right at m/z 842. This is a trypsin autolysis peak, a leftover fragment of the digestion enzyme itself, not a fragment of the sample protein, so it is excluded from the MS/MS list. The same applies to peaks at 1,045 and 2,678 Da.
3. **Measure MS/MS on the rest.** The remaining strong peaks are sent to flexControl as an MS/MS list. flexControl switches to a LIFT method and measures each one in turn: parent mode in 50-shot steps up to 800 total shots, then fragment mode in 100-shot steps up to 4,000 total shots, building a readable ladder of b-type and y-type fragment ions.
4. **Search.** Both the MS peak list and the MS/MS peak lists go to ProteinScape, which searches MASCOT using the tolerances above. A confident result comes back as a high-scoring protein hit, with several tryptic peptides matched and the MS/MS spectra confirming their exact sequences.

### Fine-tuning a low-scoring hit with simple arithmetic

Sometimes MASCOT returns a correct but low-scoring hit because automatic peak-picking missed a couple of fragment ions in the y-ion ladder (the series of ions counted from the C-terminal end of the peptide). When that happens, you do not have to accept the lower score: you can often calculate exactly where the missing peaks should be and confirm them by eye.

Suppose the y-ion ladder is missing two expected ions, y12 and y11, but y13 is clearly present at m/z 1,412. Each step down the ladder subtracts the mass of one amino acid, in the order the peptide sequence predicts:

- The amino acid between y13 and y12 is proline, which weighs **97 Da**. So y12 should sit at 1,412 minus 97, which is **1,315**.
- The next amino acid, between y12 and y11, is glutamine, which weighs **128 Da**. So y11 should sit at 1,315 minus 128, which is **1,187**.

Checking the spectrum at m/z 1,315 and m/z 1,187 finds small peaks that were there all along, just not picked up automatically. Adding and annotating these two peaks by hand (both flexAnalysis and BioTools have an amino-acid annotation tool for exactly this) and re-running the search gives the full sequence recognized, with a noticeably higher score than before.

## Figure

A box-and-arrow pipeline diagram (flexControl, flexAnalysis, ProteinScape, MASCOT, with a return loop from flexAnalysis back to flexControl for LIFT MS/MS) appears in the illustrated HTML version of this guide.

## Common misconceptions

- **"Every peak in a digest spectrum comes from the sample protein."** The digestion enzyme itself shows up too: trypsin autolysis peaks at m/z 842, 1,045, and 2,678 must be recognized and excluded before MS/MS selection.
- **"A low MASCOT score always means the identification is wrong."** Sometimes it only means a couple of fragment peaks were missed by automatic peak-picking; calculating their expected positions by simple subtraction and confirming them by eye can raise the score substantially.
- **"MS/MS fragment mode and parent mode need about the same number of shots."** Fragment mode needs far more, 4,000 shots versus 800 for parent mode, because the fragment signal is much weaker than the parent peak it came from.
- **"The mass tolerance means the same thing at every stage of the search."** The initial PMF search uses a tolerance in Da (0.1, widened to 0.5 or 1.0 if needed), while MASCOT itself works in ppm (around 40 ppm for MS, up to 1,000 ppm for MS/MS).

## Self-check questions

1. Name the four pieces of software or tools in the automated identification pipeline, in order.
2. Why is a strong peak at m/z 842 in a tryptic digest usually excluded from the peaks sent for MS/MS confirmation?
3. Why does MS/MS fragment mode require so many more total shots (4,000) than parent mode (800)?
4. If y13 is observed at m/z 1,412, and the next residue toward y12 is proline (97 Da), what m/z would you expect for y12?
5. What is the difference between the global modification Carbamidomethyl (C) and the variable modification Oxidation (M) in a MASCOT search here?

### Answers

1. flexControl, flexAnalysis, ProteinScape, and MASCOT.
2. Because m/z 842 is one of the three recognized trypsin autolysis peaks (the others are 1,045 and 2,678 Da), coming from the digestion enzyme itself rather than the sample protein.
3. Because the fragment signal is much weaker than the parent peak it came from, so more shots are needed to build up a clean, readable fragment spectrum.
4. 1,412 minus 97 equals 1,315.
5. Carbamidomethyl (C) is applied globally to every cysteine because the alkylation step modifies all of them permanently and uniformly; Oxidation (M) is only variable, allowed as a possibility on methionine, because not every methionine actually gets oxidized.

## What to take forward

A trustworthy protein identification depends on excluding the known trypsin autolysis peaks before MS/MS, using the right tolerances at each stage, and remembering that a low score can sometimes be rescued with simple arithmetic rather than discarded.

## Glossary terms introduced

- **PMF (peptide mass fingerprinting):** identifying a protein by matching a list of measured peptide masses against a database.
- **MS/MS:** a second round of mass spectrometry that measures the fragments of a chosen peptide to confirm its sequence.
- **LIFT:** the method/cell used on this instrument to perform MS/MS measurements.
- **Near-neighbour calibration:** calibrating a sample spectrum using the calibration fit from the nearest calibrant spot.
- **AutoXecute:** the flexControl feature that runs an automated measurement sequence across a whole plate.
- **PCIS window:** the mass window set around a parent ion before LIFT MS/MS measurement.
- **b-ion / y-ion:** the two families of fragment ions produced when a peptide backbone breaks, read from the N-terminal or C-terminal end respectively.
- **Carbamidomethyl (C):** a fixed, global modification applied to every cysteine, accounting for the alkylation step in sample preparation.
- **Oxidation (M):** an optional, variable modification allowed on methionine, since oxidation during handling is not guaranteed.
