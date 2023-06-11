
Detecting Ink on Ancient Papyrus Texts
CS 472 Final Project Proposal
Cheyanne Kester 
Seth Palmer 
Maddie Porcaro 

The Problem
Pompeii and nearby Herculaneum were devastated by the eruption of Mount Vesuvius in AD 79, which caused hundreds of ancient scrolls in the library of a grand luxury villa to be carbonized by the intense blast of hot gas, rendering them completely unreadable. However, researchers are now embarking on a worldwide competition to decipher the charred papyri, following a successful demonstration that an artificial intelligence program can extract letters and symbols from high-resolution X-ray images of the delicate, unrolled documents.

The Vesuvius Challenge is a global competition launched by the Institute for the Study of Ancient Worlds at New York University and the University of Naples Federico II to decipher these ancient scrolls. Participating teams will compete for a grand prize of $150,000, awarded to the first team to decipher four passages of text from the inner layers of the scrolls before the end of 2023. Additionally, progress prizes include $50,000 for accurately identifying ink on the papyri from the 3D X-ray scans. 

The challenge’s Kaggle page can be found at the following webpage: 
Vesuvius Challenge - Ink Detection | Kaggle 

For our final project, we wish to cast our own solution model for identifying ink to aid in this endeavor. Due to time constraints and the sheer size of the datasets, we are only going to analyze the campfire scroll as it’s the smallest of the datasets which makes it more manageable.


The Dataset
The team of scientists, led by Professor Brent Seales, a computer scientist at the University of Kentucky, is making its software and thousands of 3D X-ray images of two rolled-up scrolls and three papyrus fragments available for the Vesuvius Challenge.

The Kaggle competition provides the following data sets for use in the competition (descriptions taken directly from competition page):
[train/test]/[fragment_id]/surface_volume/[image_id].tif slices from the 3d x-ray surface volume. Each file contains a greyscale slice in the z-direction. Each fragment contains 65 slices. Combined this image stack gives us width * height * 65 number of voxels per fragment. You can expect two fragments in the hidden test set, which together are roughly the same size as a single training fragment. The sample slices available to download in the test folders are simply copied from training fragment one, but when you submit your notebook they will be substituted with the real test data.
[train/test]/[fragment_id]/mask.png — a binary mask of which pixels contain data.
train/[fragment_id]/inklabels.png — a binary mask of the ink vs no-ink labels.
train/[fragment_id]/inklabels_rle.csv — a run-length-encoded version of the labels, generated using this script. This is the same format as you should make your submission in.
train/[fragment_id]/ir.png — the infrared photo on which the binary mask is based.
sample_submission.csv, an example of a submission file in the correct format. You need to output the following file in the home directory: submission.csv. See the evaluation page for information.

Models to Explore
The most promising model to explore is a neural network model. With a combination of multiple classes as well as several ways to represent a single class, finding a method to linearize this type of data is highly challenging, if not improbable. Therefore, using a neural network will more easily allow us to separate this data, considering the likely non-linear nature of these data points. The inputs for all the models we explore will consist of a vector of a rectangle that roughly matches the size of the letters, enabling us to identify individual letters and determine their precise location in the image. The output of all the models will consist of a vector representing all letters we are searching for, along with a non-character. There is a good chance that the input will contain whitespace or be positioned between two or more characters.

Analysis
We have chosen to focus on the smaller datasets provided by the Kaggle post. Our plan is to allocate approximately 70% of the data for training, 20% for testing our models, and the final 10% for validating our results. We also intend to train several models with different parameters to compare their accuracy. To ensure a fair comparison of their efficacy, we will use the same training, test, and validation sets across all the models. The structure of our model allows us to create a sort of bit map, where each bit represents the model's confidence for each input rectangle as a character. This bit map will facilitate testing and validating our results, as we can convert it into a series of characters or any other format that streamlines the process.


