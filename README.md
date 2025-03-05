# Quantitative Image-Based Cytometry

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

## Introduction
This project showcases a portfolio of single-cell analysis data derived from high-content imaging experiments. The data is processed using Python-based automated pipelines and analyzed/visualized using R.

## Pipeline Workflow
*I will write a description of the image handling, processing, etc.*

## Pipeline Components

### ANALYSE_IMAGES.pynb
Front end of the pipeline. All specifications are input here.

### main.py
Backbone of the pipeline that gets called in ANALYSE_IMAGES.pynb. Contains the function `process_images`, which calls all other functions.

### timekeeping.py
Handles logging and performance tracking of pipeline execution times.

### file_management.py
Manages file input/output operations, including directory handling and metadata storage.

### image_processing.py
Contains image preprocessing functions such as filtering, segmentation, and background correction.

### measure_nuclei.py
Quantifies nuclear morphology, intensity, and other relevant single-cell metrics.

### ktr.py
Analyzes kinase translocation reporter (KTR) data to extract dynamic signaling information.

### image_output.py
Generates processed image outputs, overlays, and summary visualizations.

