# MorphologicVariability
 Code associated with Brigham and Crider's (2022) metric for calculating along-landform morphologic variability.

## Background
The shape of a landform changes with time depending on the type and rate of the processes active upon it. Identifying and untangling the contribution of each factor to landform shape is difficult, but patterns in profile form along linear landforms can be examined to determine the dominant processes. We develop a methodology to quantify these variations in profile form and define a “morphologic variability metric.”

Using the example of fault scarps in jointed bedrock, we first manually classify fault-scarp profiles extracted from the SfM-derived point clouds into six morphologic categories defined through observations of common forms across scarps.

Our morphologic variability metric quantitatively describes this change in shape. Then, we use principal component analysis with singular value decomposition, a data-reduction technique, on the positional data of the scarp-normal profiles to quantitatively distinguish between these morphologic classes. We follow this by employing a supervised learning algorithm, the support vector machine (SVM) method, to build a classifier, using the principal-component coordinates of the classified profiles in principal component space as a training set. Classification performance was assessed using 5-fold cross validation (81% accuracy) and with independent test data (80% accuracy). Finally, we define a morphologic variability metric and calculate it by determining the number of classes represented and the standard deviation of their proportions in a moving window along the scarp. This metric is then normalized, so that a value of 0 represents a section of scarp where all profiles belong to the same class, and a value of 1 represents a section where all classes are represented in equal proportion. 

The morphologic classes are user-defined based on the profile forms represented in the overall dataset and the approach does not rely on any landform-specific metrics, instead using data-reduction techniques on the positional data of the landform profile itself as the basis for classification. This allows for a widespread application of this approach to many different types of landforms, as it eliminates the need to find a sufficient number of landform-specific parameters to quantitatively characterize the shape of the profile. Our metric is a promising tool to understand how many types of landforms evolve.

## Notebooks
### 1. extract-profiles-from-dem.ipynb (morph-var 1)
In this notebook, we extract landform-normal profiles using three user-provided data: a DEM of the region of interest, a polygon shapefile that can be used to crop the DEM to the sepecific lanform if desired, and a line shapefile (contained within the cropping polygon) that traces the center of the landform.

The output of the notebook is a folder with text files for each landform-normal profile. Each text file has columns for the Easting, Northing, UTM Zone, and elevation of each point along the landform-normal profile. These text files are used as the data input for morp-var 2.

### 2. process-profiles.ipynb (morph-var 2)
In this notebook, we use the output of the first notebook (morph-var 1), which is a folder containing text files with the coordinates and elevation data of points along each landform-normal profile. This notebook focuses on formatting and normalizing the profile data, so that they are ready for use in our classification algorithm (morph-var 3).

To normalize the profiles, we calculate the two-dimensional coordinates of each profile, automatically determine the position of the crest and toe of the scarp, crop the the profile between the crest and the toe and normalize the profile by the scarp height. The output of the notebook is a landform-specific folder with text files for the processed profiles. If there are multiple landforms to be analyzed, the notebook will have to be re-run for each landform. 
### 3. train-classifier.ipynb (morph-var 3)

### 4. classify-new-landform.ipynb (morph-var 4)

### 5. calculate-variability.ipynb (morph-var 5)

Brigham, C. A. P., and Crider, J., G.: A New Metric for Morphologic Variability Using Landform Shape Classification via Supervised Machine Learning, Geomorphology, 399, (2022). https://doi.org/10.1016/j.geomorph.2021.108065
