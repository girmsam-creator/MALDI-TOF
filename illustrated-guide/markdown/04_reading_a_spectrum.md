# Reading a Spectrum

## Purpose

Once a sample has been spotted and measured, the instrument hands you a spectrum: a graph of masses and how strongly each one was detected. Everything you will ever conclude about a sample, from "which protein is this" to "did the run work at all," comes from reading that graph correctly. This tab teaches you the real features you will see on every spectrum from this instrument, using the lab's own calibration-standard numbers, so you can tell a trustworthy peak from a misleading one.

## Key ideas

### The two axes

Every MALDI-TOF spectrum has the same two axes, and reading them correctly is most of what you need to know to use the instrument.

- **X-axis: m/z (mass-to-charge ratio), measured in Daltons (Da).** For almost every MALDI ion, this is simply the mass, because almost every ion produced by this method carries a single positive charge. Further right on the axis means a heavier molecule.
- **Y-axis: intensity**, in arbitrary units called counts. A taller peak means more ions of that mass arrived at the detector. Importantly, peak height tells you how abundant and how easily-ionized a molecule is, not how biologically important it is. A very abundant, easily-ionized protein can completely overshadow a rarer one that matters much more to your question.

### Baseline, noise, and resolution

The wavy or grainy line running along the bottom of a spectrum, between the real peaks, is chemical and electronic noise, not signal. Software removes this automatically (called baseline correction) before it tries to find peaks, but a very noisy baseline is itself a warning sign of a poor-quality spot (tab 5 covers this in detail).

A peak's sharpness tells you about resolution: the instrument's ability to tell two close masses apart. A sharp, narrow peak means close masses were well separated; a broad, fat peak means they were not, and two truly different peaks might be blurred into one bump. Reflector mode gives noticeably better resolution than linear mode, at the cost of being less sensitive to very large molecules, which is why the choice between the two modes is a real decision every time you set up a method.

### Isotope patterns

Every peak is technically a small cluster of isotope peaks, spaced roughly 1 Da apart because of naturally occurring heavier isotopes such as carbon-13. At the resolution typically used for large proteins in linear mode, these isotopes blur into one broad peak. Only for smaller, well-resolved molecules, roughly under 3,000 Da and measured in reflector mode, will you actually see the individual isotope "teeth."

### Charge state

A peak's position on the x-axis tells you m/z, not mass. If an ion happens to carry two charges instead of one, it shows up at roughly half its true mass, because the charge number divides the mass. A real example from this lab's own calibration standards: Protein A (from Protein Standard II) appears at m/z 44,613 as a singly-charged [M+H]+ ion, and again at roughly m/z 22,307 as a doubly-charged [M+2H]2+ ion, almost exactly half of the first value. Spotting a pair of peaks like this, where one sits at roughly half the m/z of the other, is a useful sanity check that you are reading the spectrum correctly.

### Calibrating a spectrum before you trust it

Before any mass on a spectrum can be trusted, the spectrum has to be calibrated against peaks of known mass. In this lab that usually means a Peptide Calibration Standard II spectrum (eight peptides, 700 to 3,500 Da) for peptide work, or a Protein Calibration Standard I spectrum (four proteins, 4,000 to 20,000 Da) for intact proteins, measured on a calibrant spot right next to the sample.

The calibration sequence in flexAnalysis, the software used to process spectra from this instrument, is always the same four clicks: open the calibrant spectrum, then Calibrate, Internal, Automatic assign, Calibrate. Once each real peak has been matched to its known mass and the errors look acceptable, click Calibrate, Copy calibration, select the sample spectra, then Calibrate, Replace calibration to apply that same calibration to them.

You also have to pick how peaks are found in the first place. flexAnalysis offers two peak-picking algorithms: Centroid, which reports a peak's whole average mass and is used for larger molecules whose individual isotopes cannot be separated, and Snap, which reports the monoisotopic mass (the lightest isotope peak in the cluster) and is used once isotopes are resolved, as they typically are for peptides. Picking the wrong one for your mass range quietly shifts every mass you report.

## Worked example

Resolution is not an abstract number: it changes what you can actually see in the exact same sample. Take Cytochrome C, average mass 12,360.97 Da, one of the four proteins in Protein Calibration Standard I.

1. Run it in **linear mode**. The resolution is around **1,500**. On screen this looks like one broad hump: the individual isotope peaks exist in theory, but they blur into a single unresolved envelope.
2. Run the exact same protein, same sample, in **reflector mode**. The resolution jumps to around **30,000**. Now the isotopes separate into individual, countable teeth.
3. Nothing about the sample changed between these two runs, only the instrument mode. That is the whole lesson: resolution is something the method gives you, not something fixed by the molecule alone.

This is also why choosing linear versus reflector mode is a real, consequential decision every time a method is set up, not just a textbook distinction.

## Figure

A side-by-side comparison figure (Cytochrome C in linear mode, resolution about 1,500, one broad hump; versus reflector mode, resolution about 30,000, separated isotope teeth) appears in the illustrated HTML version of this guide.

## Common misconceptions

- **"A taller peak is a more important molecule."** Peak height mainly reflects how abundant and how easily-ionized a molecule is, not its biological significance. A highly abundant protein can dwarf a rarer, more diagnostically useful one.
- **"The x-axis number is the mass."** It is technically m/z. This only equals the mass in practice because almost every MALDI ion carries a single charge; a doubly-charged ion will not sit at its true mass.
- **"More charges means the peak moves further right."** The opposite is true: more charges divide the m/z, so a doubly-charged ion appears at roughly half the m/z of the same molecule singly charged.
- **"You should always be able to see individual isotope peaks."** You only see them for smaller molecules (roughly under 3,000 Da) measured in reflector mode. Large proteins in linear mode show one blurred hump instead, and that is expected, not a failure.

## Self-check questions

1. What does the y-axis of a MALDI-TOF spectrum actually measure, and what does a taller peak tell you (and not tell you) about a molecule?
2. A protein's singly-charged peak sits at m/z 44,613. Roughly where would you expect its doubly-charged peak to sit, and why?
3. Why does Cytochrome C show one broad hump in linear mode but separated isotope teeth in reflector mode, even though it is the exact same sample?
4. What is the difference between the Centroid and Snap peak-picking algorithms in flexAnalysis, and when is each one appropriate?
5. What are the four clicks used to calibrate a spectrum in flexAnalysis, and what has to happen before you apply that calibration to your sample spectra?

### Answers

1. It measures intensity, in arbitrary count units, which reflects how many ions of that mass arrived at the detector. A taller peak means a more abundant or more easily-ionized molecule, not necessarily a biologically more important one.
2. Roughly m/z 22,307, about half of 44,613, because a doubly-charged ion's mass is divided by its charge number (z = 2).
3. The sample did not change, only the mode. Reflector mode gives much higher resolution (about 30,000, versus about 1,500 in linear mode), which is high enough to separate the isotope peaks that linear mode blurs into one hump.
4. Centroid reports the whole peak's average mass and is used for larger molecules whose isotopes cannot be resolved; Snap reports the monoisotopic (lightest isotope) mass and is used once isotopes are resolved, as is typical for peptides.
5. Calibrate, Internal, Automatic assign, Calibrate on the calibrant spectrum. Once the matched peaks show acceptable errors, you then use Calibrate, Copy calibration, then select the sample spectra and use Calibrate, Replace calibration.

## What to take forward

Before trusting any number on a spectrum, make sure you know whether you are reading m/z or true mass (watch for charge state), and make sure the spectrum has actually been calibrated against peaks of known mass.

## Glossary terms introduced

- **m/z (mass-to-charge ratio):** the quantity plotted on a spectrum's x-axis; equals mass only when the ion carries a single charge.
- **Intensity:** the quantity plotted on a spectrum's y-axis; how many ions of a given mass were detected.
- **Baseline:** the background noise level a spectrum sits on; software subtracts it out before picking peaks.
- **Resolution:** a measure of how well an instrument separates two close masses; higher numbers mean sharper, better-separated peaks.
- **Isotope peak:** one of a small cluster of peaks, about 1 Da apart, caused by naturally occurring heavier isotopes of the same molecule.
- **Charge state:** how many charges an ion carries; a higher charge state divides its position on the m/z axis.
- **Monoisotopic mass:** the mass of the lightest isotope peak in a cluster.
- **Centroid:** a peak-picking method that reports a peak's whole average mass.
- **Snap:** a peak-picking method that reports the monoisotopic mass once isotopes are resolved.
- **Calibration:** matching real peaks to known masses so the rest of a spectrum's masses can be trusted.
