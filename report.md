# Detecting Ink on Post-Volcanically Carbonized Papyri
Using a Neural Network
Seth Palmer, Maddie Porcaro, Cheyanne Kester 


## Abstract
In this report, we will explore and test the ability of a UNet neural network in the detection of ink on fossilized papyrus texts from 79 AD. Our goal, both due to time constraints and current competitors of the Vesuvius challenge obtaining up to 90% accuracy, is to achieve 50% accuracy on ink detection. Our final solution produced a validation accuracy of 76% with an average loss of 0.38 using the Binary Intersection over the Union loss function.

## I. Introduction	
The devastation caused by the eruption of Mount Vesuvius in 79 AD not only claimed countless lives but also dealt a severe blow to the preservation of knowledge and history. Pompeii and nearby Herculaneum were among the cities profoundly affected, with one grand luxury villa losing its precious library of ancient scrolls. The intense blast of hot gas during the eruption carbonized the scrolls, rendering them completely unreadable for centuries. However, there is new hope on the horizon as researchers embark on a worldwide competition to decipher these charred papyri. Their efforts have been bolstered by a groundbreaking discovery – an artificial intelligence program capable of extracting letters and symbols from high-resolution X-ray images of these delicate, unrolled documents.

In light of this promising development, our proposed solution aims to utilize a neural network model to tackle the daunting challenge of detecting ink on charred papyri. The use of a neural network is crucial due to the complex nature of the data. The task involves combining multiple classes and finding ways to represent a single class through various means. The inherent difficulty in linearizing such data makes conventional methods highly challenging, if not improbable.

In this endeavor, we recognize the significance of unraveling the secrets contained within these ancient texts. The recovered knowledge from these carbonized papyri has the potential to reshape our understanding of history, culture, and the intellectual achievements of the ancient world. Moreover, the successful application of artificial intelligence and neural networks in this field can pave the way for future breakthroughs in deciphering and preserving other valuable documents that have remained enigmatic for centuries.

## II.  Background
The problem we are trying to solve is to recognize ink in the papyrus scrolls. To evaluate this, we have access to a 3D volume scan of the scrolls, which has been segmented into individual scans for easier processing of information. The goal of this model is to infer from the volumes where the ink is within the scan. The desired data is a 2D map of the probability that there is ink in that corresponding spot. In other words, we were compressing the 3D volume into a 2D map of where the ink might be. Thus we needed a model that can do this. This logically led to models that are suited for image recognition and computer vision. The scans used in the base datasets were already sliced from 3D to 2D, which let us focus on refining our methods for our experiments. 

## III.  Methods	
To jumpstart our work, the competition provided some starter code to help new competitors get up to speed on the progress that had been made so far along with using a neutral network architecture called UNet to segment the scans of the scrolls. However, along with testing a standard U-Net model, we also wanted to test this model with some common additions to these kinds of encode-decode networks such as skip connections and both forward and backward residual connections. The connections not only allowed for a more complex model but also helped with some common problems the vanille UNet model suffered from. Problems such as gradient vanishing and since we do not need the individual encoding and decoding sections we could connect them to make better inferences from the volume. We also wanted to use some basic overfitting prevention techniques as our initial search for potential models led to solutions with a tendency for overfitting if not fine-tuned precisely. Some of these techniques we wanted to include were dropout layers, batch size, weight regulation, and so on. 
Development took place primarily on Google Colab due to its versatility and it’s storage capacity, as the data we needed to use was too large to hold on any of the machines at our disposal. 

## IV.  Experiments	
Our experiments mostly consisted of fine-tuning the hyperparameters needed for our neural network, specifically the dropout rate, learning rate, kernel initializer, and loss function parameters. The specific process and trials of finding the ideal state of these hyperparameters are as follows:

### i. Dropout Rate
Fine-tuning the dropout rate for the model was a fairly straightforward task, as we only had to adjust a single decimal to be between .2 and .8. For the best results, we used a dropout rate of .2. While not the most significant of hyperparameters for accuracy, the dropout rate was crucial for limiting the overfitting of the model. The experiment results used to find this are below.
ii. Learning Rate
Like the dropout rate, fine-tuning the learning rate for the model was streamlined, as we only had to adjust a single decimal to be between .01 and .0001. For the best results, we used 0.001. The experiment results are below.

### iii. Kernel Initializer
In any neural network, initializing weights is crucial to the model’s validation loss. There were four potential initializers that could be used, Glorot Normal, Glorot Uniform, HE Normal, and HE Uniform, though we found that Glorot Normal was the best.


### iv. Loss Function & Parameters
Through extensive experimentation, the one parameter that has had the biggest influence on our model is the loss function used. Our experimenting has incorporated 4 different loss functions including, binary cross-entropy, binary focal cross-entropy, Tversky loss, and Log Cosh Dice loss. We chose these functions because going through models that could solve our problem we also came across common loss functions and these four came up most frequently (excluding binary intersection over union loss). So along with trying these different functions our tuning algorithm also searched through their appropriate parameters (if they had any we were interested in tuning). Three of our loss functions had parameters to tune while the binary cross entropy didn’t have any significant ones to tune. Our tuner discovered that the binary cross entropy had the best performance in terms of validation accuracy and validation loss. However, it’s worth mentioning that, when tuned for the Tversky loss function, the predictive output gave more definitive output which could lead to a better loss function given a more suited model to accompany it.

The results of each experiment are represented by this graph:


## V. Interpretations of Results
Based on the results of our experiments, our team interprets our solution to have a generally positive impact, with a few caveats. Due to time constraints, we were not able to eliminate the possibility of overfitting in our model, so if this solution were to be continued by other developers or by members of this team, it would require further fine-tuning to reduce this possibility. Additionally, whilst our final validation accuracy was quite promising, and well above our goal, it would need to be much higher, preferably in the 90% range, to be used in any professional setting. This preferred accuracy could be attained in part with further hyperparameter tuning, we would even recommend restarting the finetuning process to be completely sure of the correct values. However, we realize that our architecture itself might not be perfectly structured to fit this problem, and would need restructuring to attain higher accuracy readings. 

## VI. Contributions
Cheyanne: Created and updated the project GitHub and its ReadMe file, and headed the writing for the project’s proposal and final report. 
Maddie: Set up Google CoLab file, found the Vesuvius Challenge starter code and data, helped organize the GitHub, and aided in writing the project proposal and final report.
Seth: Hyperparameter and program optimization and fine-tuning using Tensorflow. Chief programmer of the Google Colab notebook used in our solution.

## VII. Conclusion	
The devastating eruption of Mount Vesuvius in 79 AD not only caused immense loss of life but also dealt a significant blow to the preservation of knowledge and historical records. Ancient scrolls found in a private villa had been carbonized due to the eruption, and have since been impossible to read. However, with recent advances in AI technology, there is hope that the knowledge once trapped inside the papyri may be discovered again.

Our proposed solution focuses on employing a neural network model to tackle the formidable challenge of detecting ink on the carbonized papyri. The utilization of a neural network is vital due to the intricacies involved in handling the complex data. These additions include but are not limited to skip connections and backward residual connections. Our engineers, Madeline Porcaro and Seth Palmer headlined this effort and managed to attain a validation accuracy of 76% with an average loss of 0.38 using the Binary Intersection over Union loss function.
In our solution, Seth Palmer utilized the Keras Tuner library to expedite the tuning process for the UNet model, a type of neural network. This tuning aimed to optimize critical hyperparameters including the dropout rate, loss functions and their parameters, learning rate, and kernel initializers. Choosing the scope of the search space was also facilitated by Seth, the decision to use a large search space was used in order to find a near-optimal set of hyperparameters quicker.

While it is important to note that our development process may have introduced overfitting issues, time constraints prevent us from rectifying them without jeopardizing our results. As all members of our team are seniors preparing to transition to new opportunities, we regretfully inform readers that we will not be able to continue this project. Nonetheless, we remain optimistic about the potential impact of ongoing research in this field and the broader implications it may have for understanding and preserving our shared human history.

## VIII. References	
Vesuvius Challenge - ink detection. Kaggle. (n.d.). https://www.kaggle.com/competitions/vesuvius-challenge-ink-detection/overview
Fchollet. (2023, April 12). Keras starter kit: Unet + train on full dataset. Kaggle. https://www.kaggle.com/code/fchollet/keras-starter-kit-unet-train-on-full-dataset

GitHub Link:
https://github.com/ckester23/CS472FinalProject 
Google Colab:
https://colab.research.google.com/drive/1EB6g5JF4hMHUOxUX34IqtVpnWpug3e0u 
Datasheets:
Original: https://docs.google.com/spreadsheets/d/1TY6vQi5VY_YlNHB9O6tFuoUTfOTNpNFFQBK6CxzP3VY/edit#gid=2040560680 
Revised (with graphs used in this report): https://docs.google.com/spreadsheets/d/1i78E94-SZc7YH6pnRRvwkG6rwwrcEiJ4V-eeLTO10B0/edit#gid=2040560680 



