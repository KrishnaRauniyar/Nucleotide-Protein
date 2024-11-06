# Nucleotide-Protein Package

**Nucleotide-Protein Package** is a Python tool for generating key/triplet files for Nucleotide-Protein analysis.

## Table of Contents
- [Installation](#installation)
- [Usage](#usage)
  - [Generate Keys and Triplets](#generate-keys-and-triplets)
- [Results](#results)

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

### CSV file information as input (drug_protein_cross.csv)
You should pass a csv file drug_protein_cross.csv which has the follwoing format.

| drug              | drug_seq | drug_coordinates     | protein         | protein_seq | protein_coordinates   | distance (angstrom) |
|-------------------|----------|----------------------|-----------------|-------------|-----------------------|----------------------|
| 3D0A_E_DC_1_O5'   | 109      | -3.283_17.038_0.965 | 3D0A_A_SER_121_O | 109         | -2.462_18.759_2.734  | 2.6                  |
| 3D0A_E_DC_1_C5'   | 106      | -3.710_17.876_-0.156 | 3D0A_A_SER_121_O | 109         | -2.462_18.759_2.734  | 3.3                  |
| 3D0A_E_DG_2_OP2   | 109      | -5.794_20.820_2.780 | 3D0A_A_SER_121_N | 108         | -4.315_20.590_5.173  | 2.8                  |
| 3D0A_E_DG_2_OP2   | 109      | -5.794_20.820_2.780 | 3D0A_A_SER_121_CA | 106         | -3.485_19.453_4.782  | 3.3                  |

The csv input file includes information for both Nucleotide (drug) and Protein. The first three columns contains the drug name, drug sequence number, and X, Y, Z coordinates and the following three columns contains the protein name, protein sequence number, and X, Y, Z coordinates and the last columns is the distance between these drug and protein.

## Result
CrossKeys will be generated between:
- One drug and two protein
- Two drug and one protein

The results will be stored in output_dir as:
- filename.keys_Freq_theta29_dist18 (1_1TSR_E_DT.keys_Freq_theta29_dist18): It will store the frequency triplets
- filename.keys_theta29_dist18 (1_1TSR_E_DT.keys_theta29_dist18): It will store the keys information

If their are less atoms than 3 then no cross keys will be generated and the terminal will output error message like the example below:
- Cannot make keys for 46_3TS8_L_DT having only 2 atoms.
- Cannot make keys for 9_7B4G_B_DC having only 2 atoms.


