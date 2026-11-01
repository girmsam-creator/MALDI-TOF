# TOF/TOF, LIFT & Intact Proteins (ISD)

## Purpose

So far in this study guide, the instrument has mostly been used to weigh whole molecules. This tab explains two more advanced tricks the same MALDI-TOF/TOF instrument can do: breaking a peptide apart on purpose so you can read its sequence from the pieces, and reading a long stretch of a whole protein's sequence without cutting it into peptides at all. Both tricks rely on the same physics of flight time, so understanding one helps you understand the other.

## Key ideas

### How breaking a peptide apart actually produces a readable spectrum

In the first flight tube, called TOF1, ions separate out by mass the normal way: lighter ions arrive first, heavier ions arrive later. While this is happening, some peptide ions break apart on their own (called laser-induced decay, or LID), or are made to break apart on purpose by colliding with a gas such as argon (called collision-induced decay, or CID). The key physical fact is this: a fragment and the parent ion it broke off from keep travelling at exactly the same speed as each other, because splitting apart mid-flight changes an ion's mass but not its speed.

A gate called the PCIS (PreCursor Ion Selector) uses that fact to pick out one specific peptide from a whole mixture. It lets through only the chosen parent ion and the fragments still travelling at its speed, and blocks everything else. Anything not travelling at the parent's speed never makes it through the gate.

The ions that pass through the PCIS then enter the LIFT cell (a second ion source) for reacceleration. This step exists because a lighter fragment, moving at the same speed as its heavier parent, carries proportionally less kinetic energy (the energy of motion), not less speed. Left alone, the small fragments would arrive at the detector with too wide a spread of energies to all be captured sharply at one fixed reflector voltage. The LIFT cell gives every surviving ion an extra push of voltage, which brings even the lightest fragment's energy back up close to the same share as the parent's. That way the whole fragment spectrum can be read at once, at a single fixed reflector voltage, instead of scanning through many different voltages.

### Reading a whole protein's sequence without digesting it first (ISD)

Normally, to identify a protein you cut it into peptides first and read those (this is called tryptic digestion, and it is covered elsewhere in this guide). But this instrument can also read a long stretch of sequence directly off a whole, undigested protein, through a phenomenon called in-source decay, or ISD. Some of the protein's backbone bonds spontaneously break apart right in the ion source, before the ions even start flying. This produces two separate ladders of fragments in the resulting spectrum: one ladder counting in from the protein's N-terminus (the start of the chain) and one counting in from its C-terminus (the end of the chain). Reading the gap between two neighbouring rungs on either ladder tells you the mass, and so the identity, of the amino acid at that position.

Getting a good ISD spectrum needs a different recipe from a normal peptide measurement:

- **Matrix**: sinapinic acid or DHAP (2,5-dihydroxyacetophenone). DHAP crystallizes as a ring around the rim of the dried droplet rather than evenly across the whole spot, so when using DHAP, the usual "random walk" shooting pattern (which spreads laser shots evenly across a spot) is switched off, and shots are aimed only inside that ring.
- **Linear mode**, not reflector mode, the same choice made elsewhere in this guide for large, fragile molecules.
- **High laser power**, around 70%, and many shots, around 5,000, moving the laser around the spot as you go to build up that many shots.

Reading the ladder out in software (rather than just eyeballing the raw spectrum) uses the instrument software's own ISD tools: the spectrum is permanently marked as ISD-type before MS/MS processing can begin; a "TDS mascot search" (top-down sequencing) is run with no enzyme selected, no carbamidomethylation, a loose 50 ppm mass tolerance, and the instrument set to MALDI-ISD; and a dedicated annotation mode reads the ladder out amino acid by amino acid. One real wrinkle: ISD does not break the protein backbone at proline, so a proline in the sequence shows up as a missing rung rather than a wrong one.

## Worked example

**The LIFT reacceleration math.** A parent ion of 1000 Da, accelerated at 8 kV in the first ion source, ends up with a kinetic energy of 8 keV (call that 100%). A 100 Da fragment of that same parent comes out of the first flight tube with only 10% of that energy, 0.8 keV, because it is moving at the same speed but carries only a tenth of the mass.

After a 19 kV LIFT reacceleration, the parent's energy becomes 27 keV (still counted as 100%), and the small 100 Da fragment's energy becomes 19.8 keV, about 73% of the parent's energy. That is close enough, across the whole range of fragment masses, for one fixed reflector voltage to capture the entire fragment spectrum in one go. Without the LIFT step, that same 100 Da fragment would have stayed at only 10% of the parent's energy, far too different to be captured sharply alongside the parent and the other fragments.

**Why this matters for reading real spectra.** The peptide FQSEEQQQTEDELQDK loses 98 Da (H3PO4, phosphoric acid) when it is fragmented this way in MS/MS. That kind of loss is a classic sign of phosphorylation, because a phosphate group readily falls off as neutral phosphoric acid during fragmentation. This same peptide and the same phosphorylation show up again elsewhere in this guide, but spotted from the opposite direction: as a +80 Da mass increase on the whole, unfragmented peptide rather than a 98 Da loss after fragmentation. Both are two sides of the same diagnostic coin.

## Figure

A figure (The LIFT cell brings a small fragment's energy share from 10% up to about 73% of its parent's, close enough for one reflector voltage to capture the whole fragment spectrum at once, based on the "TOF/TOF, LIFT & Intact Proteins (ISD)" tab of the MALDI-TOF Study Guide.) appears in the illustrated HTML version of this guide. Alt text: A diagram showing a 1000 Da parent ion and a 100 Da fragment, each with their kinetic energy before and after the LIFT cell's 19 kV reacceleration, showing the fragment's energy share rising from 10% to about 73% of the parent's.

## Common misconceptions

- **"Breaking a peptide apart changes how fast the pieces fly."** It does not. A fragment and the parent ion it came from travel at the same speed; only their energy and mass differ, because speed only changes when fragmentation happens before the first acceleration, not mid-flight.
- **"The LIFT cell is just there to speed everything up."** Its real job is narrower: it corrects an energy mismatch. Without it, light fragments would arrive with too little energy relative to heavy fragments for one fixed reflector voltage to focus them all sharply.
- **"ISD is just a worse version of normal digestion."** ISD answers a different question. Normal digestion identifies a protein by matching many small peptide masses to a database. ISD reads a direct sequence ladder off one intact protein, which is useful for checking things digestion cannot easily show, such as whether a specific end of the protein chain still carries an N-terminal or C-terminal modification.
- **"A gap in an ISD ladder always means a sequencing error."** Not always: ISD does not cleave the backbone at proline, so a true gap at a proline position is expected and is accounted for by the annotation software, not a sign that something went wrong.

## Self-check questions

1. Why do a fragment and its parent ion arrive at the PCIS gate at the same speed?
2. What problem does the LIFT cell's 19 kV reacceleration solve, and why can it not simply be skipped?
3. In the worked example, what percentage of the parent's kinetic energy does the 100 Da fragment carry before and after the LIFT step?
4. What does ISD let you read that a normal tryptic digestion cannot?
5. Why does a proline residue show up as a missing rung rather than a wrong one in an ISD ladder?

### Answers

1. Fragmentation happens mid-flight, after acceleration, and splitting apart changes an ion's mass but not its speed.
2. It solves the problem that a lighter fragment carries proportionally less kinetic energy than its heavier parent even though it moves at the same speed; without reacceleration, fragments would arrive with too wide a spread of energies to all be focused at one fixed reflector voltage.
3. Before LIFT: 10% (0.8 keV out of 8 keV). After the 19 kV LIFT step: about 73% (19.8 keV out of 27 keV).
4. ISD lets you read a direct N-terminal and C-terminal sequence ladder off a whole, undigested protein, including end-of-chain modifications such as an N-terminal acetyl or pyroGlu group, or a missing C-terminal lysine.
5. Because ISD does not break the protein backbone at the proline amino acid, so that position simply never produces a rung in the ladder, rather than producing an incorrect one.

## What to take forward

A fragment keeps its parent's speed, not its parent's energy, and the LIFT cell exists purely to fix that energy mismatch so the whole fragment spectrum can be read at one fixed voltage; the next tab builds on this same mass-shift way of thinking to read sugar chains on glycopeptides.

## Glossary terms introduced

- TOF1: the first flight tube in a TOF/TOF instrument, where ions first separate out by mass.
- Laser-induced decay (LID): a peptide ion breaking apart on its own, without being deliberately collided with a gas.
- Collision-induced decay (CID): a peptide ion being made to break apart by colliding with a gas such as argon.
- PCIS (PreCursor Ion Selector): a gate that lets through only one chosen parent ion and its matching fragments, blocking everything else.
- LIFT cell: a second ion source that reaccelerates fragments so they can all be read at one fixed reflector voltage.
- Kinetic energy: the energy an object has because it is moving; it depends on both mass and speed.
- In-source decay (ISD): spontaneous breaking of a protein's backbone bonds in the ion source, before the ions start flying, which produces readable sequence ladders from an intact protein.
- N-terminus / C-terminus: the start and end, respectively, of a protein's amino acid chain.
