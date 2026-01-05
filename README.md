# phenolytics_computational_analysis-


# Methods

# Molecular Dataset Preparation
A curated dataset of phenolic and polyphenolic compounds was compiled using compound names as primary identifiers. Canonical SMILES representations were obtained either manually or programmatically via the PubChem database to ensure unambiguous molecular structures. All subsequent calculations were performed using these standardised molecular representations.
3D Geometry Construction

Initial three-dimensional molecular geometries were generated from SMILES strings using RDKit. Explicit hydrogen atoms were added, followed by the generation of conformers via distance geometry. A preliminary geometry optimisation was performed using the Universal Force Field (UFF) to obtain physically reasonable starting structures for quantum mechanical calculations.
Semi-Empirical Quantum Mechanical Calculations

Quantum mechanical calculations were conducted using the MOPAC software package (version 2016). Geometry optimisations were carried out using the PM7 semi-empirical Hamiltonian with the Eigenvector-Following (EF) optimisation algorithm. Default convergence criteria were applied unless otherwise specified.

Each molecule was processed individually, producing standard MOPAC output (.out) and archive (.arc) files. Calculations that did not converge successfully were excluded from the descriptor extraction process.
Extraction of Quantum Mechanical Descriptors

# Quantum Mechanical Descriptors 

Quantum mechanical descriptors were parsed directly from MOPAC output files using automated text-processing routines. Extracted descriptors included energetic, electronic, and reactivity-related quantities, such as:

    • Heat of formation
    • Highest occupied molecular orbital (HOMO) energy
    • Lowest unoccupied molecular orbital (LUMO) energy
    • HOMO–LUMO energy gap
    • Dipole moment
    • Core–core repulsion energy
    • COSMO solvation surface area and volume (when available)
Derived reactivity indices were computed according to conceptual density functional theory, including chemical hardness, softness, and electrophilicity.
Cheminformatics Descriptor Calculation

# Topographical and Topological Molecular Descriptors 

In parallel with quantum calculations, additional physicochemical and structural descriptors were computed from SMILES representations using RDKit. These included:

    • Molecular weight
    • Topological polar surface area (TPSA)
    • LogP
    • Number of hydrogen bond donors and acceptors
    • Number of hydroxyl groups
    • Number of carbonyl groups
    • Number of aromatic rings
    • Number of rotatable bonds
    
These descriptors complement quantum mechanical features and provide structural context for downstream modelling.
Descriptor Integration and Data Assembly

Quantum mechanical and cheminformatics descriptors were merged into a unified descriptor table indexed by compound name. The final dataset was exported as a CSV file, enabling direct use in statistical analysis, QSAR modelling, or machine learning workflows. Missing values resulting from failed calculations were explicitly flagged to preserve data integrity.
Software and Environment

All data processing and analysis were conducted using Python (version ≥ 3.9) with the following libraries: RDKit, NumPy, and Pandas. Quantum calculations were performed using MOPAC2016 on a Linux-based system

# Particularities of the Method

In this QSAR study, the chemical structures of phenolic compounds—molecules containing a phenol functional group and primarily used as antioxidants—were correlated with their biological activity measured as Trolox-Equivalent Antioxidant Capacity (TEAC). A comprehensive set of physicochemical and structural descriptors was generated during feature engineering, from which the most relevant features were identified using three complementary feature-selection strategies.

Initially, correlation analysis and Random Forest–based importance ranking were employed to remove redundant and weakly informative descriptors. This was followed by Support Vector–based feature evaluation and, finally, Gaussian Process–based feature selection, which accounts for nonlinear relationships and uncertainty in the data.

The limited sample size posed a significant challenge in assessing the generalisation ability of the derived QSAR models, particularly with respect to accurately predicting TEAC values for unseen compounds. To address this, multiple regression approaches were systematically evaluated, including simple linear regression, Elastic Net regression, Support Vector Regression (SVR), and Gaussian Process Regression (GPR). Model performance was assessed using consistent evaluation metrics across all methods.

Among the evaluated models, Gaussian Process Regression, a non-parametric Bayesian approach, demonstrated superior predictive performance. Its ability to model complex nonlinear relationships while explicitly accounting for uncertainty enabled more accurate prediction of antioxidant activity based on the physicochemical properties of phenolic compounds.

# References 
The TEAC values were collected from:
Cai, Y. Z., Mei, S., Jie, X., Luo, Q. & Corke, H. Structure-radical scavenging activity relationships of phenolic compounds from
traditional Chinese medicinal plants. Life. Sci. 78(25), 2872–2888 (2006).
      │
