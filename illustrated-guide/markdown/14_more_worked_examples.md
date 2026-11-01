# More Worked Examples

## Purpose

Reading about mass spectrometry workflows is not the same as practicing them. This tab walks through four realistic research situations on this instrument: deciding how far to loosen a search tolerance, pinning down a phosphorylation site, judging whether a glycopeptide match can be trusted, and reading a protein's ends from a sequencing ladder. Each one shows the questions a researcher actually has to ask of the data, not just the final answer.

## Key ideas

**Order of operations matters more than loosening a setting.** When a database search fails to find a confident match, the instinct might be to immediately make the search more forgiving. The right first step is instead to check whether the data itself has a problem: bad calibration, or contaminating peaks that do not belong to the sample at all.

**A dominant signal can hide the evidence you actually need.** A phosphorylated peptide's fragmentation spectrum is often dominated by one very strong signal (the loss of the phosphate group itself), which can starve out the weaker signals needed to pin the modification to one exact location.

**A percentage alone does not make a match trustworthy.** Software can report two different coverage statistics, one about which fragment types appeared and one about how much signal they represent, and a result can score well on one while scoring poorly on the other.

**A ladder of peaks reveals structure one step at a time.** In sequencing-style spectra, the mass difference between two neighbouring peaks in an ion ladder should equal exactly one amino acid's mass. Where that pattern breaks, something real is usually different about the molecule, not the method.

## Worked example

**Case: deciding how far to widen a PMF search tolerance.**

Research question: a tryptic digest's peptide mass fingerprint (PMF) search comes back with no confident hit at the default, strict 0.1 Da tolerance. Is the protein simply not identifiable, or is something else going on?

Step by step, the way the real workflow handles it:

1. **Check calibration first, not the tolerance.** The strict 0.1 Da default only works when calibration is excellent. Check the calibration error on the calibrant spot used for that run. If it is already over 5 ppm, no amount of loosening the tolerance will fix a truly miscalibrated spectrum. Recalibrate before anything else.
2. **Check for autolysis peaks.** If calibration looks fine (under 5 ppm), check whether any of the unidentified peaks are actually trypsin autolysis peaks. These show up at m/z 842, 1045, and 2678 in almost every tryptic digest, because they come from the digestion enzyme itself, not the sample protein. A peak list cluttered with them can confuse the database search. Remove them and re-search at the strict 0.1 Da tolerance first.
3. **Only now widen the tolerance, one step at a time.** If calibration is clean and no autolysis peaks were the problem, widen the tolerance to 0.5 Da and search again. If still no hit, widen to 1.0 Da. Checking for a hit after each step, rather than jumping straight to the loosest setting, matters because a looser tolerance also raises the odds of a false match.
4. **If nothing works even at 1.0 Da,** check the taxonomy or database choice, and confirm the protease really was trypsin.

What a positive result looks like: a confident hit found once calibration is confirmed clean and autolysis peaks are excluded, ideally at the strict 0.1 Da tolerance or with only a modest widening. A hit that only appears at 1.0 Da, with calibration still shaky, is a result to treat with real caution rather than celebrate.

## Figure

A figure (Widening a PMF search tolerance should be the last step, not the first, based on the "More Worked Examples" tab of the MALDI-TOF Study Guide.) appears in the illustrated HTML version of this guide. Alt text: A vertical flow diagram showing that when a PMF search finds no confident hit, the correct order is to first check calibration error, then check for trypsin autolysis peaks at m/z 842, 1045 and 2678, and only after that widen the search tolerance step by step from 0.1 to 0.5 to 1.0 Da.

## Common misconceptions

- **"If the default tolerance finds nothing, just widen it."** Widening the tolerance is the last resort, not the first move. Calibration error and contaminating peaks (like trypsin autolysis peaks) should be ruled out first, because a looser tolerance also makes false matches more likely.
- **"A clean-looking +80 Da mass shift means the phosphorylation site is confirmed."** The shifted mass only confirms that the peptide is phosphorylated somewhere. Pinning down which exact residue carries the phosphate needs a clean fragment-ion ladder, which the dominant neutral-loss signal can make harder to see.
- **"A high percentage score always means a trustworthy match."** A glycopeptide match can have high Fragmentation Coverage (the right fragment types appear) while having low Intensity Coverage (those fragments represent only a small part of the real signal). Both numbers, and the raw spectrum, need checking together.
- **"Any deviation from a predicted sequence ladder means the experiment failed."** A mismatch confined to one end of the ladder, such as a protein's N-terminus or C-terminus, is often real biological information, like a terminal modification or a missing terminal residue, not a mistake.

## Self-check questions

1. Why is checking calibration error the first step, rather than widening the search tolerance, when a PMF search finds no hit?
2. At what three m/z values do trypsin autolysis peaks typically appear, and why can they interfere with a database search?
3. In the phosphorylation example, what mass loss commonly dominates the MS/MS spectrum, and why does this make localizing the site harder?
4. Why can't Fragmentation Coverage alone tell you whether a glycopeptide match is trustworthy?
5. In the ISD ladder example, what would an unexplained extra mass on the very first fragment of a sequence series suggest?

### Answers

1. A strict 0.1 Da tolerance only works if calibration is excellent. If the calibration error is already over 5 ppm, no amount of widening the tolerance will fix a truly miscalibrated spectrum, so recalibrating first avoids wasting steps on the wrong problem.
2. Around m/z 842, 1045, and 2678. They come from the digestion enzyme (trypsin) itself, not the sample protein, so if left in the peak list they can confuse or dilute a database search.
3. The 98 Da neutral loss of H3PO4 (phosphoric acid) commonly dominates the spectrum. Because it is so strong, it can starve out the weaker backbone b- and y-ion fragments needed to identify exactly which residue carries the phosphate.
4. Fragmentation Coverage only shows how much of the theoretical fragment pattern appeared in the spectrum; it says nothing about how much of the spectrum's real signal intensity that match actually accounts for, which is what Intensity Coverage measures.
5. It suggests a terminal modification (such as an N-terminal acetyl group) rather than a sequencing mistake, since the mismatch is confined to the start of the ladder rather than scattered throughout it.

## What to take forward

Before changing a setting to force a result, check whether the data itself, through calibration, contaminating peaks, or a dominant unrelated signal, is the real reason an identification looks uncertain.

## Glossary terms introduced

- Peptide mass fingerprint (PMF): identifying a protein by matching the set of masses from its digested fragments against a database.
- Calibration error: how far off an instrument's mass readings are from their true values, usually measured in parts per million (ppm).
- Autolysis peaks: peaks in a spectrum that come from the digestion enzyme breaking down itself, not from the sample.
- Neutral loss: a fragment of a molecule (such as phosphoric acid) that breaks away during fragmentation and is lost from the measured ion.
- Fragmentation Coverage: the percentage of a theoretical fragment pattern that actually appears in a spectrum.
- Intensity Coverage: the percentage of a spectrum's total signal intensity that a proposed match actually accounts for.
- Ion ladder: a series of fragment peaks, each one amino acid's mass apart, used to read a protein's sequence from one end.
