# HuBMAP - Hacking the Human Vasculature Kaggle competition
![hubmap-long](https://github.com/theros88/hubmap-vasculature/assets/103253087/d5a34ef3-6317-429b-811e-ca11b13b9e3a)
The latest HuBMAP kaggle competition is on! This time it is about "Hacking the Human Vasculature".

The goal of this competition is to segment instances of microvascular structures, including capillaries, arterioles, and venules. We will have to create a model trained on 2D PAS-stained histology images from healthy human kidney tissue slides. The model will be able to locate microvasculature structures (blood vessels) within human kidney histology slides.

For more detailed information check: [HuBMAP - Hacking the Human Vasculature](https://www.kaggle.com/competitions/hubmap-hacking-the-human-vasculature/overview)

In this repository the code, notebooks and tchniques which will be used in the competition will be archived and logged.

## EDA
The first EDA on the images provided by the competition and its datasets is performed in order to have a much more clear understanding and deeper insights on the data. It is foreseen that cutting-edge instance segmentation models must be used and Semi-Supervised/Unsupervised Learning techniques in order to achieve optimum results.

If you would like to run the EDA notebook locally, you will have first to download the dataset of the competition to your machine:

`kaggle competitions download -c hubmap-hacking-the-human-vasculature`

Then you can unzip the data to a directory and run the EDA notebook from this directory 

## Creating a baseline
Based on the findings in the EDA notebook, a stohastic submission was performed in order to get a first baseline on the hidden test data of the competition. The notebook produced random sized ellipsis of blood vessels and glomerulus based on the statistical characteristics described in EDA, but this produced no results as the resulting score of this attempt was 0.  

The next step is to train a baseline instance segmentation model to get some first results on the problem at hand. A [Detectron2](https://github.com/facebookresearch/detectron2) pre-trained model was used. More specifically a Mask R-CNN model with FPN and a ResNet-101 as backbone is pre-trained on the COCO dataset and this was fine-tuned on the competition's dataset. Basic augmentations were applied to the dataset like `RandomFlip`, but other than that the training was as simple as it could be with only 5000 iterations due to the large size of it as it converged quite fast. The model was trained in a Colab notebook with a Tesla T4 GPU in less than 25 minutes. The training details and other nuances can be seen in the notebook `HuBMAP_HHV_Detectron2_Baseline.ipynb`.

The results of this baseline are the following. By evaluating the model, we got an `APm:34.14` at segmentation. It was easier for the model to discern the `glomerulus` class with a score of `AP:60` and less so for the blood vessels at an accuracy of about `AP:27`. When the model was tested on the public test dataset of the competition, it achieved a score of about `0.3` (Public score: 0.294). It is observed though, that a quite low threshold (below 0.1) for the blood vessel instances' confidence score of the model should be set to achieve this score. The glomerulus threshold was set at 0.2 .

The inference process and how it was achieved, can be seen in the `HubMAP-HHV_baseline_inference.ipynb` notebook.
