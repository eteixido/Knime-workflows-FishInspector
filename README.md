# Knime Workflows for FishInspector

This collection of KNIME workflows is required for subsequent analysis of the output of [FishInspector]( https://github.com/sscholz-UFZ/FishInspector).
The FishInspector software has been initially developed for images obtained with an automated capillary position system [VAST](http://www.unionbio.com/vast/) BioImager™. However, images from other sources can be used as well after appropriate conversion using the example below.
The FishInspector provides the coordinates of morphological features as [JSON]( https://en.wikipedia.org/wiki/JSON) files. We had been mainly interested in concentration-response analysis of fish embryos exposed to chemicals. Therefore, various KNIME workflows with embedded R-scripts are provided for subsequent data processing and analysis. Prior to concentration-response analysis it is required to analyse the distribution/variability of features in control embryos. 

In order to run the workflows a [KNIME](http://www.knime.org) and [R](https://www.r-project.org/) installation is required. The workflows can be imported into KNIME by importing each KNIME archive file (\*.knwf).  You may have to install certain additional packages in R (please open workflows in KNIME for further instructions). Our workflows have been established and tested with R version 3.4.1 but other versions may work as well. 
You will have to install various KNIME extentions in order to run the workflows. Extensions are indicated in each workflow. 

More details on the software and the subsequent data analysis can be found in the following publication:

*[Teixido, E., Kießling, T.R., Krupp, E., Quevedo, C., Muriana, A., Scholz, S., 2018. Automated morphological feature assessment for zebrafish embryo developmental toxicity screens.  Tox. Sci. accepted.](https://academic.oup.com/toxsci/advance-article/doi/10.1093/toxsci/kfy250/5123521)*

## Conversion workflow for non-capillary images
Images not obtained by automatic positioning in a glass capillary - and hence, not presenting capillary boundaries - can be used as well but require automatic conversion to an image with a virtual capillary. This can be done with a KNIME workflow and an embedded imageJ macro. The workflow can handle multiple images simultaneously. An installation of KNIME and imageJ on your computer is required. Depending on the image quality certain parameters of the workflow may have to be adjusted. Images of embryos from a lateral orientation are required.

Knime extensions required: 
* Knime community contributions - Image Processing
* Image processing - [ImageJ extension](https://www.knime.com/community/imagej)
* Knime Quick Forms


[Knime workflow archive](Rotate_crop_v2.knwf)

## Workflow for extraction of JSON files and generation of box-whisker plots for different features
This workflow extracts the coordinates of the annotated features in the FishInspector JSON files and calculates these morphological parameters: 
* Body length
* Eye size
* Pericard size
* Yolk sac size
* Head size
* Maximum tail curvature 
* Three tail angles (three equidistance points along the nothocord)
* Head-trunk angle (48 hpf)
* Otolith-eye distance (96 hpf)
* Jaw-eye distance (96 hpf)
* Mandibular arch distance (96 hpf)
* Swim bladder presence and size (96 hpf)

The morphological paramaters are calculated using the R packages [Features](https://cran.r-project.org/web/packages/features/features.pdf) and [Momocs](https://cran.r-project.org/web/packages/Momocs/Momocs.pdf). The workflow generates whisker plots to a better visualization of concentration dependent effects on the morphological features using the R package [ggplot2](https://cran.r-project.org/web/packages/ggplot2/ggplot2.pdf). 

[KNIME workflow archive](FishInspector_features_Jan_2019.knwf)

## Determination of thresholds for control variability

This workflow calculates the control variability of the morphological features (among different replicates). A range of a two-fold standard deviation around the mean is used as a threshold to indicate deviation from control embryos and calculation of quantal concentration-response curves.

[KNIME workflow archive](Control_variability_v2.knwf)

## Workflow for concentration-response analysis based on thresholds for the deviation of features from normal phenotypes

This workflow creates the concentration-response curves for the morphological features analysed with the FishInspector using the xls files obtained with the two last workflows. The concentration-response curves are derived using a four-paramater log-logistic function with the R package [drc](https://cran.r-project.org/web/packages/drc/drc.pdf).

[KNIME workflow archive](Concentration_response_curves_v2.knwf)
