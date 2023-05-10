# CS472 Final Project - Identifying Ink on Ancient Papyrus Texts
Cheyanne Kester, Seth Palmer, and Maddie Porcaro

### Download campfire.zip 
http://dl.ash2txt.org/campfire.zip 


## The Problem
Pompeii and nearby Herculaneum were devastated by the eruption of Mount Vesuvius in AD 79, which caused hundreds of ancient scrolls in the library of a grand luxury villa to be carbonized by the intense blast of hot gas, rendering them completely unreadable. However, researchers are now embarking on a worldwide competition to decipher the charred papyri, following a successful demonstration that an artificial intelligence program can extract letters and symbols from high-resolution X-ray images of the delicate, unrolled documents.

The Vesuvius Challenge is a global competition launched by the Institute for the Study of Ancient Worlds at New York University and the University of Naples Federico II to decipher these ancient scrolls. Participating teams will compete for a grand prize of $150,000, awarded to the first team to decipher four passages of text from the inner layers of the scrolls before the end of 2023. Additionally, progress prizes include $50,000 for accurately identifying ink on the papyri from the 3D X-ray scans. 

The challenge’s Kaggle page can be found at the following webpage: 
Vesuvius Challenge - Ink Detection | Kaggle 

For our final project, we wish to cast our own solution model for identifying ink to aid in this endeavor. Due to time constraints and the sheer size of the datasets, we are only going to analyze the campfire scroll as it’s the smallest of the datasets which makes it more manageable.


## The Dataset
The team of scientists, led by Professor Brent Seales, a computer scientist at the University of Kentucky, is making its software and thousands of 3D X-ray images of two rolled-up scrolls and three papyrus fragments available for the Vesuvius Challenge.

The Kaggle competition provides the following data sets for use in the competition (descriptions taken directly from competition page):
[train/test]/[fragment_id]/surface_volume/[image_id].tif slices from the 3d x-ray surface volume. Each file contains a greyscale slice in the z-direction. Each fragment contains 65 slices. Combined this image stack gives us width * height * 65 number of voxels per fragment. You can expect two fragments in the hidden test set, which together are roughly the same size as a single training fragment. The sample slices available to download in the test folders are simply copied from training fragment one, but when you submit your notebook they will be substituted with the real test data.

[train/test]/[fragment_id]/mask.png — a binary mask of which pixels contain data.

train/[fragment_id]/inklabels.png — a binary mask of the ink vs no-ink labels.

train/[fragment_id]/inklabels_rle.csv — a run-length-encoded version of the labels, generated using this script. This is the same format as you should make your submission in.

train/[fragment_id]/ir.png — the infrared photo on which the binary mask is based.

sample_submission.csv, an example of a submission file in the correct format. You need to output the following file in the home directory: submission.csv. See the evaluation page for information.


## Models to Explore
TBD


## Analysis
Due to time constraints, we will only be able to analyze the campfire scroll, as it is the smallest of the datasets. TBD
