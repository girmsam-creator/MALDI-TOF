# Overview & How It Works

## Purpose

Before you touch any sample or any button on the instrument, you need one clear picture in your head: what is this machine actually doing, and why should you trust the numbers it gives you. This tab builds that picture using the real instrument your course is built around, a Bruker UltrafleXtreme MALDI-TOF/TOF in Aalto University's Molecular Biotechnology lab. Everything later in the guide, sample prep, reading a spectrum, every case study, leans on the ideas introduced here, so it is worth reading slowly even if you plan to skim the rest.

## Key ideas

**What the name means.** MALDI-TOF stands for Matrix-Assisted Laser Desorption/Ionization, Time-Of-Flight mass spectrometry. In plain words, it is a very precise, very fast weighing machine for molecules. You put a biological sample in, and it tells you the exact masses of the molecules inside it, proteins, peptides, or sugar chains, as a list of peaks on a graph.

**The real instrument.** The Bruker UltrafleXtreme used in this lab can reach a resolution up to 40,000 and an advertised mass accuracy of 1 ppm (one part per million: for a 1000 Da peptide, that is an error of about 0.001 Da). You will work with it through several programs: flexControl (fires the laser and collects spectra), flexAnalysis (processes spectra and picks peaks), ProteinScape (searches a database to identify what you found), GlycoQuest (a glycan search built into ProteinScape), and WARP-LC (automates runs where the sample is separated by liquid chromatography first).

**Three things this lab actually uses it for.** The one capability, "tell me the masses in this sample," solves several different problems:

1. Identifying proteins from a digest, by peptide mass fingerprinting (matching peptide masses to a database) plus MS/MS (fragmenting peptides for confirmation).
2. Identifying glycopeptides, by working out the sugar chain (glycan) and the peptide part together from how the glycopeptide breaks apart.
3. Sequencing an intact protein end to end without digesting it first, using a technique called in-source decay (ISD), which reads a ladder of fragments straight off the whole protein.

**The six-step journey from sample to spectrum.** Every MALDI-TOF run follows the same physical sequence, whatever the sample:

1. Matrix co-crystallization: the sample is mixed with a large excess of a small, light-absorbing chemical, the matrix (commonly HCCA), and dried onto a metal plate so the matrix crystallizes around the sample molecules.
2. Laser pulse: a short pulse from a nitrogen laser (337 nm, invisible UV light) hits the crystal.
3. Desorption and ionization: the laser energy vaporizes a tiny volume of the crystal and transfers a proton to some sample molecules, giving them a positive charge, usually just one, written [M+H]+.
4. Acceleration: a strong electric field (typically 15 to 25 kV) pushes all the newly formed ions down the flight tube, giving every ion approximately the same kinetic energy.
5. The flight tube (time-of-flight): past the accelerator there is no more field, so ions simply coast through a vacuum. Since they all got the same kinetic energy, lighter ions move faster and arrive sooner.
6. Detector: a detector at the far end records the exact arrival time of every ion. The software turns each arrival time into a mass-to-charge ratio (m/z) and plots it against how many ions arrived at that time (intensity). That plot is the spectrum.

One extra practical choice sits inside step 5: the instrument can run in linear mode (ions fly straight to a detector at the tube's end) or reflector mode (an electric mirror bounces ions back to a detector near the source, roughly doubling the flight path). Reflector mode gives sharper, more accurate peaks but only works well for smaller molecules; linear mode is used for larger molecules like intact proteins.

**The one equation behind all of it.** Everything the instrument reports comes from a single measurement, how long an ion takes to cross the flight tube:

t = L × sqrt(m / (2 z e V))

Here t is flight time, L is the length of the flight tube, m is the ion's mass, z is the number of charges on it, e is the elementary charge, and V is the accelerating voltage. The instrument already knows L, e, and V, so measuring t lets it solve for m/z directly. The plain-language version: lighter ions and more highly charged ions arrive sooner; heavier, less-charged ions arrive later. This is also why the axis on every spectrum is labeled "m/z" and not just "mass": almost all MALDI ions carry only one charge (z = 1), so m/z and mass are numerically the same, but the label leaves room for the rare doubly- or triply-charged ion.

**Where the tool is strong, and where it struggles.** No single instrument is best at everything.

| Where it wins | Where it struggles |
| --- | --- |
| Fast: results in minutes, not hours or days | Mostly gives you mass only; structural or linkage detail needs extra fragmentation work |
| Cheap per sample once the instrument is owned (roughly EUR 0.70 in reagents per bacterial ID) | High upfront instrument cost (roughly EUR 150,000 to 250,000) |
| Tolerant of "dirty" or crude samples: the matrix does a lot of the cleanup work | Mostly produces singly-charged ions, so less rich fragmentation than some other methods |
| Works on small amounts of material | Limited dynamic range: in tissue imaging it mostly detects the top 5 percent or so most abundant proteins |
| No antibody or label needed | Labile modifications (such as phosphorylation) can fall off during ionization or fragmentation |

## Worked example

Protein A, from the calibration standard used in this lab, shows how the m/z axis and charge state fit together in a real spectrum.

1. Protein A has a true mass of about 44,613 Da.
2. Most of the time, MALDI gives it one proton, so it shows up as a singly-charged [M+H]+ ion at m/z 44,613.
3. Occasionally, MALDI gives the same molecule two protons instead of one. It is now the same molecule, carrying two charges, written [M+2H]2+.
4. Because m/z is mass divided by charge, that doubly-charged version appears at roughly m/z 22,307, almost exactly half of 44,613.
5. The lesson: a single real molecule can create two different peaks on the same spectrum, far apart on the x-axis, simply because it picked up a different number of protons during ionization. Reading m/z correctly means always asking "which charge state is this."

## Figure

A six-step vertical flow diagram (sample+matrix on a plate, laser pulse, desorption and ionization, acceleration, flight tube, detector, ending in a mass spectrum) appears in the illustrated HTML version of this guide. It is based on the real six-step mechanism described above.

## Common misconceptions

- "The instrument puts the sample on a scale and weighs it directly." In reality, it never weighs anything. It measures how long each ion takes to fly down a tube, then calculates mass from that flight time using the equation above.
- "The number on the x-axis (m/z) is always the molecule's exact mass." Only when the ion carries a single charge (z = 1), which is the most common case in MALDI. A doubly-charged ion of the same molecule appears at roughly half that m/z value, as the Protein A example shows.
- "MALDI-TOF can tell you exactly how a molecule is built, atom by atom, on its own." Mostly it gives you mass only. Working out structural or linkage detail (such as where a sugar chain attaches) needs extra fragmentation steps or complementary software, covered in later tabs.
- "Linear mode and reflector mode are basically the same, just pick either one." They trade off sharply: reflector mode gives much sharper peaks but only works well for smaller molecules, while linear mode is needed for very large, intact molecules that would lose signal in the mirror.

## Self-check questions

1. What does MALDI-TOF measure directly, and how does the instrument turn that measurement into a mass?
2. List the six steps of a MALDI-TOF run, in order, from sample to spectrum.
3. Why does Protein A appear at two different m/z values in a real spectrum (around 44,613 and around 22,307)?
4. Name one strength and one weakness of MALDI-TOF from the comparison table in this tab.
5. Why is reflector mode not always the better choice, even though it gives sharper peaks?

### Answers

1. It measures flight time, how long each ion takes to travel down the flight tube. Using the equation t = L × sqrt(m / (2zeV)), with L, e, and V known from the instrument's design and settings, it solves for m/z from the measured t.
2. Matrix co-crystallization, laser pulse, desorption and ionization, acceleration, flight through the field-free tube, and detection (which produces the m/z vs intensity spectrum).
3. Because m/z is mass divided by charge. The same 44,613 Da molecule carrying one proton ([M+H]+) appears at m/z 44,613; carrying two protons ([M+2H]2+) it appears at roughly half that value, m/z 22,307.
4. Any one pairing from the table is correct, for example: strength, it is fast (minutes, not hours); weakness, it mostly gives mass only, so structural detail needs extra fragmentation work.
5. Reflector mode only works well for smaller molecules; very large, intact molecules can fragment or lose too much signal bouncing off the mirror, so linear mode is used for those instead.

## What to take forward

Every number this instrument reports traces back to one measured quantity, flight time, and one equation linking flight time to mass and charge; once that clicks, every later tab (sample prep, spectra, troubleshooting) is really just details layered on top of this one idea.

## Glossary terms introduced

- MALDI-TOF: a technique that uses a laser and a light-absorbing matrix to turn a biological sample into flying ions, then measures their masses by timing their flight.
- Matrix: a small, light-absorbing chemical mixed with the sample that protects it from the laser's energy and helps it become charged.
- Desorption/ionization: the moment the laser's energy vaporizes part of the sample-matrix crystal and gives some molecules an electrical charge.
- Time-of-flight (TOF): the part of the instrument where ions travel through a vacuum tube and get sorted by how fast they move.
- m/z (mass-to-charge ratio): the value plotted on a spectrum's x-axis; equals mass divided by the number of charges on the ion.
- Reflector mode: a setting where an electric mirror bounces ions back to a detector, giving sharper peaks for smaller molecules.
- Linear mode: a setting where ions fly straight to a detector without bouncing, used for very large molecules.
- Resolution: how finely the instrument can tell apart two very close masses.
- Mass accuracy: how close the instrument's reported mass is to the true mass, often given in parts per million (ppm).
- PMF (peptide mass fingerprinting): identifying a protein by matching the masses of its digested peptides against a database.
- ISD (in-source decay): a technique that reads fragments directly off an intact protein without digesting it first.
