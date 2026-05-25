# Conformational Gating Governs Substrate Selectivity in Fungal Laccase

This repository contains the input data, structures, parameters, and scipts associated with the manuscript:

> *Conformational Gating of an Active-Site Loop Governs Phenolic and Aromatic Amine Substrate Selectivity in Fungal Laccase*
**Anushka Biswas, Deepshikha Singh, Bhaskar Datta and Mithun Radhakrishna**
---

## Repository Structure

```
LAC_conformational-gating/
├── ligands/
│   ├── parameters/          # GAFF2, Charmm, Amber, and Gromacs force field parameters for each ligand
│   └── structure/           # 3D ligand structures from PubChem (SDF)
├── mcpbpy/                  # Catalytic pocket parameters (MCPB.py output)
├── msm/
│   ├── intermediate-poses/  # 200 representative protein conformations (PDB)
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

- **`parameters/`** — Per-ligand subdirectories containing GAFF2, CHARMM, AMBER & GROMACS force field parameters generated via ACPYPE and Gaussian 09 geometry optimization (B3LYP/6-31G\*).
- **`structure/`** — Conformer SDF files downloaded from PubChem, used as starting geometries for parameterization.

---

### `mcpbpy/`

MCPB.py (Metal Center Parameter Builder, AmberTools23) output files for the four copper centers of laccase:

- **`.mol2` files** — Atom-typed structures for Cu1, Cu2, Cu3, Cu4 (T1 blue copper and T2/T3 trinuclear cluster), and coordinating residues (histidines, cysteine, CX1).
- **`.frcmod` files** — AMBER force field modification files encoding bonded and non-bonded parameters for each copper coordination sphere.

These files are required to reproduce the GROMACS topology for the copper-containing enzyme system.

---

### `msm/`

Markov State Model (MSM) data 

#### `intermediate-poses/`

200 representative PDB structures (`pose1.pdb` – `pose200.pdb`) covering the conformational space of ligand binding mechanisms sampled across all MD trajectories. These poses contain the enzyme (protein + CU ions) and the intermedate poses of the ligands (residue name `UNK`) from unbound to bound state, with solvent removed. They were used as the structural basis for MSM featurization and clustering.


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

- **`Movie-S1.mp4`** — A typical binding event of a phenolic ligand to the active site of laccase.
- **`Movie-S2.mp4`** — A typical binding event of an aromatic amine to the active site of laccase.

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

> Biswas A., Singh D., Datta B., and Radhakrishna M. *Conformational Gating of an Active-Site Loop Governs Phenolic and Aromatic Amine Substrate Selectivity in Fungal Laccase.* (2025) *(under review)*

---

## Contact

**Anushka Biswas** — anushkab2703@gmail.com 
Indian Institute of Technology Gandhinagar
