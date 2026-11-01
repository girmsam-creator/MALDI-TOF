# Common Errors & Troubleshooting

## Purpose

Sooner or later a spectrum will look wrong. The good news for a beginner is that on this instrument, a bad result is almost never caused by broken physics. It is almost always calibration drift or contamination, and each of those leaves its own recognizable fingerprint in the spectrum. Learning to recognize those fingerprints, instead of guessing, is what this tab is for.

## Key ideas

### Crystal and sample problems

Before you even shoot a spot, look at how it crystallized. Good crystals are small and even across the spot. How fast a spot dries, which depends on how much organic solvent is in the matrix solution, controls this: too little organic solvent and the spot dries slowly, producing large, uneven crystals; too much organic solvent and it dries too fast, so the sample never crystallizes properly at all, a visible pattern called the half-moon effect. The usual fix is adjusting the solvent ratio. For a matrix that crystallizes unevenly, such as 2,5-DHAP, it can also help to switch off Random Walk (the setting that moves the laser around the spot automatically) and shoot only inside the ring of crystals that forms at the edge of the dried drop, rather than letting the measurement wander into the empty middle.

### Reading the laser power signs

The laser power setting in flexControl, the software that controls the instrument during measurement, tells its own story about what is wrong:

- High noise together with a weak, low signal means the laser power is too low: increase it.
- A poor baseline, meaning the signal does not return to the baseline between isotope peaks, means the laser power is too high: decrease it.

### Calibration drift

If any single calibrant peak comes back with an error over 10 ppm (parts per million) after calibrating, do not trust that calibration: repeat it. If a detector check shows the recommended voltage has drifted more than 30 V from the current setting, the detector's gain needs adjusting before you can trust anything measured since the last check.

### Contamination

Salts, buffers, detergents, and polymers such as PEG all suppress or ruin a MALDI signal. As concrete numbers to keep in mind: PEG is tolerated only up to 0.1% w/v, and SDS, CHAPS, and CHAPSO are flatly incompatible with MALDI at any working concentration. If any of these might be present, desalting the sample first, for example with a C18 ZipTip, is not optional before trying again.

### The trypsin autolysis gotcha

If a sample was digested with trypsin, the enzyme itself shows up in the spectrum, not just the protein of interest. Trypsin autolysis peaks regularly appear at m/z 842, 1,045, and 2,678, and they are very easy to mistake for real peptides from the sample. Learn to recognize these three masses on sight and exclude them before sending a peak list to a database search.

### A "no hits" checklist

When a MASCOT search through ProteinScape comes back empty, work through these steps in order before concluding the protein simply is not in the database:

1. Widen the mass tolerance in steps: from 0.1 Da, to 0.5 Da, to 1.0 Da.
2. Double check the calibration the peak list was measured against.
3. Check that the taxonomy and database searched were the right ones.
4. Check that the protease really was trypsin, and not something else.
5. Check the sample quality itself, going back to the crystal and contamination checks above.

### How to tell if a result is good

Every step in this workflow produces some kind of number, and each one has a rough line between "trust it" and "look again":

| Step | Good value | Bad value, and what it usually means |
| --- | --- | --- |
| Calibration error | Under about 5 ppm for a peptide calibrant | Over 10 ppm: the calibration itself is unreliable; repeat it |
| Detector check | Small drift from the last setting | Over 30 V drift from the current setting: the detector's gain has degraded and needs adjusting |
| PMF search tolerance | A hit found at the strict default, 0.1 Da | Needing to widen to 0.5 or 1.0 Da to get any hit at all: a workable but weaker, less certain result |
| MASCOT score | At or above the significance threshold MASCOT reports (one real example from this lab's own protocol used an ions score threshold of 15.0) | Below that threshold: not a statistically significant match, even if it is the top name in the list |
| Resolution, reflector mode | Tens of thousands (about 30,000 for Cytochrome C) | A broad, unresolved hump where sharp isotope teeth were expected |

A good value is one that is tight, strong, or clearly ahead of its alternatives. A bad one is loose, weak, or ambiguous, which does not automatically mean the result is wrong, only that it needs a second look, a repeat measurement, or a second piece of supporting evidence before you act on it.

## Worked example

Suppose a MASCOT search through ProteinScape comes back with no hits at all for a tryptic digest. Here is how you would work through it using the real checklist above, in order:

1. **Widen the tolerance.** Start by widening the PMF search tolerance in steps: try 0.1 Da first (the strict default), then 0.5 Da, then 1.0 Da if needed. If a hit now appears at 0.5 Da, that is a workable result, but it is weaker and less certain than a hit found at the strict 0.1 Da default.
2. **Check the calibration.** Go back to the calibration run and check each calibrant peak's error. If any single peak is over 10 ppm, the calibration itself cannot be trusted, which would explain why tight tolerances found nothing: repeat the calibration before trying the search again.
3. **Check the taxonomy and database.** Confirm the search was pointed at the right organism and the right protein database; a search of the wrong species will not find a match no matter how good the spectrum is.
4. **Check the protease.** Confirm the digest really used trypsin, since the search's cleavage rules assume it; a different protease would cut the protein into different pieces than MASCOT is expecting.
5. **Check the sample itself.** If all of the above check out, go back to the crystal and contamination checks: uneven crystals or contamination (salts, detergents, PEG above 0.1% w/v) can quietly ruin a signal even when the software settings are all correct.

Working through these five checks in order, rather than jumping straight to "the protein is not in the database," catches the great majority of empty searches.

## Figure

A two-panel figure (laser power too low: high noise, weak signal, fix is to increase power; laser power too high: poor baseline between peaks, fix is to decrease power) appears in the illustrated HTML version of this guide.

## Common misconceptions

- **"If a search finds nothing, the protein just is not in the database."** In practice, calibration problems, the wrong tolerance, the wrong taxonomy, or sample contamination are far more common causes, and the checklist above should be worked through first.
- **"A weak signal always means the matrix or sample failed."** It can also simply mean the laser power is set too low, which is fixed by increasing it, not by remaking the sample.
- **"Once a spectrum is calibrated, its masses can always be trusted."** Only if the calibration error is small (under about 5 ppm for a peptide calibrant). An error over 10 ppm on any calibrant peak means the calibration itself needs to be repeated.
- **"A small amount of salt or detergent in a sample is not a big deal."** Some contaminants have very tight limits: PEG is only tolerated up to 0.1% w/v, and SDS, CHAPS, and CHAPSO are flatly incompatible with MALDI at any working concentration.

## Self-check questions

1. A spectrum shows high noise and a weak signal overall. What is the likely cause, and what should you adjust?
2. A spectrum's peaks sit on a baseline that never drops back down between isotope peaks. What does this suggest, and what should you do?
3. After calibrating, one calibrant peak comes back with an error of 14 ppm. Should you trust that calibration? Why or why not?
4. You see a strong peak at m/z 842 in a tryptic digest spectrum. Should you send it for MS/MS confirmation as a candidate sample peptide? Why or why not?
5. A MASCOT search comes back with no hits. Name two of the five checks you should work through before concluding the protein is not in the database.

### Answers

1. The laser power is likely too low; increase it.
2. This suggests the laser power is too high, since the baseline is not returning to zero between isotope peaks; decrease it.
3. No. The source rule is that an error over 10 ppm on any single calibrant peak means the calibration is unreliable and should be repeated before trusting anything measured against it.
4. No. m/z 842 is one of the three recognized trypsin autolysis peaks (the others are 1,045 and 2,678), which come from the digestion enzyme itself, not the sample protein, so it should be excluded.
5. Any two of: widen the mass tolerance in steps (0.1, 0.5, 1.0 Da); double check the calibration; check the taxonomy and database; check the protease was really trypsin; check the sample quality (crystals and contamination).

## What to take forward

When a result looks wrong on this instrument, check calibration error and contamination or crystal quality first. Those two things, not the underlying physics, are almost always the real cause.

## Glossary terms introduced

- **Half-moon effect:** a visible crystallization failure pattern caused by too much organic solvent drying the spot too fast.
- **Random Walk:** a flexControl setting that moves the laser automatically around a spot during measurement.
- **ppm (parts per million):** the unit used to express how far a measured mass is from its expected, calibrated value.
- **Calibration drift:** when a calibrant peak's measured mass no longer matches its known mass closely enough to trust.
- **Detector gain:** the amplification setting of the ion detector; it needs re-adjusting if its voltage drifts too far from its previous setting.
- **ZipTip:** a small cleanup tip (here, C18) used to desalt a sample before trying MALDI again.
- **Trypsin autolysis peak:** a peak coming from the digestion enzyme itself, not the sample protein; the three to recognize are m/z 842, 1,045, and 2,678.
- **PMF search tolerance:** how far, in Da, a measured peptide mass is allowed to differ from a database value during a peptide mass fingerprint search.
- **MASCOT ions score:** the confidence score MASCOT assigns to a search hit, compared against a significance threshold.
