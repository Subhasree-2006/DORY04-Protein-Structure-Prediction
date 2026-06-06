# D0RY04-Protein-Structure-Prediction
A comparative structural bioinformatics study of D0RY04 involving 3D structure prediction, model refinement, validation, and optimization to obtain a high-quality protein model for downstream functional analysis.
# D0RY04 Protein Structure Prediction, Optimization and Validation

## Background

The target protein DORY04 did not have any experimentally determined three-dimensional structure available in the Protein Data Bank (PDB). Sequence similarity searches showed high identity to another UniProt sequence but no experimentally solved structure was available.

Therefore, computational structure prediction methods were employed to generate a reliable 3D model.

---

# Workflow

## Step 1: Protein Sequence Retrieval

The amino acid sequence of DORY04 was obtained from UniProt in FASTA format.

---

## Step 2: Structure Prediction

Since no experimental structure existed, multiple structure prediction approaches were used.

### Prediction Servers Used

| Tool        | Method                            |
| ----------- | --------------------------------- |
| AlphaFold   | AI-based structure prediction     |
| I-TASSER    | Threading and ab initio modeling  |
| Phyre2      | Homology recognition and modeling |
| SWISS-MODEL | Template-based homology modeling  |

The protein sequence was submitted independently to all four servers and predicted structures were obtained in PDB format.

---

## Step 3: Initial Structure Validation

All predicted structures were evaluated using SAVES v6.0.

Validation tools used:

* ERRAT
* VERIFY3D
* PROCHECK
* WHATCHECK

### Initial Comparison

| Model       | Observation                             |
| ----------- | --------------------------------------- |
| AlphaFold   | Highest overall structural quality      |
| I-TASSER    | Lower structural quality than AlphaFold |
| Phyre2      | Acceptable but lower confidence         |
| SWISS-MODEL | Limited by template availability        |

Among all models, AlphaFold showed the best overall stereochemical quality and was selected for further refinement.

---

## Step 4: AlphaFold Model Validation

The AlphaFold structure was analyzed using SAVES.

### Results

| Validation Tool | Result        |
| --------------- | ------------- |
| ERRAT           | ~91           |
| VERIFY3D        | 74.84% (Fail) |
| PROCHECK        | Acceptable    |

### Observation

Although ERRAT indicated good structural quality, VERIFY3D failed because less than 80% of residues achieved a 3D-1D score greater than 0.1.

This suggested the presence of poorly modeled or disordered regions.

---

## Step 5: Structure Refinement Using GalaxyRefine

The AlphaFold structure was submitted to GalaxyRefine.

Five refined models were generated.

### GalaxyRefine Comparison

| Model   | RMSD  | MolProbity | Clash Score | Ramachandran Favored (%) |
| ------- | ----- | ---------- | ----------- | ------------------------ |
| Initial | 0.000 | 1.756      | 6.7         | 94.3                     |
| Model 1 | 0.468 | 1.434      | 8.0         | 99.1                     |
| Model 2 | 0.472 | 1.504      | 9.6         | 99.4                     |
| Model 3 | 0.542 | 1.550      | 10.8        | 99.1                     |
| Model 4 | 0.479 | 1.610      | 12.6        | 99.4                     |
| Model 5 | 0.510 | 1.657      | 14.2        | 99.1                     |

### Selected Refined Model

GalaxyRefine Model 1 was selected because it showed:

* Lowest MolProbity score
* Low RMSD
* Good stereochemical quality
* High Ramachandran favored residues

---

## Step 6: Validation of GalaxyRefine Model

The selected GalaxyRefine model was validated again.

### Results

| Validation Tool | Result        |
| --------------- | ------------- |
| ERRAT           | 92.12         |
| VERIFY3D        | 74.84% (Fail) |
| PROCHECK        | Good          |

### Observation

GalaxyRefine improved local geometry but VERIFY3D still failed.

This indicated that low-confidence regions were still present in the structure.

---

## Step 7: Identification of Low-Confidence Regions

The AlphaFold confidence profile was inspected.

Low-confidence residues were observed in the N-terminal region.

These residues corresponded to flexible or disordered segments that negatively affected VERIFY3D scores.

---

## Step 8: Structure Trimming

To remove unreliable regions, residues 1–66 were deleted.

### Trimmed Region

Residues removed:

1–66

### Final Structure

Remaining residues:

252

File:

alphafold_trimmed.pdb

---

## Step 9: Final Structure Validation

The trimmed structure was submitted again to SAVES v6.0.

### ERRAT

| Parameter              | Value |
| ---------------------- | ----- |
| Overall Quality Factor | 91.25 |

### VERIFY3D

| Parameter                 | Value  |
| ------------------------- | ------ |
| Residues with score ≥ 0.1 | 96.03% |
| Status                    | PASS   |

### PROCHECK

| Parameter          | Value |
| ------------------ | ----- |
| Core Region        | 93.2% |
| Additional Allowed | 6.8%  |
| Generously Allowed | 0.0%  |
| Disallowed Region  | 0.0%  |
| G-Factor           | 0.03  |

---

## Final Model Selection

The trimmed AlphaFold model was selected as the final structure because it achieved:

* ERRAT > 90
* VERIFY3D PASS (96.03%)
* Ramachandran favored residues > 90%
* No disallowed residues
* Acceptable G-factor
* Good stereochemical quality

---

## Final Conclusion

Four independent structure prediction approaches were evaluated:

* AlphaFold
* I-TASSER
* Phyre2
* SWISS-MODEL

AlphaFold generated the best initial structure.

GalaxyRefine improved local geometry but did not resolve the VERIFY3D failure.

Analysis of AlphaFold confidence scores identified a low-confidence N-terminal region. Removal of residues 1–66 produced a significantly improved model.

The final validated structure (alphafold_trimmed.pdb) achieved:

* ERRAT = 91.25
* VERIFY3D = 96.03%
* Ramachandran favored = 93.2%
* Disallowed residues = 0%

The final structure was considered suitable for downstream applications such as molecular docking, binding-site prediction, and molecular dynamics simulations.
