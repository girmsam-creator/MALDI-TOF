# Sample Prep & Instrument Setup

## Purpose

This is where the guide turns from theory into bench work. Good spectra start before the instrument ever fires a laser: how you prepare the sample decides whether you get a clean, identifiable spectrum or noise. This tab walks through the real plate, the real recipe, the real calibration standards, and the real software settings used with the Bruker UltrafleXtreme MALDI-TOF/TOF in Aalto University's Molecular Biotechnology lab.

## Key ideas

**The target plate.** The plate used in this lab holds 384 spots, arranged as 16 rows (A to P) by 24 columns (1 to 24). Ground steel is the default plate for almost everything: peptides, protein digests, and most other biomolecules in acetonitrile or water. Because it is easy to lose track across 384 positions, mark which spots you used on the paper target plate map that comes with the plate. Loading the plate follows a fixed routine: check the access light is green and no plate is loaded, open the inlet door, check the rubber sealing is clean, insert the plate with its frame cut corners first (sample spots facing the machine's longer side), close the door and press Load/Eject, then wait for the status light to turn green before doing anything else. After measuring, press Load/Eject again and wait for green a second time before opening the door.

**Preparing a simple peptide sample with HCCA.** The most common case in this lab is a plain peptide sample (for example a tryptic digest) spotted with HCCA matrix:

1. Make sure the sample contains no salts, buffers, or detergents, these will ruin the spectrum; desalt first if needed, for example with a C18 ZipTip.
2. Prepare a saturated solution of HCCA in TA30 (the standard solvent: 30 percent acetonitrile and 70 percent 0.1% TFA in water, by volume).
3. Mix one part of your sample solution with one part of the HCCA solution (a 1:1 mix).
4. Deposit 0.5 microliters of the mixture onto a clean, unused spot and let it dry at room temperature. This is the dried droplet method.
5. Always spot a calibrant alongside your sample, mixed with the same matrix, so you have something of known mass to calibrate against.

**The calibration standards used in this lab.** A spectrum is only as trustworthy as its calibration. Three Bruker standards are kept in the freezer, each covering a different mass window, and each must be mixed with the same matrix as whatever sample it calibrates:

| Standard | Covers roughly | Contents and exact masses ([M+H]+) |
| --- | --- | --- |
| Peptide Calibration Standard II | 700 to 3500 Da | 8 peptides: Bradykinin 1-7 (757.3992 Da), Angiotensin II (1046.5418 Da), Angiotensin I (1296.6848 Da), Substance P (1347.7354 Da), Bombesin (1619.8223 Da), ACTH clip 1-17 (2093.0862 Da), ACTH clip 18-39 (2465.1983 Da), Somatostatin 28 (3147.4710 Da) |
| Protein Calibration Standard I | 4000 to 20,000 Da | 4 proteins: Insulin (5734.51), Ubiquitin I (8565.76), Cytochrome C (12360.97), Myoglobin (16952.30) |
| Protein Standard II | roughly 10,000 to 50,000 Da | 3 proteins: Trypsinogen (23982), Protein A (44613), and BSA (approximately 66.5 kDa); BSA is not recommended as a calibrant on its own because its mass is too variable from batch to batch |

A small honest note from the source material: the manufacturer's own instructions say the peptide standard contains nine peptides, but only eight ever show up with masses given anywhere in the documentation, so work from the eight you can actually confirm. Store all three standards frozen, never refreeze one once thawed, and always use a fresh spot of standard for the detector check too.

**Walking through flexControl.** flexControl is the program you use to fire the laser and acquire a spectrum. The camera view on the left shows your sample spot, and you can click to move around within it even while shooting. Laser power is adjusted on the right of the camera view: if the signal is weak and noisy, power is too low, increase it; if the baseline does not return to zero between isotope peaks (poor "baseline separation"), power is too high, decrease it. The Add button adds the current spectrum to your running sum, Undo removes the last one added, and you can only fire the laser when the screen says READY. When done, Save As lets you save either Single (individual shots) or Sum (the summed spectrum).

Methods follow a naming convention worth learning: LIFT means MS/MS mode, L means linear mode, R means reflector mode, P means positive ion mode, N means negative ion mode, and any numbers give the mass range. For example, "RP 700-3500" is reflector mode, positive ions, covering 700 to 3500 Da, a typical peptide method.

A few flexControl tabs matter most day to day:

- Sample Carrier: controls how the plate moves while shooting. Random Walk (moving the plate slightly after a set number of shots) is best left on: use "Complete sample" on normal plates and "Partial sample" on AnchorChip plates.
- Detection: sets the mass range and sample rate. A sample rate of 2.00 works well for peptides; for large proteins use a lower rate like 1.00, or the file size balloons.
- Processing: a quick look while shooting; the real processing happens afterwards in flexAnalysis. Centroid picks the whole-peak average mass (better for large molecules whose isotopes cannot be told apart); Snap picks the monoisotopic mass (better for peptides, where isotopes are resolved). A signal-to-noise threshold around 10 is typical for picking peaks at all.
- Calibration: calibrate against the standard spotted alongside your sample, in the same matrix. Near-neighbour calibration (using the physically closest calibrant spot) gives the best accuracy; on a normal plate, one calibrant spot in the middle of eight sample spots works well. Three calibration modes exist: cubic enhanced (most accurate, needs at least 6 known calibrant masses), quadratic polynomial (needs at least 4), and linear (least accurate, needs only 2, so it suits a narrow mass range). An acceptable calibration error is under 5 ppm for peptides and under 100 ppm for intact proteins.

**Keeping the instrument healthy.** The detector's sensitivity drifts slowly over time, so run a detector check monthly, and always before an important project, using a fresh spot of HCCA matrix. If the recommended voltage differs from the one currently set by more than 30 V, adjust the detector gain to match.

**Lab discipline and why it matters.** The MALDI room also houses nano-LC and ESI equipment that is extremely sensitive to contamination, especially from detergents and synthetic polymers like PEG. MS-grade glassware stays in the room, used only with MS-grade solvents, never washed with detergent or put in a dishwasher. Bring your own pipettes for MALDI work rather than using the room's LC/MS-only pipettes, and never pipette directly from a large solvent bottle, use the smaller working bottles instead. Two numbers make the stakes concrete: PEG is tolerated only up to 0.1% w/v before it hurts signal quality, and detergents such as SDS, CHAPS, and CHAPSO are flatly incompatible with MALDI at any real concentration.

## Worked example

Here is the complete, real walkthrough for preparing and measuring a tryptic peptide digest, step by step, using only the numbers given in this tab:

1. Confirm the sample has no salts, buffers, or detergents; if unsure, desalt with a C18 ZipTip.
2. Prepare a saturated HCCA solution in TA30 (30% acetonitrile, 70% 0.1% TFA in water).
3. Mix your peptide sample 1:1 with the HCCA solution.
4. Deposit 0.5 microliters onto a clean, unused spot on the 384-spot ground steel plate, and let it dry (dried droplet method).
5. Spot Peptide Calibration Standard II (covering 700 to 3500 Da, a good match for typical tryptic peptides) mixed with the same HCCA matrix on a nearby spot, following near-neighbour practice, one calibrant spot in the middle of eight sample spots.
6. Load the plate: confirm the access light is green, open the inlet door, check the seal, insert the plate corners-first, close the door, press Load/Eject, and wait for green.
7. In flexControl, choose a method named along the lines of "RP 700-3500", reflector mode, positive ions, 700 to 3500 Da, matching both the peptide mass range and the calibrant's range.
8. Set the sample rate to 2.00 (suited to peptides) and use Snap peak picking, since peptide isotopes are resolved, with a signal-to-noise threshold around 10.
9. Calibrate using the standard's 8 known masses; with 8 available, cubic enhanced calibration (needs at least 6) is usable, and should give an error under 5 ppm, the acceptable threshold for peptides.
10. Save the summed spectrum (Sum) once enough shots have been added for a clean signal.

## Figure

A five-step vertical flow diagram (sample+HCCA in TA30 mixed 1:1, spot 0.5 microliters as a dried droplet, add a calibrant spot, load the 384-spot plate, run flexControl) appears in the illustrated HTML version of this guide.

## Common misconceptions

- "A little salt or buffer in the sample will not matter much." Salts, buffers, and detergents are not allowed in a MALDI sample and will ruin the spectrum; they need to be removed (desalted) before spotting.
- "Any one calibration spot anywhere on the plate is good enough." Near-neighbour calibration, using the calibrant spot physically closest to your sample, gives the best accuracy; calibration error should stay under 5 ppm for peptides and under 100 ppm for intact proteins.
- "More laser power always gives a better, cleaner spectrum." Too much power causes a baseline that never returns to zero between isotope peaks (poor baseline separation); the fix is to decrease power, not increase it.
- "Pipettes and glassware in the MALDI room are interchangeable with other lab equipment." The room also houses contamination-sensitive nano-LC and ESI equipment, so MS-grade glassware and dedicated pipettes are used only there, never washed with detergent, because even small amounts of PEG (above 0.1% w/v) or common detergents like SDS can ruin results.

## Self-check questions

1. What are the five steps of preparing a simple HCCA peptide sample, in order?
2. Why must a calibrant be spotted alongside every sample, and what does "near-neighbour calibration" mean?
3. Which calibration mode (cubic enhanced, quadratic polynomial, or linear) requires the fewest known calibrant masses, and what is the trade-off?
4. If the baseline does not return to zero between isotope peaks in flexControl, what is wrong, and what should you do?
5. Why can even a small amount of detergent or PEG in a MALDI sample be a serious problem in this particular lab?

### Answers

1. Confirm the sample has no salts, buffers, or detergents (desalt if needed); prepare saturated HCCA in TA30; mix the sample 1:1 with the HCCA solution; deposit 0.5 microliters on a clean spot and let it dry; spot a calibrant in the same matrix alongside it.
2. A spectrum's calculated mass depends on calibration against ions of known mass, and conditions can vary slightly across the plate, so using the calibrant spot physically closest to the sample spots (near-neighbour calibration) gives the most accurate result.
3. Linear calibration needs only 2 known masses, but it is the least accurate and suits only a narrow mass range; cubic enhanced is the most accurate but needs at least 6 known calibrant masses.
4. The laser power is too high; the fix is to decrease it.
5. The MALDI room also houses nano-LC and ESI equipment that is extremely sensitive to contamination; PEG above 0.1% w/v already hurts signal quality, and detergents like SDS, CHAPS, and CHAPSO are flatly incompatible with MALDI at any real concentration, so contamination can ruin results for everyone using the shared room.

## What to take forward

A good spectrum is decided before the laser ever fires: clean sample prep (no salts or detergents), the right matrix and plate, and a calibrant spotted right next to your sample are what make the next tab's job, reading the spectrum, possible at all.

## Glossary terms introduced

- Target plate: the metal plate with many spots where matrix-sample mixtures are deposited and dried before measurement.
- TA30: the standard solvent used for HCCA, 30% acetonitrile and 70% 0.1% TFA in water.
- Calibrant: a substance of known, exact mass spotted alongside a sample so the instrument's mass readings can be corrected against it.
- Near-neighbour calibration: calibrating a sample spot using the calibrant spot physically closest to it, for the best accuracy.
- Signal-to-noise (S/N) threshold: the minimum ratio of peak height to background noise the software requires before it will count something as a real peak.
- Centroid vs Snap: two peak-picking modes in flexControl; Centroid reports the whole-peak average mass, Snap reports the monoisotopic mass.
- LIFT: the naming-convention label in flexControl methods meaning MS/MS (fragmentation) mode.
- Detector gain: a setting adjusted to keep the detector's sensitivity consistent over time.
- ZipTip: a small pipette-tip device used to desalt or clean up a sample before MALDI analysis.
