# Glossary

Every technical term introduced anywhere in this guide, in one alphabetical list. Each entry also names the tab where it first appears, so you can jump back for the full context and worked example.

**AnchorChip / BigAnchor / SmallAnchor:** target plate formats with small, chemically treated anchor spots of different sizes that concentrate a sample for a stronger, sharper signal. (Mechanism; LC-MALDI)

**Anaerobic bacteria:** bacteria that grow only in environments without oxygen, traditionally slow to identify by biochemical methods. (Other Organisms)

**Archaea:** a domain of single-celled organisms chemically distinct from bacteria, including different lipids and no true peptidoglycan cell wall. (Other Organisms)

**Autolysis peak (trypsin autolysis peak):** a peak coming from the digestion enzyme itself, not the sample protein. The three to recognize on this instrument are m/z 842, 1,045, and 2,678, and they are excluded from the real peptide list before a search. (Errors; Case Study: PMF; Test Your Knowledge)

**AutoXecute:** the flexControl feature that runs an automated measurement sequence across a whole plate. (Case Study: PMF)

**b-ion / y-ion:** the two families of fragment ions produced when a peptide backbone breaks, read from the N-terminal or C-terminal end respectively. (Case Study: PMF)

**Baseline:** the background noise level a spectrum sits on; the software subtracts it out before picking peaks. (Reading a Spectrum)

**Biotyper:** Bruker's clinical system for identifying bacteria by matching a whole-cell MALDI fingerprint against a reference library. (Other Applications)

**Bottom-up proteomics:** identifying and studying proteins by first cutting them into peptides, then measuring those peptides. (Proteomics and PTMs)

**C18:** a common non-polar column material used in reversed-phase liquid chromatography to separate molecules by hydrophobicity. (LC-MALDI)

**Calibrant:** a substance of known, exact mass spotted alongside a sample so the instrument's mass readings can be corrected against it. (Sample Prep)

**Calibration:** matching real peaks to known masses so the rest of a spectrum's masses can be trusted. (Reading a Spectrum)

**Calibration drift:** when a calibrant peak's measured mass no longer matches its known mass closely enough to trust, the most common cause of a bad result. (Errors)

**Calibration error:** how far off an instrument's mass readings are from their true values, usually measured in parts per million (ppm). (More Worked Examples)

**Carbamidomethyl (C):** a fixed, global modification applied to every cysteine in a search, accounting for the alkylation step in sample preparation. (Case Study: PMF)

**Carbapenemase:** a bacterial enzyme that breaks open a carbapenem antibiotic's ring, making the bacterium resistant to that drug. (Proteomics and PTMs)

**Cell line:** a population of cells, often from one original source, grown and maintained in culture for research. (Other Organisms)

**Centroid vs Snap:** two peak-picking modes in flexControl; Centroid reports a peak's whole average mass, Snap reports the monoisotopic mass once isotopes are resolved. (Sample Prep; Reading a Spectrum)

**Charge state:** how many charges an ion carries; a higher charge state divides its position on the m/z axis. (Reading a Spectrum)

**Charge-state deconvolution:** working out how many charges an ion carries so its true mass can be calculated from its m/z. (Alternative Methods)

**Co-crystallization:** the process of the matrix and sample crystallizing together evenly as a spot dries. (Mechanism)

**Collision-induced decay (CID):** a peptide ion being made to break apart by deliberately colliding it with a gas such as argon. (TOF/TOF, LIFT and ISD)

**Collision cross section (CCS):** a measure of an ion's size and shape, used by ion mobility methods to separate molecules of the same mass but different shape. (Alternative Methods)

**Cross-contamination (cell lines):** when a cell culture becomes mixed with or overtaken by cells from a different line without the researcher noticing. (Other Organisms)

**Cross-ring cleavage:** a sugar ring breaking apart internally rather than at the bond connecting it to its neighbour, producing smaller, characteristic mass gaps. (Glycopeptides)

**Dalton (Da):** the unit of mass used throughout this guide for peptides, proteins, and mass differences; one Dalton is about the mass of one hydrogen atom. (Cheat Sheet)

**Desorption/ionization:** the moment the laser's energy vaporizes part of the sample-matrix crystal and gives some molecules an electrical charge. (Overview)

**Detector gain:** the amplification setting of the ion detector; it needs re-adjusting if its voltage drifts too far from its previous setting. (Sample Prep; Errors)

**DNA barcode gene:** a short, standardized gene region used to tell species apart genetically. (Other Organisms)

**Dried droplet method:** the common sample prep method of mixing matrix and sample in solution and letting the drop dry on the plate. (Mechanism)

**Electron ionization:** an ionization method that uses a beam of high-energy electrons, producing highly reproducible fragmentation, used in GC-MS. (Alternative Methods)

**Electrospray ionization (ESI):** a method that sprays a liquid sample into charged droplets to ionize it, often producing ions with more than one charge. (Alternative Methods)

**Eluate:** the liquid coming off a chromatography column, carrying the separated molecules with it. (LC-MALDI)

**End cap:** a chemical group attached to the end of a polymer chain, with its own fixed mass. (Other Applications)

**False discovery rate (FDR):** an estimate of how many of the reported matches in a database search are likely wrong, usually kept below a set limit such as 1 percent. (Alternative Methods)

**Feature matrix:** a table with one row per sample and one column per peak, used as the input to matching or classification. (R and Python)

**Filamentous fungi:** mold-forming fungi that grow as branching thread-like structures, harder to identify by MALDI-TOF than yeast because reference databases cover them less completely. (Other Organisms)

**Fragmentation Coverage:** the percentage of a theoretical fragment pattern that actually appears in a spectrum. (More Worked Examples)

**FT-ICR-MS:** a technique that measures mass using a magnetic field instead of a flight tube, for extremely high precision. (Mechanism)

**Glycopeptide:** a peptide with a sugar chain (glycan) attached at a specific site. (Glycopeptides)

**Half-moon effect:** a visible crystallization failure pattern caused by too much organic solvent drying the spot too fast. (Errors)

**Hard ionization:** an older, rougher ionization method (such as electron beam bombardment) that destroys fragile molecules. (Mechanism)

**Hexose, HexNAc, sialic acid (NeuAc):** three types of sugar units commonly found in glycan chains, each with its own fixed mass contribution. (Glycopeptides)

**In-source decay (ISD):** a technique that reads a ladder of fragments directly off an intact protein, spontaneously breaking its backbone in the ion source before the ions start flying, without digesting it first. (Overview; TOF/TOF, LIFT and ISD)

**Intact-cell MALDI:** a MALDI-TOF measurement taken on whole, unlysed cells rather than a digested or extracted sample. (Other Organisms)

**Intensity:** the quantity plotted on a spectrum's y-axis; how many ions of a given mass were detected. (Reading a Spectrum)

**Intensity Coverage:** the percentage of a spectrum's total signal intensity that a proposed match actually accounts for. (More Worked Examples)

**Ion ladder:** a series of fragment peaks, each one amino acid's mass apart, used to read a protein's sequence from one end. (More Worked Examples)

**Ion-mobility TOF (IMS-TOF-MS):** a coupled technique that separates ions by shape as well as mass. (Mechanism)

**Ion suppression:** when high-abundance molecules dominate ionization and hide low-abundance ones in the same spectrum, unless the mixture is separated first. (LC-MALDI; Test Your Knowledge)

**Isobaric:** having the same total mass, so labeled peptides from different samples overlap in the plain MS spectrum until fragmented. (LC-MALDI)

**Isotope peak:** one of a small cluster of peaks, about 1 Da apart, caused by naturally occurring heavier isotopes of the same molecule. (Reading a Spectrum)

**iTRAQ:** an isobaric labeling method that lets up to 8 samples be compared in a single MS run. (LC-MALDI)

**Kinetic energy:** the energy an object has because it is moving; it depends on both mass and speed. (TOF/TOF, LIFT and ISD)

**LIFT:** on this instrument, the naming convention and the physical cell used to reaccelerate fragment ions so a whole MS/MS spectrum can be read at one fixed reflector voltage. (Sample Prep; Case Study: PMF; TOF/TOF, LIFT and ISD)

**Linear mode / Reflector (reflectron) mode:** two ways of timing ion flight. Linear mode sends ions straight to a detector at the tube's end and is needed for very large, intact molecules. Reflector mode bounces ions off an electric mirror back to a detector near the source, giving sharper, more accurate peaks, but only works well for smaller molecules. (Overview; Mechanism; Glycopeptides)

**Liquid chromatography (LC):** a technique that separates molecules in a mixture by pumping them through a column that holds some of them back more than others. (LC-MALDI)

**Log(Score):** the confidence number a Biotyper-style result reports for each candidate match; higher means more reliable. (Other Applications)

**MALDI-TOF:** Matrix-Assisted Laser Desorption/Ionization, Time-Of-Flight mass spectrometry: a technique that uses a laser and a light-absorbing matrix to turn a biological sample into flying ions, then measures their masses by timing their flight. (Overview)

**MALDIquant:** an R package purpose-built for importing, preprocessing, and analyzing MALDI-TOF spectra. (R and Python)

**MASCOT ions score:** the confidence score MASCOT assigns to a search hit, compared against a significance threshold to decide if an identification is trustworthy. (Errors)

**Mass accuracy:** how close the instrument's reported mass is to the true mass, often given in parts per million (ppm). (Overview)

**Mass discrimination:** the instrument's built-in tendency to detect light ions more easily than heavy ones, even when equal amounts are present. (Mechanism)

**Matrix:** a small, light-absorbing chemical mixed with the sample that protects it from the laser's energy and helps it become charged. (Overview)

**Metabolomics:** the study of small molecules (metabolites) in a sample, such as sugars, lipids and amino acids, using mass spectrometry. (Other Applications)

**MH+:** the mass of a molecule plus one added proton, the form in which it is usually measured and reported in positive-ion MALDI. (Glycopeptides)

**Monoisotopic mass:** the mass of the lightest isotope peak in a cluster. (Reading a Spectrum)

**Multiply charged ion:** an ion carrying more than one charge, which makes its m/z value lower than its true mass. (Alternative Methods)

**Mycoplasma:** a cell-wall-free bacterium that commonly and silently contaminates laboratory cell cultures. (Other Organisms)

**m/z (mass-to-charge ratio):** the value plotted on a spectrum's x-axis; equals mass divided by the number of charges on the ion, so it equals mass itself only when the ion carries a single charge. (Overview; Reading a Spectrum)

**Near-neighbour calibration:** calibrating a sample spectrum using the calibrant spot or calibration fit physically closest to it, for the best accuracy. (Sample Prep; Case Study: PMF)

**Neutral loss:** a small, uncharged chemical group (such as phosphoric acid) breaking off a peptide during fragmentation, seen as a drop in mass rather than a separate charged peak. (Proteomics and PTMs; More Worked Examples)

**N-terminus / C-terminus:** the start and end, respectively, of a protein's amino acid chain. (TOF/TOF, LIFT and ISD)

**Oxidation (M):** an optional, variable modification allowed on methionine in a search, since oxidation during handling is not guaranteed to have happened. (Case Study: PMF)

**Oxonium ion:** a small, positively charged, sugar-only fragment (for example at 204 Da or 366 Da) that appears at a fixed mass regardless of which protein it came from, used to flag a glycopeptide spectrum. (Glycopeptides; Cheat Sheet)

**PCIS (PreCursor Ion Selector) window:** a gate, with a mass window set around it, that lets through only one chosen parent ion and its matching fragments before LIFT MS/MS measurement, blocking everything else. (Case Study: PMF; TOF/TOF, LIFT and ISD)

**Percent identity:** in sequencing-based identification, how closely a DNA read matches a reference sequence, expressed as a percentage. (Alternative Methods)

**Peptide mass fingerprint / PMF (peptide mass fingerprinting):** identifying a protein by matching the masses of its digested peptides, or the set of masses from its digested fragments, against a database. (Overview; Case Study: PMF; Proteomics and PTMs; More Worked Examples)

**PMF search tolerance:** how far, in Da, a measured peptide mass is allowed to differ from a database value during a peptide mass fingerprint search. (Errors)

**Post-translational modification (PTM):** a small chemical change added to a protein after it has been built. (Proteomics and PTMs)

**ppm (parts per million):** the unit used to express a small measurement error, such as calibration error or a search tolerance, as a fraction of the measured mass. (Errors; Cheat Sheet)

**Principal component analysis (PCA):** a method that compresses many correlated measurements (such as peak intensities) into a smaller number of combined components. (R and Python)

**Random Walk:** a flexControl setting that moves the laser automatically around a spot during measurement. (Errors)

**Reference library / database:** the stored collection of known spectral fingerprints that a new MALDI-TOF measurement is matched against. (Other Organisms)

**Repeat unit:** the small chemical unit that repeats many times to build up a polymer chain, each one adding the same fixed mass. (Other Applications)

**Resolution:** how finely the instrument can tell apart two very close masses; higher numbers mean sharper, better-separated peaks. (Overview; Reading a Spectrum)

**Resolving power:** another name for resolution, used when comparing TOF against other instrument types such as Orbitrap or FT-ICR. (Alternative Methods)

**Retention index:** a standardized, more reproducible version of a GC-MS peak's retention time. (Alternative Methods)

**Retention time:** how long a molecule takes to travel through and come off an LC column. (LC-MALDI)

**Reversed-phase:** an LC setup where more hydrophobic molecules stick to the column longer and come off later. (LC-MALDI)

**Ribosomal proteins:** highly abundant proteins that are part of a cell's protein-building machinery, useful for whole-cell fingerprinting. (Other Applications)

**Signal-to-noise (S/N) ratio or threshold:** the minimum ratio of peak height to background noise the software requires before it will count something as a real peak. (Sample Prep; LC-MALDI; R and Python)

**SILAC / ICPL:** quantitation labeling methods whose signal is visible already at the plain MS level, limited to comparing 4 samples at once. (LC-MALDI)

**Surface-enhanced Raman spectroscopy (SERS):** a version of Raman spectroscopy boosted with metal nanoparticles to make a weak signal detectable. (Alternative Methods)

**TA30:** the standard solvent used for the HCCA matrix, 30 percent acetonitrile and 70 percent 0.1 percent TFA in water. (Sample Prep)

**Target plate:** the metal plate with many spots where matrix-sample mixtures are deposited and dried before measurement. (Sample Prep)

**Time-of-flight (TOF):** the part of the instrument where ions travel through a vacuum tube and get sorted by how fast they move, which depends on their mass and charge. (Overview)

**TOF1:** the first flight tube in a TOF/TOF instrument, where ions first separate out by mass before MS/MS. (TOF/TOF, LIFT and ISD)

**Tolerance window:** the allowed mass difference (for example, plus or minus 2 Da) when deciding whether an observed peak matches a reference mass. (R and Python)

**Total ion current (TIC):** the sum of all signal intensity in a spectrum, used as a reference to normalize spectra so different runs are comparable. (R and Python)

**Trypsin:** an enzyme that reliably cuts a protein chain right after every lysine or arginine, used to produce measurable peptides. (Proteomics and PTMs)

**WARP-LC:** the automated software that manages an LC-MALDI run, tracking peptides across spots and scheduling MS/MS. (LC-MALDI)

**ZipTip:** a small pipette-tip device (commonly C18) used to desalt or clean up a sample before trying MALDI again. (Sample Prep; Errors)
