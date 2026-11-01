# Mechanism Explained Simply

## Purpose

The previous tab explained the six-step MALDI-TOF process with equations and precise terms. This tab has one job: make that same process stick in your memory using everyday comparisons, so that when you walk up to the real instrument, the physics feels familiar rather than abstract. It draws on *Fundamentals of MALDI-ToF-MS Analysis* (Hosseini and Martinez-Chapa, Springer, 2017).

## Key ideas

**The matrix as an airbag.** Before 1985, mass spectrometry could only ionize samples by blasting them with an electron beam, a "hard" ionization that shattered fragile molecules like proteins into thousands of pieces. In 1985, two German scientists, Karas and Hillenkamp, found a gentler way: mix the fragile molecule with a small, sturdy helper molecule (the matrix) and fire a laser at the mixture. In 2002, Koichi Tanaka won a share of the Nobel Prize in Chemistry for extending this idea to large biological molecules. Think of the matrix as an airbag: the laser energy has to go somewhere, and the matrix absorbs almost all of it instead of your protein. The matrix heats up, flips from solid to gas in an instant, and drags your sample along with it into a small cloud of ions, mostly still in one piece. That protective role is why it is called soft ionization.

**The time-of-flight race.** Once the cloud of ions exists, an electric field gives every ion the exact same push of energy, like a starting gun firing for every runner in a race at once. With the same push (kinetic energy), a light ion accelerates to a higher speed than a heavy ion, the same way a tennis ball flies faster than a bowling ball if you push both with equal force. So lighter ions cross the flight tube faster and arrive first; heavier ions lag behind. The instrument only ever measures one thing directly, arrival time, then calculates the mass-to-charge ratio (m/z) using m/z = 2eE(t/d)^2, where E is the accelerating voltage, t is flight time, d is the tube length, and e is a physical constant. This is the same equation as tab 1's t = L × sqrt(m / 2zeV), just rearranged and dressed in a foot-race analogy instead of algebra.

**Linear mode vs reflectron mode, as a running track.** In theory, every ion of the same mass should arrive at exactly the same instant. In practice the laser does not hand out energy perfectly evenly, so ions of the same mass leave with slightly different speeds. In linear mode, that small spread in speed becomes a spread in arrival time, so the peak you see is broad and mushy, like trying to read a car's exact speed from a blurry photograph. Reflectron (mirror) mode fixes this: an electric mirror at the end of the tube reflects the ions back toward a second detector. Ions moving slightly faster penetrate slightly deeper into the mirror's field before turning around, which costs them a little extra time, so slower and faster ions of the same mass arrive back together. It works like sending runners of the same speed around a longer track with a U-turn: the ones who sprinted out too fast spend more time looping back, and the group re-syncs at the finish line.

| | Linear mode | Reflectron (mirror) mode |
| --- | --- | --- |
| How it works | Ions fly straight to one detector | Ions bounce off an electric mirror to a second detector |
| Resolution | Lower; peaks can blur together | Much higher; peaks are sharp and well separated |
| Best for | Very large, intact molecules that would fragment or lose signal in the mirror | Smaller molecules and peptides where exact mass matters |
| Trade-off | Simpler, more robust signal for huge molecules | Adds flight distance and time; huge ions can lose too much signal |

**Picking a matrix is real chemistry, not a formality.** A good matrix must strongly absorb light at the laser's exact wavelength, be mildly acidic so it can donate a proton to help ionize the sample, and crystallize evenly with the sample (co-crystallization) rather than separating out. Seven matrices actually get used in this lab:

| Matrix | What it's good for |
| --- | --- |
| HCCA | Peptides and proteins, roughly 0.7 to 20 kDa; default choice for most peptide and protein digest work |
| 2,5-DHB | A wide variety of peptides, proteins, polymers and carbohydrates, including phosphopeptides and glycoproteins |
| 2,5-DHAP | Proteins from about 8 to 100 kDa; prevents in-source decay fragmentation; good for glycoproteins |
| SA (sinapinic acid) | Larger proteins, roughly 10 to 150 kDa; weak below about 3 kDa |
| SDHB | Very large proteins and glycoproteins; suitable for ISD spectra of intact proteins |
| 3-HPA | Oligonucleotides (DNA/RNA), roughly 1 to 30 kDa |
| 1,5-DAN | Helps top-down ISD sequencing of intact proteins; hazardous, make fresh immediately before use |

Matrices are not perfect: some matrix/sample combinations are only stable for a few minutes before the signal degrades, some matrices self-polymerize and muddy the spectrum, certain matrices worsen mass discrimination, liquid matrices can contaminate the ion source over repeated runs, and matrices with low "protein affinity" cause more unwanted peptide fragmentation. The target plate matters too: ground steel (flat, the default, works for virtually any sample), AnchorChip (800 micron anchor, concentrates a dilute sample for high-throughput runs), BigAnchor (2000 micron, for matrices like DHAP that crystallize poorly on narrower spots), SmallAnchor (400 micron, for oligonucleotides with 3-HPA), and polished steel (flat, for low surface tension samples, must be washed right after use). Across almost all of these, the actual method used in this lab is the simplest one, dried droplet: mix matrix and sample in solution and let the drop dry on the plate.

**Mass discrimination: small ions crowd the door.** Even with a perfect matrix and perfect prep, MALDI-TOF under-reports heavy ions compared to light ones. Picture the detector as a single narrow doorway during a fire drill: the smallest, fastest people (light ions) reach the doorway first and pack it solid for a moment, so some of the taller, slower people (heavy ions) arriving a fraction of a second later never quite register as clearly. The main fix is turning up the laser power, which pushes more energy into heavier ions, but too much power causes unwanted fragmentation and can push ions to clump together (dimerize). There is no setting that eliminates mass discrimination entirely, only ways to reduce it.

**Coupling MALDI with other techniques.** MALDI-TOF is often paired with a second technique: ion-mobility TOF (IMS-TOF-MS) separates ions by shape as well as mass, useful for telling apart phosphorylated from non-phosphorylated peptides; FT-ICR-MS gives extremely precise mass measurements using a magnetic field instead of a flight tube; thin-layer chromatography (TLC) and size-exclusion chromatography (SEC) are offline separation steps performed before the sample ever reaches the MALDI plate.

## Worked example

This tab states a direct, real decision rule this lab actually follows for choosing mode and matrix. Walking through it step by step:

1. Ask what you are analyzing. For ordinary peptide work, such as the peptide identification case study elsewhere in this guide, peptides are small and robust.
2. Because they are small, reflector mode's sharper peaks matter and the peptides survive the extra flight path without losing signal. So: reflector mode + HCCA matrix is the default combination for peptide work.
3. Now ask about a different case: sequencing an intact, large, fragile protein end to end by in-source decay (ISD), without digesting it first.
4. Because these molecules are big and fragile, they would lose too much signal, or fragment further, bouncing around in reflector mode.
5. So the rule flips: linear mode + sinapinic acid (SA) or DHAP is used instead for ISD work on intact proteins.
6. The underlying logic in both cases is the same one from the table above: match the matrix's mass range and the mode's "best for" column to what you are actually measuring, rather than defaulting to one combination every time.

## Figure

A two-panel figure (linear mode giving one broad, blurry peak; reflectron mode giving two sharp, resolved peaks) appears in the illustrated HTML version of this guide.

## Common misconceptions

- "The matrix is just filler, the important chemistry happens to the sample alone." The matrix does most of the work: it absorbs the laser energy, protects the sample from being destroyed, and donates the proton that ionizes the sample.
- "Reflector mode is always better because it is sharper." It only works well for smaller molecules; very large, intact proteins lose too much signal or fragment further bouncing off the mirror, so linear mode is used for those instead.
- "If a peak looks small, there must be very little of that molecule in the sample." It might just be a heavy ion suffering from mass discrimination, the built-in bias where heavier ions are under-reported compared to light ones, even if equal amounts of each are present.
- "Any matrix works for any sample, you just pick your favorite." Matrix choice depends on mass range, chemistry, and even which target plate you use; the wrong matrix can mean poor crystallization, extra fragmentation, or a muddied spectrum.

## Self-check questions

1. Why is MALDI-TOF's ionization step called "soft" ionization, and what does the airbag analogy capture about it?
2. In the time-of-flight race analogy, why does a lighter ion arrive at the detector before a heavier one?
3. Why does reflectron mode produce sharper peaks than linear mode, using the U-turn track analogy?
4. Name one real matrix from the table and the approximate mass range it is suited to.
5. What is mass discrimination, and what is the one practical way (with its own trade-off) to reduce it?

### Answers

1. It is called soft because the matrix, not the sample, absorbs almost all of the laser's energy, like an airbag absorbing an impact, so fragile biomolecules survive mostly intact instead of being shattered.
2. Every ion gets the same push of kinetic energy from the electric field. With equal energy, a lighter object reaches a higher speed than a heavier one (like a tennis ball versus a bowling ball pushed equally hard), so it crosses the flight tube faster.
3. Ions of the same mass that happen to be moving slightly faster penetrate deeper into the mirror's electric field before turning around, which costs them extra time, so faster and slower ions of the same mass arrive back at the detector together, producing a sharper peak.
4. Any one is correct, for example: HCCA for peptides and proteins roughly 0.7 to 20 kDa, or SA for larger proteins roughly 10 to 150 kDa.
5. Mass discrimination is the built-in tendency to under-report heavy ions compared to light ones, because light ions crowd the detector first. The main fix is turning up the laser power, but too much power causes unwanted fragmentation and can make ions clump together (dimerize).

## What to take forward

The matrix protects your sample so it can become a gentle cloud of ions, and the choice of matrix, mode, and target plate is not a formality: it is a real decision, matched to the size and fragility of what you are measuring, that you will make every time you load a plate.

## Glossary terms introduced

- Hard ionization: an older, rougher ionization method (such as electron beam bombardment) that destroys fragile molecules.
- Co-crystallization: the process of the matrix and sample crystallizing together evenly as a spot dries.
- Reflectron mode: another name for reflector mode, where an electric mirror re-focuses ions of the same mass so they arrive together, sharpening the peak.
- Mass discrimination: the instrument's built-in tendency to detect light ions more easily than heavy ones, even when equal amounts are present.
- Dimerize: when two ions clump together under too much laser power, distorting the apparent mass distribution.
- Dried droplet method: the common sample prep method of mixing matrix and sample in solution and letting the drop dry on the plate.
- AnchorChip / BigAnchor / SmallAnchor: target plates with small chemically treated anchor spots of different sizes that concentrate a sample for sharper results.
- Ion-mobility TOF (IMS-TOF-MS): a coupled technique that separates ions by shape as well as mass.
- FT-ICR-MS: a technique that measures mass using a magnetic field instead of a flight tube, for extremely high precision.
