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
Based on the findings in the EDA notebook, a stohastic submission will be performed in order to get a first baseline on the hidden test data of the competition. Then we will have to beat this baseline with instance segmentation models. 
[TO BE CONTINUED]
