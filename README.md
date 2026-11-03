# Modeling Malaria Dynamics and Interventions in Burkina Faso

This repository contains the main individual-based simulation code (C++) used for simulating *Plasmodium falciparum* malaria dynamics and studying the effects of interventions in Burkina Faso. The work utilizes the Temple-Malaria-Simulation framework, developed by the Boni Lab (formerly associated with Penn State's Center for Infectious Disease Dynamics (CIDD), now at Temple Univdersity).  



## System Requirements
- **Operating System:**  Ubuntu 24.04
- **Compiler:** GNU G++ (13.3.0)
- **CPU** : Single-core execution (no multithreading)
- **RAM** : 25 GB for large-scale runs simulating 25% of Burkina Faso's ~23 million population
- **Disk** : ~40 MB per output SQLite file
- **Dependencies**
  - GSL
  - yaml-cpp
  - fmt
  - CLI11
  - date
  - args
  - unofficial-sqlite3
- **Non-standard hardware:** None required


## Installation and Running Simulations

### Clone the repository

```bash
git clone https://github.com/bonilab/malariaibm-BurkinaFaso-MFT-rotation-complex-strategies.git
cd malariaibm-BurkinaFaso-MFT-rotation-complex-strategies
```
### Build the simulation executable

```bash
# Clone and bootstrap vcpkg
git clone https://github.com/microsoft/vcpkg.git
cd vcpkg
./bootstrap-vcpkg.sh

# Install required packages
./vcpkg install gsl yaml-cpp fmt cli11 date args3 unofficial-sqlite3

# Build with toolchain
cd ..
mkdir build
cd build
cmake .. -DCMAKE_TOOLCHAIN_FILE=/path/to/vcpkg/scripts/buildsystems/vcpkg.cmake
make
```
Replace /path/to/vcpkg/ with your local vcpkg path.

The build process should take less than 5 minutes on a modern machine

### Run the simulation

```bash
./MaSim -i input.yml -r SQLiteMonthlyReporter -j 1
```

- -i specifies the input yml configuration file
- -r specifies the reporter
- -j specifies the job ID, which is used to label the output file

The simulation will produce:

```bash
monthly_data_1.db
```

### Reproducibility

The raster files used for this Burkina Faso Model are uploaded to following folder
https://github.com/sarit-adh/ART-R-Preparation-Burkina-Faso/tree/main/Calibration/raster_files

The input files used for calibration and intervention studies are as follows:

**Calibration** : https://github.com/sarit-adh/ART-R-Preparation-Burkina-Faso/tree/main/Calibration/input_files

**Study** : https://github.com/sarit-adh/ART-R-Preparation-Burkina-Faso/tree/main/Studies/input_files

Each simulation run for intervention study takes from 20 to 25 hours to complete on high performance computing system, and upto 45 hours on a standard desktop computer.

The complete simulation output dataset can be downloaded from the following link

https://filedn.com/lexUxgNbsuUbyRIygA2lmeR/Malaria-Simulation-Output-Files/2026-08-malariaibm-BurkinaFaso-MFT-rotation-complex-strategies/

The processed datasets from following folder can be used to replicate the results in the paper. 

https://github.com/sarit-adh/ART-R-Preparation-Burkina-Faso/tree/main/Studies/output_files

The python code used for analysis can be downloaded from

https://github.com/sarit-adh/ART-R-Preparation-Burkina-Faso/tree/main/Studies

If the processed dataset is used, the analysis and visualizations created for the paper can be reproduced within couple of hours.

