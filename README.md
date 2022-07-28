# FD Analysis

![Fractal Analysis](https://upload.wikimedia.org/wikipedia/commons/thumb/4/4d/32_segment_fractal.jpg/240px-32_segment_fractal.jpg)

Code to compile and analyze FD data. Includes folders with FD data (as of 7/27/2022) for pruning, offsets, artery/vein, DNN, FACTOR scaling, and surface area via marching cubes.

Works in Windows.

## Installation
1.) Clone or download the repository using https://github.com/actsao/fd_analysis.git for cloning or under Code > ZIP for downloading. Extract files if needed.
 - Download recommended for new github users

2.) In Anaconda Prompt, while in the directory for fd_analysis (create does not create the file but rather uses the file to create) run

```
conda env create -f environment.yml
```

- Anaconda Prompt is recommended over CMD for ease of use. Either is fine otherwise.

## Sample Usage
1.) In Anaconda Prompt, activate the environment

```
conda activate fd_analysis
```

2.) CD into the folder containing the downloaded files

3.) Use the following command to begin Jupyter Lab

```
jupyter lab
```

## Guide
### Relevant Data:
| Data (.csv)         | Description                                                                     |
|---------------------|---------------------------------------------------------------------------------|
| analysis_FDs_data   | Raw data from FDs_data, which includes most of generated FD data minus pruning. |
| analysis_DNN        | Basic stats for DNN and FACTOR scaled data                                      |
| pruned_FDs          | Raw data of % BV5 pruning                                                       |
| analysis_BV5Pruning | Basic stats of % BV5 pruning                                                    |


### Relevant Notebooks:
| Notebook (.ipynb)    | Description                                                                                                                                         |
|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| analysis_BV5Pruning  | Simple demo of % BV5 pruned or thresholded data. Outputs "pruned_FDs.csv" w/ raw data and "analysis_BV5Pruning.csv" w/ stats                        |
| analysis_FDs_data    | Simple demo of FDs_data folder. Outputs "analysis_FDs_data.csv" w/ raw data and "analysis_DNN.csv" w/ basic DNN and FACTOR_SCALE stats              |
| Compare_FD           | (Unused) Basic exploration of different FD data                                                                                                     |
| compileData          | Original notebook for compiling FDs_data. Includes code to recalculate FDs for custom box size ranges (used in ATS 2022 poster))                    |
| ComputeFD            | (Unused) Uses ManySizeBy1 (or similar) data to calculate original, 20Size, 20SizeBy1, and ManySize data                                             |
| exploreFeatures      | (Unused) Basic exploration of file importing and stats                                                                                              |
| FD_visual            | Generates figures w/ trend lines, residual graphs, & histograms                                                                                     |
| FD_visual_ManySize   | (Unused) Generates figures w/ trend lines, residual graphs, & histograms                                                                            |
| organizeFactorScales | Organizes FACTOR_SCALE folder from cluster into separate folders based on percentage. Needs to be run for FACTOR_SCALE data to be properly imported |
| plotFeatures         | Different visuals of FACTOR_SCALE and DNN_SCALE data. Includes interactive graph w/ sliders for custom box size ranges                              |
| plotFeatures_demo    | Version of plotFeatures.ipynb that only includes the interactive graph w/ sliders for custom box size ranges                                        |
| posterStatistics     | (Unused) Used to generate stats for the 2022 ATS poster presentation                                                                                |
| testMarchingCubes    | Calculates Surface Area using scipy's Marching Cubes algorithm and Volume for nrrd files                                                            |
| visualizeNrrd        | (Unused) Explorations in visualizing nrrd files through Jupyter (did not work very well; just use Slicer)                                           |
| volumeStatistics     | Explorations in generating statistics based on Surface Area and Volume data                                                                         |

### Folders:
| Folder              | Description                                                                             |
|---------------------|-----------------------------------------------------------------------------------------|
| FDs_data            | Contains most FD data. Data here is compiled into "analysis_FDs_data.csv". See below for more info |
| scaled_results      | Old testing of constant scaling (Unused, replaced by FACTOR_SCALE data)                 |
| stencils            | Stencils for sample patients (Unused)                                                   |
| thresholded_results | Contains % BV5 pruned or thresholded data                                               |

### "FDs_data" Folders:
| Folder Name     | Description                                           |
|-----------------|-------------------------------------------------------|
| FDs             | FDs using powers of 2 as box sizes                    |
| FDs_20Size      | FDs using [2, 20, 2] as box sizes                     |
| FDs_20SizeBy1   | FDs using [2, 20, 1] as box sizes                     |
| FDs_ManySize    | FDs using [2, max_size/2, 2] as box sizes             |
| FDs_ManySizeBy1 | FDs using [2, max_size/2, 1] as box sizes             |
| SurfaceArea     | Surface Area calculated using marching cubes + Volume |
- FDs, unless indicated, are calculated over the ENTIRE series of box sizes
- Square brackets indicate a series of numbers defined as [start, end, step_size] (inclusive)
- "max_size" indicates maximum box size allowed for image
  - this is usually the smallest image dimension
- Surface Area and Volume are calculated on 3d numpy arrays, then converted into real world units (as given by nrrd file)

### "FDs_data Folder" Endings:
| Folder Ending   | Description                                                                      |
|-----------------|----------------------------------------------------------------------------------|
| _Visual         | Contains images of residual graphs and histograms                                |
| _ArtVein        | Contains FD data separated by artery and vein                                    |
| _DNN_SCALE      | Contains FD data calculated using DNN sizing for particles                       |
| _FACTOR_SCALE   | Contains FD data calculated using particle sizes multiplied by a constant FACTOR (1_0 is original)|
