# Case Study: Glycopeptides

## Purpose

A plain peptide has one fixed mass: cut it with an enzyme and you get the same number every time. A glycopeptide is that same peptide wearing a sugar chain that can vary enormously in size and shape from one copy to the next, so the glycopeptide's total mass keeps shifting even though the peptide underneath never changes. This tab explains the real software settings a lab uses to pull those two things apart: the fixed peptide, and the variable sugar sitting on top of it.

## Key ideas

### Why a fixed mass shift works for one modification, but not for a glycopeptide

A standard database search finds a chemical modification by looking for a fixed mass offset. For example, the peptide FQSEEQQQTEDELQDK has an unmodified calculated mass of MH+ 1981.8 Da. Its phosphorylated form comes in at MH+ 2061.8 Da, a clean +80 Da that software can search for directly, because every phosphate group adds the same amount of mass no matter which protein it sits on.

A glycopeptide cannot be searched this way. The same peptide backbone, at the same glycosylation site, can carry ten or more different sugar chains, each adding a different mass to the total, so there is no single number to add. This means glycopeptide software needs a separate strategy: first work out that a spectrum belongs to a glycopeptide at all, then work out the peptide's mass separately from the sugar's mass.

### Spotting a glycopeptide spectrum: oxonium ions and mass gaps

A glycopeptide-recognition tool filters MS/MS spectra in two steps. First, it checks for diagnostic oxonium ions, small sugar-only fragments that appear at the same fixed masses no matter what protein they came from, such as 204 Da and 366 Da. Second, it checks for diagnostic mass distances between peaks: 162 Da for a hexose sugar, 203 Da for a HexNAc sugar, and 291 Da for a sialic acid (also called NeuAc). Any spectrum that shows these signatures is flagged as a likely glycopeptide, and the tool then works out a likely mass for the peptide alone by reading backward from those same sugar-specific patterns.

On top of this, there is a more specific signature: the last HexNAc sugar still attached to the peptide tends to break apart in a recognisable three-gap pattern, 17, 83, and 120 Da apart. This pattern comes from cross-ring cleavage of that terminal HexNAc, right at the asparagine glycosylation site. It is a separate, smaller-scale phenomenon from the 162/203/291 Da gaps and the 204/366 Da oxonium ions, so the two sets of numbers should not be treated as interchangeable.

The actual settings used for this recognition step: classification method "N-glycopeptide MALDI", a distance tolerance of 0.5 Da, a peptide mass offset of H+ (1.008 Da), and a minimum peptide mass of 800 Da. A stricter minimum than the usual default of 600 Da is used deliberately, because false matches from random short "peptides" are more likely to appear at low mass.

### Matrix and mode: a correctness decision, not just a sensitivity one

Which matrix and which mode to use is not only about getting a strong signal. On a glycopeptide, it changes what the spectrum actually shows. Neutral, non-sialylated glycopeptides are run with HCCA matrix in reflector mode. Acidic, sialylated glycopeptides must be run with 2,5-DHB or 2,5-DHAP matrix in linear mode, not reflector mode, because reflector mode causes sialic acid groups to break off mid-flight through metastable decay. A sialylated glycopeptide run in reflector mode would give a wrong picture of the real sugar pattern; only linear mode shows the true one.

### Searching for the glycan itself

Once a spectrum is flagged as a glycopeptide and a peptide mass has been worked out, a second search tool looks for the glycan itself, treating the peptide mass as a known, fixed offset rather than something it needs to solve. Typical settings: glycan type "N-glycan core basic", a public glycan database, underivatized samples, a free reducing end, H+ ions, an MS tolerance of 0.7 Da, and an MS/MS tolerance of 0.9 Da. The match score for this search has two parts: Fragmentation Coverage % (what fraction of the expected glycan fragments were actually seen) and Intensity Coverage % (how much of the total signal those matched fragments account for).

## Worked example

EEQFNSTFR is a real tryptic glycopeptide from mouse IgG1, carrying an N-glycosylation site at the asparagine (N). Its MS/MS spectrum shows a spread of peaks across the full mass range, and reading them step by step shows exactly how the recognition logic above plays out on a real spectrum:

1. **Low-mass oxonium ions appear first.** Peaks at 204.102 Da and 366.085 Da sit close to the 204 Da and 366 Da oxonium ion signatures, immediately flagging this spectrum as a likely glycopeptide.
2. **A ladder of glycan fragments fills the middle of the spectrum.** Peaks such as 138.081, 241.089, 423.194, 735.338, 982.595, 1,709.862, and 2,399.432 Da are all glycan-moiety fragments, pieces of the sugar chain breaking apart at different points.
3. **The bare peptide mass shows up as its own region.** Around 1,506.768 Da, a peak labelled "Peptide MH+" in the lab's own training material marks something close to the bare peptide mass, exactly the number the recognition software works out from the surrounding glycan pattern.
4. **The full, intact glycopeptide appears at the high-mass end.** A peak at 2,618.544 Da is labelled "[Peptidoglycan] MH+", the complete peptide plus its attached sugar chain together, with the highest-mass peak in the spectrum observed at 2,764.071 Da.

Two honest notes on this real spectrum: the diagnostic mass often quoted for fucose (around 146 Da) is general glycobiology knowledge and does not actually appear as a number in this particular lab's own documents, so it is useful background rather than something confirmed here. Also, real instrument documentation is sometimes a little inconsistent: one peak above is listed as 2,561.498 Da in one training slide and as 2,506.5 Da in a different, zoomed-in copy of the same figure, most likely a labelling or digitization slip between two copies of one real spectrum rather than two different measurements.

## Figure

A figure (The EEQFNSTFR glycopeptide spectrum moves from diagnostic sugar-only oxonium ions, through glycan mass gaps, to the bare peptide region, and finally the full glycopeptide mass, based on the "Case Study: Glycopeptides" tab of the MALDI-TOF Study Guide.) appears in the illustrated HTML version of this guide. Alt text: A left-to-right diagram showing oxonium ions at 204 and 366 Da, then the three diagnostic mass gaps of hexose, HexNAc and sialic acid, leading to a bare peptide region near 1,507 Da, and finally the intact glycopeptide mass of 2,618.5 Da.

## Common misconceptions

- **"A glycopeptide's mass can be searched the same way as a phosphopeptide's."** It cannot. A phosphate group always adds a fixed +80 Da, but a glycan's mass varies hugely from one copy of the same peptide to the next, so there is no single fixed offset to search for.
- **"The 162/203/291 Da gaps and the 17/83/120 Da gaps mean the same thing."** They do not. The larger gaps (162, 203, 291 Da) come from whole sugar units breaking off the glycan chain. The smaller 17/83/120 Da gaps come from a single terminal HexNAc breaking apart internally, right at the glycosylation site, a separate and smaller-scale effect.
- **"Reflector mode is always the better choice because it gives sharper peaks."** For sialylated glycopeptides specifically, reflector mode is wrong, not just lower quality: it causes sialic acid groups to break off mid-flight, distorting the real sugar pattern. Linear mode is required there.
- **"Oxonium ions tell you which protein the glycopeptide came from."** They do not. Oxonium ions are sugar-only fragments and appear at the same fixed masses no matter which protein or peptide they are attached to; they only flag that a glycan is present, not which peptide it sits on.

## Self-check questions

1. Why can a glycopeptide's extra mass not be searched for as a single fixed offset, unlike a phosphate group's?
2. What two kinds of clues does the recognition software look for to flag a spectrum as a likely glycopeptide?
3. Why must a sialylated glycopeptide be run in linear mode rather than reflector mode?
4. In the EEQFNSTFR example, roughly what mass marks the bare peptide region, and what mass marks the full intact glycopeptide?
5. Why is the fucose mass of about 146 Da described as background knowledge rather than a confirmed number in this tab?

### Answers

1. Because the sugar chain attached to a glycopeptide varies enormously in size from one copy to the next, so there is no single number that always represents "the glycan's mass" the way +80 Da always represents a phosphate group.
2. Diagnostic oxonium ions (small sugar fragments at fixed masses, such as 204 and 366 Da) and diagnostic mass distances between peaks (162 Da for a hexose, 203 Da for a HexNAc, 291 Da for a sialic acid).
3. Because reflector mode causes sialic acid groups to break off mid-flight through metastable decay, which distorts the real sugar pattern; only linear mode shows the sugar pattern accurately.
4. The bare peptide region sits around 1,506.768 Da ("Peptide MH+"), and the full intact glycopeptide appears at 2,618.544 Da ("[Peptidoglycan] MH+").
5. Because that number is general glycobiology knowledge and does not actually appear anywhere in this lab's own documents, so it should be treated as useful background rather than a value confirmed by this lab's own protocols.

## What to take forward

A glycopeptide's mass keeps moving because its sugar chain varies, so recognizing one depends on spotting sugar-specific oxonium ions and mass gaps first, then working out the peptide's fixed mass separately; the next tab returns to this same peptide to show the phosphorylation side of this same mass-shift logic in more depth.

## Glossary terms introduced

- Glycopeptide: a peptide with a sugar chain (glycan) attached at a specific site.
- Oxonium ion: a small, sugar-only fragment that appears at a fixed mass regardless of which protein it came from, used to flag a glycopeptide spectrum.
- Hexose, HexNAc, sialic acid (NeuAc): three types of sugar units commonly found in glycan chains, each with its own fixed mass contribution.
- Cross-ring cleavage: a sugar ring breaking apart internally rather than at the bond connecting it to its neighbour, producing smaller, characteristic mass gaps.
- Linear mode / reflector mode: two ways of measuring ion flight time; some fragile ions, such as sialylated sugars, only give an accurate reading in linear mode.
- MH+: the mass of a molecule plus one added proton, the form in which it is usually measured and reported in positive-ion MALDI.
