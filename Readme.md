#Image Analysis Notebooks and Scripts

This is a place where I keep Image Analysis code written for various projects.  Some more structure may emerge over time, for the time being the code is 
in multiple projects (each in the directory projects), where each is completely contained and has instructions how to create the needed environment and how to run the code.


Overview of projects:
- Kunal: Quantification of Ca uncaging.  Takes time-lapse series (created by Mciro-Manager) as input.  Also reads in ImageJ-ROIManager files with locations of uncaging.  Identifies cells on the mean intensity projection of the time-lapse using Cellpose, then plots the mean intensity (normalized by mean intensity of the first time point) of each cell as a function of time.


