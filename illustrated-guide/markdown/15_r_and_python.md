# Analyzing with R & Python

## Purpose

Every step a researcher does by hand in ProteinScape or flexAnalysis, smoothing a spectrum, removing its wavy noise floor, matching peaks against a reference list, can also be written as code. Learning to read that code, even without being able to write it from scratch yet, means you can see exactly what a "preprocessing step" actually does to the numbers, and reuse the same steps on hundreds of spectra instead of one at a time.

## Key ideas

**R has a purpose-built toolkit for this exact job.** The package **MALDIquant** (with **MALDIquantForeign** for reading vendor files such as Bruker's) walks through the same stages described earlier in this guide:

1. Import raw spectra.
2. Stabilize variance, then smooth to reduce noise (using a method called Savitzky-Golay smoothing).
3. Remove the baseline, the wavy noise floor described in the "Reading a Spectrum" tab.
4. Normalize so different runs are comparable (using total ion current, TIC).
5. Align spectra to a common m/z scale, since small calibration drift between runs would otherwise look like real differences.
6. Detect peaks, using a signal-to-noise ratio (SNR) threshold.
7. Bin peaks across all samples so the same biological peak lines up at the same position in every sample, even with tiny mass shifts.
8. Reshape the result into one row per sample, one column per peak, called a feature matrix, ready for matching or classification.

**Python does the same job with general-purpose tools instead of one dedicated package.** The scientific stack **numpy**, **scipy**, and **pandas** performs the same steps (smoothing, a rolling-minimum baseline correction, normalizing by total ion current, then peak detection), which is actually a good way to see what each step does, since there is no single function hiding the details.

**Matching peaks against a reference list is the coding version of work you already do by hand.** Both R and Python can compare an unknown spectrum's peak list against a list of known reference masses within a tolerance window (for example, plus or minus 2 Da), and report what fraction matched, the same logic used throughout this guide's protein identification workflow.

**A simple classifier can learn to tell species or classes apart from peak patterns.** Using the feature matrix idea (one row per sample, one column per binned peak), a method such as PCA (principal component analysis) can compress many peak-intensity columns into a handful of combined components, which a classifier then uses to assign new samples to a class. This is the same basic idea behind the AI and machine-learning spectrum classifiers described in the "Alternative Methods & Future Trends" tab.

**You often do not need a raw spectrum file to get started.** ProteinScape's own result tables (the protein table and the peptide table) can be exported directly to Excel from inside the software, by right-clicking the table. That Excel export, read into R with readxl or into Python with pandas.read_excel, is the natural starting point for most people who want to go further than the on-screen results, rather than starting from a raw spectrum file.

**Which language to reach for depends on the job.** For plain, routine MALDI-TOF spectral processing and classification, R with MALDIquant is the more direct, purpose-built path, since it was written by and for this exact field. For large-scale machine learning, deep learning, or combining spectral data with other data types, Python's broader ecosystem (scikit-learn, PyTorch, pandas) usually pays off. Many labs use both: R for initial spectral quality control, then Python for downstream modeling.

## Worked example

Here is the real peak-matching code from this guide, in Python, explained line by line. It checks a list of observed peaks against five real reference masses from the Peptide Calibration Standard II: 757.3992, 1046.5418, 1296.6848, 1347.7354, and 1619.8223 Da.

```python
import numpy as np

reference = np.array([757.3992, 1046.5418, 1296.6848, 1347.7354, 1619.8223])
observed = peaks_df["mz"].values

# absolute difference between every observed peak and every reference mass
diffs = np.abs(observed[:, None] - reference[None, :])
matched = (diffs <= 2).any(axis=0)  # True/False per reference mass
score = matched.sum() / len(reference)
print(f"{matched.sum()} of {len(reference)} reference peaks matched ({score:.0%})")
```

1. `import numpy as np` loads numpy, the package that handles lists of numbers (arrays) efficiently.
2. `reference = np.array([...])` stores the five known calibration masses as a numpy array, so they can all be compared at once.
3. `observed = peaks_df["mz"].values` pulls the m/z column out of a table of detected peaks (made earlier by a peak-detection step) as a plain array of numbers.
4. `diffs = np.abs(observed[:, None] - reference[None, :])` is the clever part: by reshaping the two arrays, numpy computes the absolute difference between every single observed peak and every single reference mass, all in one step, producing a grid of differences.
5. `matched = (diffs <= 2).any(axis=0)` checks, for each reference mass, whether any observed peak came within 2 Da of it (the matching tolerance). The result is a True or False for each of the five reference masses.
6. `score = matched.sum() / len(reference)` counts how many of the five reference masses were matched, and divides by 5 to get a fraction.
7. The final line prints a sentence such as "5 of 5 reference peaks matched (100%)", in the same way a confidence score is reported for a real identification.

Reading the output: the matching score tells you, in one number, roughly how confident an identification is, the same idea as a Biotyper-style score band, just computed by hand.

## Figure

A figure (The real MALDIquant preprocessing pipeline turns a raw spectrum into a feature matrix ready for matching or classification, based on the "Analyzing with R & Python" tab of the MALDI-TOF Study Guide.) appears in the illustrated HTML version of this guide. Alt text: A six-step vertical pipeline diagram showing a MALDI-TOF spectrum being imported, smoothed and baseline-corrected, normalized, aligned across samples, peak-detected, and finally reshaped into a feature matrix.

## Common misconceptions

- **"You need to be a programmer to benefit from this tab."** Many researchers on this instrument never touch a raw spectrum file in code at all; they export ProteinScape's result tables to Excel and read those into R or Python instead.
- **"Python has one standard MALDI package, like R's MALDIquant."** Python instead relies on general-purpose packages (numpy, scipy, pandas) assembled step by step; there is no single dominant MALDI-specific package the way R has MALDIquant.
- **"Aligning spectra is an optional extra step."** Without aligning spectra to a common m/z scale first, small calibration drift between runs can look like a real biological difference when samples are compared.
- **"A classifier's test accuracy always predicts how it will perform in real use."** How the test set was chosen matters: a random split from the same batch of samples will look better than performance on truly new, later samples, and only the latter shows how the model behaves in practice.

## Self-check questions

1. What is the purpose of aligning spectra to a common m/z scale before comparing samples?
2. Name two of the five real reference masses from the Peptide Calibration Standard II used in the worked peak-matching example.
3. In the Python preprocessing example, what two methods are chained together to build a smoothed, estimated baseline?
4. Why might a lab use R for the early stages of an analysis and Python for the later stages, rather than only one language?
5. What does it mean if a classifier shows high accuracy on a random test split but performs far worse on truly new samples collected later?

### Answers

1. Because small calibration drift between runs can otherwise look like a real difference between samples; alignment makes sure the same biological peak lines up at the same position across all spectra before they are compared.
2. Any two of: 757.3992, 1046.5418, 1296.6848, 1347.7354, 1619.8223 Da.
3. A rolling-minimum filter (`minimum_filter1d`) estimates the baseline, and a uniform (averaging) filter (`uniform_filter1d`) then smooths that baseline estimate itself before it is subtracted.
4. Because R's MALDIquant package is purpose-built for MALDI-TOF spectral processing and encodes a lot of domain best practice, while Python's broader ecosystem (scikit-learn, PyTorch) is usually stronger for large-scale machine learning or combining data types, so labs can use each language for the part it does best.
5. It means the model has not generalized well: its apparent performance came partly from the test samples being too similar to its training samples, and only testing on truly new, later data reveals how it will actually behave in real use.

## What to take forward

The preprocessing steps you do by hand on one spectrum (smoothing, baseline removal, peak detection, matching against a reference) are exactly the steps that get written as reusable code when a project needs to analyze many spectra at once.

## Glossary terms introduced

- MALDIquant: an R package purpose-built for importing, preprocessing, and analyzing MALDI-TOF spectra.
- Total ion current (TIC): the sum of all signal intensity in a spectrum, used as a reference to normalize spectra so different runs are comparable.
- Signal-to-noise ratio (SNR): a threshold used to decide whether a bump in a spectrum is a real peak or just background noise.
- Feature matrix: a table with one row per sample and one column per peak, used as the input to matching or classification.
- Principal component analysis (PCA): a method that compresses many correlated measurements (such as peak intensities) into a smaller number of combined components.
- Tolerance window: the allowed mass difference (for example, plus or minus 2 Da) when deciding whether an observed peak matches a reference mass.
