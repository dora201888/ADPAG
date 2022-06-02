# ADPAG: An Open-Source R/R-Markdown Package for Accelerometer Data Processing after Running GGIR



# Introduction


## What is GGIR?

[GGIR](https://CRAN.R-project.org/package=GGIR) is an R-package to process multi-day raw accelerometer data for physical activity and sleep research. GGIR will write all output files into two sub-directories of ./meta and ./results. GGIR is increasingly being used by a number of academic institutes across the world.  
 

## What is ADPAG?

[ADPAG](https://CRAN.R-project.org/package=ADPAG) is an R-package to data processing after running GGIR for accelerometer data. In detail, all necessary R/Rmd/shell files were generated for data processing after running GGIR for accelerometer data. Then in module 1, all csv files in the GGIR output directory were read, transformed and then merged. In module 2, the GGIR output files were checked and summarized in one excel sheet. In module 3, the merged data was cleaned according to the number of valid hours on each night and the number of valid days for each subject. In module 4, the cleaned activity data was imputed by the average ENMO over all the valid days for each subject. Finally, a comprehensive report of data processing was created using Rmarkdown, and the report includes few explortatory plots and multiple commonly used features extracted from minute level actigraphy data in module 5-7. This vignette provides a general introduction to ADPAG.

 
 
 
## Software Architecture

The R package ADPAG has been released with an open-source GPL-3 license on CRAN, and ADPAG can run on Windows and Linux. Parallel computing in Linux is recommended due to the memory requirements associated with reading in multiple of the large data files. The package contains one primary function for users which, when run, generates all necessary R/R Markdown/shell executable files for data processing after running GGIR for accelerometer data; load, read, transform and merge long activity data;  examine and summarize GGIR outputs; clean the merged activity data according to the number of valid hours per night and the number of valid days per subject; activity data imputation by taking the average across the valid days for each subject; build a comprehensive report of data processing and exploratory plots; extract multiple commonly used features and study feature structure by the covariance decomposition. Figure 1 presents a flowchart for each step in this process which is described in greater detail below. The procedure, R functions, inputs, and outputs are all described in this package vignette. In addition, more documentation and example data could be found in ADPAG repository on GitHub (URL: https://github.com/dora201888/ADPAG).          
 


#
Mirroring the GGIR structure of processing individual data files in multiple parts, the ADPAG package is split into seven modules, grouping functionalities in logical processing order. The modules are numbered from 1 to 7. modules 1 to 4 are dedicated to data processing. modules 5 to 7 are dedicated to producing R Markdown reports of data cleaning, feature extraction, and unsupervised covariance decomposition via the joint and individual variance explained (JIVE) method, respectively.  These seven modules are carried out sequentially with milestone data automatically being saved locally. To use ADPAG, the first step for users is to install and load the ADPAG package. Then, users run the create.adpag.shell() function which creates a single R script. The newly created R script, Studyname_module0.maincall.R, is then edited by users, allowing for the specification of arguments relevant for each of the seven modules. All optional arguments and their defaults are described in the package vignette. In addition, for users with access to a cluster for parallel processing, a shell function, named as module9_swarm.sh is created which can parallelizes the processing of individual files with minor modifications by the user. These modifications are described in the package vignette.   Computationally, module 1 is the most time-consuming task, taking up at least 60% of the processing time, which the activity data in .csv format was transformed and merged.  Generally, module 1 takes about 10~30 minutes to process a file with 14 days of data recorded at 30 Hz on a GeneActiv device in processor cores of 36 x 2.3 GHz (Intel Gold 6140). All output created for each module is described in the package vignette. Briefly, module 1 and module 2 output are saved using a directory structure with a depth of two, containing output data and summary for all participants. The reports for modules 5 to 7 are saved in .html format and are generated using R Markdown (.Rmd) files. These .Rmd files are included in the output, users the flexibility to adapt the source code to their research purpose. 

