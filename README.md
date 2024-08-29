## 1 Repository Structure
- After `git clone`, you will see the directory structure shown below:
  - The `./dataset` folder contains the dataset needed for AE. Readers need to manually extract the dataset downloaded to this path. 
    - The folders named as `section[x]` contain the data required for "Section X" in the paper. 
    - The `raw_dataset` folder includes the metric and trace datasets as described in Section 2.3 in the paper. 
    - It's important to mention that computing directly on the `raw_dataset` can be very time-consuming (potentially taking several hours). Therefore, what we provide in the `section[x]` folders are precomputed data derived from the `raw_dataset`. 
  - The `./source_code` folder contains scripts organized by sections that are required to reproduce the results of the paper. This folder contains two types of files:
    - **R scripts** for simple calculations and plotting, which can directly generate the tables and figures in the paper. 
    - **Python scripts** for pre-calculating on the `raw_dataset` and for various simulation experiments. 
    - Both types of scripts can be run directly after setting the working directory.
  - The `./figure` folder stores the generated figures.

```markdown
- eurosys25_ae
  -- dataset
    --- raw_dataset
    --- section3
    --- section4
    --- ...
  -- source_code
    --- section3
    --- section4
    --- ...
  -- figure
    --- figure_1_a.pdf
    --- figure_1_b.pdf
    --- ...
```
## 2 Requirements

### 2.1 Download Dataset

Readers need to download the dataset from [**XXXX**] and manually extract it to the path `./dataset`.

### 2.2 Install Requirements

It is important to note that **installing R alone is sufficient to reproduce the results of the paper**. The purpose of Python is to run scripts for pre-calculating on the `raw_dataset` and runs simulation experiments.

- **R language**: The author uses **R version 4.1.0** and has installed the following necessary R packages: `data.table (1.15.2)`, `dplyr (1.1.4)`, `ggplot2 (3.5.0)`, `tidyr (1.3.1)`, `glue (1.7.0)`.
- **Python**: The author runs the Python scripts in a conda virtual environment with **Python version 3.8.18**. The virtual environment has the Python packages installed as listed in `./requirements.txt`.

### 2.3 Modify Working Directory

To run the R and Python scripts, readers need to manually modify the working directory in the source code files. 
- For R scripts, search for `setwd` in the code file and modify the path as `setwd("/path/to/eurosys25_ae")`.
- For Python scripts, searchr for `os.chdir()` in the code file and modify the path as `os.chdir("/path/to/eurosys25_ae")`.

## 3 Reproduce the Results by Section

### Results in "3 Dataset Overview"

- The results of `Table.2 Baseline statistics of the metric data` can be obtained by running the R script at `./source_code/section3/table_2.R`.

### Results in "4 Load Balancing in the Hypervisor"

- The six sub-figures of `Figure 2. Load Balancing in the Hypervisor` are generated by the R script `./source_code/section4/figure_2.R`.
- Note that the results in Figure 2(d) come from the rebind simulation script in `./source_code/section4/rebind_simulation.py`.

### Results in "5 Traffic Throttle in the Hypervisor"

- The results in `Figure 3. Traffic Throttle in the Hypervisor` can be obtained by running the R script `./source_code/section5/figure_3.R`.
- Note that the results in `Figure 3(d)-(g)`, i.e., the simulation results of the proposed "limited lending" (Sec.5.3 in the paper) come from the Python script `./source_code/section5/traffic_throttle_simulation.py`.

### Results in "6 Load Balancing in the Storage Cluster"

- The results in `Figure 4. Frequent Segment Migration` and `Figure 5. Balanced Write but Skewed Read ` are generated by the R scripts `./source_code/section6/figure_4.R` and `figure_5.R`, respectively.
- Note that the functions of the various Python scripts are as follows:
  - `filter_frequent_migration.py`: This script is used to mark the "frequent migration" as defined in Section 6.1.1 of the paper.
  - `segment_migration_simulation.py`: This script is used to simulate segment migration under different importer selection methods (Sec.6.1.2) and to calculate the migration frequency.
  - `predict_bs_traffic.py`: This script uses various methods to predict the traffic of the BlockServer, as described in Sec.6.1.3.

### Results in "7 Cache Across the EBS Stack"

- The results in `Figure 6. Cache across the EBS Stack` and `Figure 7. Cache across the EBS Stack` come from the R scripts `./source_code/section7/figure_6.R` and `figure_7.R`, respectively.
- Note that the python script `cache_simulation.py` calculates the hit rate under different cache algorithms (Sec.7.3).