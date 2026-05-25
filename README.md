# Conformational Gating of an Active-Site Loop Governs Phenolic and Aromatic Amine Substrate Selectivity in Fungal Laccase

**Anushka Biswas and Mithun Radhakrishna**

This repository contains the data, parameters, and analysis objects associated with the manuscript:

> *Conformational Gating of an Active-Site Loop Governs Phenolic and Aromatic Amine Substrate Selectivity in Fungal Laccase*

---

## Repository Structure

```
LAC_conformational-gating/
├── ligands/
│   ├── parameters/          # GAFF2 force field parameters for each ligand
│   └── structure/           # 3D ligand structures from PubChem (SDF)
├── mcpbpy/                  # Metal center parameters (MCPB.py output)
├── msm/
│   ├── intermediate-poses/  # 189 representative protein conformations (PDB)
│   └── scripts/             # Serialized MSM and clustering objects
└── supplementary_videos/    # Supplementary Movies S1 and S2
```

---

## Contents

### `ligands/`

Force field parameters and 3D structures for the ten substrates studied:

| Ligand | PubChem CID |
|--------|------------|
| Aniline | 6115 |
| 2,5-Xylidine | 11994988 |
| Benzene | 241 |
| Phenol | 996 |
| Catechol | 289 |
| Resorcinol | 7259 |
| Hydroquinone | 785 |
| Pyrogallol | 1057 |
| Phloroglucinol | 359 |
| Hydroxyquinol | 10787 |

- **`parameters/`** — Per-ligand subdirectories containing GAFF2 force field parameters generated via ACPYPE and Gaussian 09 geometry optimization (B3LYP/6-31G\*).
- **`structure/`** — Conformer SDF files downloaded from PubChem, used as starting geometries for parameterization.

---

### `mcpbpy/`

MCPB.py (Metal Center Parameter Builder, AmberTools23) output files for the four copper centers of laccase:

- **`.mol2` files** — Atom-typed structures for Cu1, Cu2, Cu3, Cu4 (T1 blue copper and T2/T3 trinuclear cluster), and coordinating residues (histidines, cysteine, CX1).
- **`.frcmod` files** — AMBER force field modification files encoding bonded and non-bonded parameters for each copper coordination sphere.

These files are required to reproduce the GROMACS topology for the copper-containing enzyme system.

---

### `msm/`

Markov State Model (MSM) data for the conformational analysis of Loop-1.

#### `intermediate-poses/`

189 representative PDB structures (`pose1.pdb` – `pose189.pdb`) covering the conformational space of the active-site loop sampled across all MD trajectories. These poses contain the enzyme (protein + CU ions) and the bound ligand (residue name `UNK`), with solvent removed. They were used as the structural basis for MSM featurization and clustering.

The poses span:
- **Catechol** MD trajectories (poses 1–43): 43 independent simulations
- **Hydroquinone, Xylidine, Resorcinol** trajectories (poses 44–60): extracted from earlier docking-initiated MD
- **Benzene, Cat+Xyl, Hydroxyquinol, Phloroglucinol** trajectories (poses 61–200 in the full set): evenly-spaced snapshots from µs-scale simulations

#### `scripts/`

- **`clustering.pkl`** — Serialized `sklearn`/PyEMMA k-means clustering object defining the MSM microstates.
- **`pyemma.pkl`** — Serialized PyEMMA MSM object, including the transition probability matrix, stationary distribution, and TICA coordinates. Load with:

```python
import pickle, pyemma

with open("scripts/pyemma.pkl", "rb") as f:
    msm = pickle.load(f)

with open("scripts/clustering.pkl", "rb") as f:
    clustering = pickle.load(f)
```

---

### `supplementary_videos/`

- **`Movie-S1.mp4`** — MD trajectory showing Loop-1 conformational transitions in the apo enzyme.
- **`Movie-S2.mp4`** — Overlay of representative MSM macrostate structures illustrating the three principal loop conformations (Conf1, Conf2, Conf3).

---

## Software and Versions

| Software | Version | Use |
|----------|---------|-----|
| GROMACS | 2023.3 | MD simulations |
| AmberTools (MCPB.py) | 23 | Copper center parameterization |
| ACPYPE web server | — | Ligand GAFF2 parameterization |
| Gaussian 09 | — | Ligand geometry optimization and RESP charges |
| H++ | 3.0 | Protein protonation at pH 5 |
| PROPKA | 3.5.0 | pKa prediction |
| AutoDock Vina | — | Molecular docking |
| PyEMMA | 2.5.12 | MSM construction and analysis |
| Python | 3.10 | Analysis scripts |
| VMD | 1.9.4 | Trajectory visualization |
| UCSF Chimera | 1.18 | Structure preparation and visualization |
| ColabFold | — | Mutant structure prediction |

---

## Citation

If you use data or methods from this repository, please cite:

> Biswas A., Radhakrishna M. *Conformational Gating of an Active-Site Loop Governs Phenolic and Aromatic Amine Substrate Selectivity in Fungal Laccase.* (2025) *(in preparation / under review)*

---

## Contact

**Anushka Biswas** — anushkabiswas@iitgn.ac.in  
Indian Institute of Technology Gandhinagar
