# Protein-Crystal-Symmetry-Reconstruction
This project focuses on the transformation and symmetry-based reconstruction of the crystal structure of **Pyruvate Oxidase**, a peripheral membrane enzyme from *Escherichia coli*.

## Structural Data

- **PDB ID:** 3EY9  
- **Experimental Method:** X-ray crystallography  
- **Resolution:** ~2.2 Å  
- **Structure Type:** Peripheral membrane enzyme  
- **Chains Present:** A, B  
- **Gene Names:** poxB, B0871, JW0855  

---

## Crystallographic Properties

- **Space Group:** P 43 21 2  
- **Crystal System:** Tetragonal  
- **Biological Unit:** Tetramer  

Tetramer formation allows cooperative interactions between subunits and is energetically favorable  
(ΔG ≈ −304 kcal/mol).

---

## Symmetry Operators

The structure contains **8 crystallographic symmetry operators**, including:

- 1 identity operation  
- 2 rotations by 180°  
- 2 screw-axis rotations by 90°  
- 3 translational operations  

Crystallographic symmetry defines how protein units assemble within the crystal lattice and is dictated by the space group.

The structure also includes **2 BIOMT operators (REMARK 350)**, which explicitly direct tetramer formation from the two chains present in the asymmetric unit.

Symmetry operations applied to the asymmetric unit construct the complete biological assembly from chains A and B.

Symmetry ensures:
- Equal exposure of membrane-binding regions  
- Coordinated activation of catalytic sites  

The asymmetric unit contains chains A and B, which, after applying the 8 symmetry operations, populate the unit cell.

---

## ZIP File Contents

1. Output image from PyMOL  
2. All 8 transformed structures (load all into PyMOL to visualize the complete assembly)  
3. Input file: `3EY9.pdb`  
4. Python code  
5. Python Markdown file  

---

## Methodology (Pseudocode)

### 1. Initialization & Data Retrieval
- Download the PDB file (`3EY9`) from the RCSB server  
- Read and store atomic coordinates:
  - `ATOM` records (protein atoms)
  - `HETATM` records (cofactors/ligands, if present)
- Initialize empty lists for symmetry matrices (SMTRY)

---

### 2. Parse Symmetry Transformations
- Extract crystallographic symmetry operations from **REMARK 290** in the legacy PDB file  
- For each symmetry operation, store:
  - 3×3 rotation matrix (**R**)
  - 3×1 translation vector (**t**)

Full arrays of rotation and translation matrices are constructed directly from the PDB metadata.

**Optional:** Apply **REMARK 350 BIOMT** operations to first construct the tetramer and then apply the 8 crystallographic symmetry operations.

This produces the same result as using only **REMARK 290 (SMTRY)** because:
- The two BIOMT operations required to form the tetramer are already embedded within the 8-fold crystallographic symmetry of the lattice
- SMTRY operators rotate and translate the asymmetric unit throughout the unit cell, recreating the same tetramer arrangement

---

### 3. Transformation Loop
For each of the 8 symmetry operations:
- For each atom in the newly created tetramer:
  - Apply the transformation:  
    **X″ = R · X′ + t**
- Write the transformed coordinates to a new PDB file and append to the output set

---

## Output

- **8 PDB files** representing symmetry-related instances of the biological assembly
