# Nucleotide-Protein Package

**Nucleotide-Protein Package** is a Python tool for generating key/triplet files for Nucleotide-Protein analysis.

## Table of Contents
- [Installation](#installation)
- [Usage](#usage)
  - [Generate Keys and Triplets](#generate-keys-and-triplets)
- [Examples](#examples)

## Installation

### Cloning the Repository

To get started with the `Nucleotide-Protein Package`, clone the repository from GitHub:

```bash
git clone https://github.com/KrishnaRauniyar/Nucleotide-Protein.git
cd Nucleotide-Protein
```

### Installing the Package
1. It's recommended to create a virtual environment:

```bash
python3 -m venv tsrenv
source tsrenv/bin/activate  # Mac/Linux
tsrenv\Scripts\activate  # Windows
```

2. Install the necessary dependencies:

```bash
pip install -r requirements.txt
```

## Usage
### Generate Keys and Triplets
To generate keys or triplet files for the Nucleotide-Protein:

```python
python cross_key.py -p drug_protein_cross.csv -o output_dir
```

### CSV file information as input
You should pass a csv file drug_protein_cross.csv which has the follwoing format.

| drug              | drug_seq | drug_coordinates     | protein         | protein_seq | protein_coordinates   | distance (angstrom) |
|-------------------|----------|----------------------|-----------------|-------------|-----------------------|----------------------|
| 3D0A_E_DC_1_O5'   | 109      | -3.283_17.038_0.965 | 3D0A_A_SER_121_O | 109         | -2.462_18.759_2.734  | 2.6                  |
| 3D0A_E_DC_1_C5'   | 106      | -3.710_17.876_-0.156 | 3D0A_A_SER_121_O | 109         | -2.462_18.759_2.734  | 3.3                  |
| 3D0A_E_DG_2_OP2   | 109      | -5.794_20.820_2.780 | 3D0A_A_SER_121_N | 108         | -4.315_20.590_5.173  | 2.8                  |
| 3D0A_E_DG_2_OP2   | 109      | -5.794_20.820_2.780 | 3D0A_A_SER_121_CA | 106         | -3.485_19.453_4.782  | 3.3                  |

The csv input file includes information for both Nucleotide (drug) and Protein. The first three columns contains the drug name, drug sequence number, and X, Y, Z coordinates and the following three columns contains the protein name, protein sequence number, and X, Y, Z coordinates and the last columns is the distance between these drug and protein.


## Examples
### Example 1: Retrieving PDB Files and Generating Keys

```python
from nucleotide_tsr_package.tsr.retrieve_pdb_files import retrieve_pdb_files
from nucleotide_tsr_package.tsr.generate_keys_and_triplets import NucleotideTSR

# Step 1: Retrieve PDB files
data_dir = "Dataset/" # It is also the default directory if not declared
pdb_ids = ["1GTA", "1gtb", "1lbe"] # Not case-sensitive
chain = ["A", "A", "A"] # Case-sensitive
mirror_image: "True" # Optional argument. Set to True if you want the TSR to address for the mirror image triangles.
retrieve_pdb_files(pdb_ids, data_dir)

# Step 2: Generate key files for the proteins
NucleotideTSR(data_dir, pdb_ids, chain=chain, output_option="keys", mirror_image=mirror_image) # Modify the output option as desired
```
zxs3e 
### Example 2: Using CSV File for Input

```python
from nucleotide_tsr_package.tsr.retrieve_pdb_files import retrieve_pdb_files
from nucleotide_tsr_package.tsr.generate_keys_and_triplets import NucleotideTSR

# Use CSV input for batch processing
data_dir = "Dataset/"
csv_file = "sample_details.csv"
mirror_image: "True" # Optional argument. Set to True if you want the TSR to address for the mirror image triangles.
retrieve_pdb_files(csv_file, data_dir)
NucleotideTSR(data_dir, csv_file, output_option="triplets", mirror_image=mirror_image)
```
