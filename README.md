# Quantitative Image-Based Cytometry
[dwtcullen.github.io](https://github.com/dwtcullen)

Portfolio of single-cell analysis data processed using Python and visualized using R.

## Table of Contents
- [Introduction](#introduction)
- [Pipeline Workflow](#pipeline-workflow)
- [Pipeline Components](#pipeline-components)
  - [ANALYSE_IMAGES.pynb](#analyse_imagespynb)
  - [main.py](#mainpy)
  - [timekeeping.py](#timekeepingpy)
  - [file_management.py](#file_managementpy)
  - [image_processing.py](#image_processingpy)
  - [measure_nuclei.py](#measure_nucleipy)
  - [ktr.py](#ktrpy)
  - [image_output.py](#image_outputpy)

## Summary
This project showcases a portfolio of single-cell analysis data derived from high-content imaging experiments. The data is processed using Python-based automated pipelines and analyzed/visualized using R.

## Pipeline Workflow
### Managing the pipeline
The image processing pipeline is run through a computing cluster located at the University of Queensland. Individual functions of the pipeline are stored in several .py files, separated according to purpose. To simplify pipeline operation across users of varying programming knowledge, I used a simple front-end function 'process_images' from which users can specify conditions. These include the use of different microscopes, cell types and the output of example images. 

### File Sorting
The file names of images produced in QIBC experiments vary between microscopes but contain information on the well, field and channel of each image (e.g. E_6_fld_4_wv_488_Green.tif). I wrote a different regular expression for files from each microscope used in my research, and use groupdict to create a dictionary with each group name as a key. I then sort the files by WV (wavelength) and return a dataframe grouped by Row, Column and Field. Each resulting group contains the names of each channel from a single field in the 96-well plate. 

### Image Reading and Pre-processing
Each group of images is read and assembled in a list. For ease of use, blank images are added if less than four images are produced per group. 

### Segmentation
Segmentation is performed using a Cellpose model trained on a set of 150 images to identify in-focus, unclumped nuclei. 

### Cell Measurement
After segmentation, each individual cell is measured for various characteristics including fluorescence intensity of antibody signals and nuclear morphology. 

### Data Output
Finally, all the measurements are compiled and outputted as a CSV file for further analysis and visualization. In R, I use dplyr to clean and filter the data then create plots using the ggplots package.

## Pipeline Components

### ANALYSE_IMAGES.pynb
Front end of the pipeline. All specifications are input here.

### main.py
Backbone of the pipeline that gets called in ANALYSE_IMAGES.pynb. Contains the function `process_images`, which calls all other functions.

### timekeeping.py
Handles logging and performance tracking of pipeline execution times. Outputs a string that can be printed througout the pipeline to accurately monitor individual steps of the pipeline.

### file_management.py
Manages file input/output operations, including directory handling and image metadata.

### image_processing.py
Contains image processing functions such as segmentation and background correction.

### measure_nuclei.py
Quantifies features such as morphology and signal intensity for each identified cell.

### ktr.py
The ktr module is only used for cells containing a kinase translocation reporter system such as DHB (DNA Helicase B) reporter to measure CDK2 activity. It handles cytoplasmic segmentation and the calculation of cytoplasmic/nuclear ratio per cell.

### image_output.py
Generates annotated output images for troubleshooting and traning of machine learning models.

