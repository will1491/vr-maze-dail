# vr-maze-dail
The `vr-maze-dail` repository contains the algorithm for identifying backtracking moments in participants' trajectories and processing the dataset to understand when and where people backtrack. This research is part of the wayfinding studies at **DAIL** (Design & Augmented Intelligence Lab), aiming to optimize people’s navigation experiences and improve signage effectiveness in complex environments.

## backtrack_6.1.ipynb
This is the main algorithm for identifying participants' wayfinding behaviors, specifically focusing on detecting backtracking moments in their movement trajectories. The algorithm processes raw trajectory data, applies preprocessing steps, detects backtracking based on velocity changes, and validates those moments using acceleration analysis.

### Functions in the Algorithm:
#### 1. `preprocess_trajectory(t, x, y)`
   - **Purpose:** Cleans and processes the raw trajectory data.
   - **Steps:**
     - Removes the first few data points to avoid noise.
     - Flips the y-coordinates for consistency in visualization.
     - Computes displacement vectors, velocity vectors, and unit direction vectors.
     - Identifies straight-line movements by calculating angular deviations over a sliding window.

#### 2. `detect_backtracking(t, x, y, velocity_vectors)`
   - **Purpose:** Detects backtracking moments using velocity direction changes.
   - **Steps:**
     - Computes displacement vectors over time.
     - Applies a sliding window to compare previous and future velocity directions.
     - Uses the dot product to measure angular differences.
     - Flags points where the angular change exceeds a set threshold.

#### 3. `validate_backtracking(t, x, y, backtracking_indices, velocity_vectors)`
   - **Purpose:** Filters out false positives by checking acceleration directions.
   - **Steps:**
     - Computes acceleration vectors based on velocity changes.
     - Measures the alignment between acceleration and velocity vectors.
     - Retains only backtracking points where acceleration opposes velocity significantly.

#### 4. **Trajectory Plotting and Visualization**
   - The algorithm generates trajectory plots highlighting:
     - The original movement path.
     - Significant movement changes.
     - Detected and validated backtracking points.
   - Plots are saved in a multi-page PDF for further analysis.

#### 5. **Sorting PDF Reports (`sort_pdf_by_participant`)**
   - Extracts participant IDs from trajectory plots.
   - Reorders the PDF pages to ensure that data is presented in a structured way.

## Data Processing Overview
The algorithm reads trajectory data from `.txt` files formatted with the following columns:
- `UNIX`: Timestamps
- `xHead, yHead`: X and Y coordinates
- `Task`: Associated navigation task

It outputs:
- A **CSV file** (`Table_Backtrack.csv`) containing detected backtracking moments per participant.
- A **multi-page PDF** (`All_Trajectory_Plots.pdf`) with visualized movement paths and detected backtracking instances.

## Installation & Usage
### Requirements
This project requires Python and the following dependencies:
```bash
pip install numpy pandas matplotlib PyPDF2
