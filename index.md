## Welcome to GitHub Pages


## Introduction

In recent years, memes have grown into one of the most widespread forms of content on social media. While generally intended for humor, hateful and misleading content has been on the rise (Fig. 1).  Hence, an effective method of classifying memes into toxic or non-toxic is a major issue to be tackled to ensure a healthy atmosphere online. 

We intend to build a meme classifier that can augment the human moderators in filtering out the toxic ones. The dataset used for the project would include the data from Meta’s Hateful Memes Challenge [3].


## Problem

Due to the massive number of memes being posted on the internet daily, no human team of moderators can effectively filter out every harmful meme containing hate speech, cyberbullying, propaganda, and other toxic behaviors. Therefore, high-bandwidth machine learning algorithms capable of detecting such memes can be extremely helpful in reporting such harmful content. 

Frequently, the harmfulness of a meme is due to the combination of both image and text, e.g. the text may be harmless with a certain background image but harmful when used with another image. Therefore, unimodal models can’t perform the above-mentioned tasks with high accuracy. To tackle this problem, we intend to develop a multimodal model similar to those used in [1,2,4,5] that is capable of classifying harmful memes based on both the background image and embedded text.

## Data Collection

The meme dataset was obtained from Meta’s AI Hateful Meme Challenge Dataset.  The 12,140 memes are pre labeled as 0 (not hateful) or 1 (hateful).  Training set includes 8500 memes and the rest are testing.  Each meme contains a single image and caption.  For clustering, only the training images are used.  External measures are based on the 0 or 1 binary hate classification. 

## Methods

Feature extraction from captions was performed using BERT, a pre-trained neural network to get sentence vectors. Similarly, feature extraction from images was performed using ResNet50, another pre-trained neural network.  Additionally, the layer outputs of both neural networks were saved at each stage of applying the respective model to the dataset.  

Upon generating features, we fuse the features from different stages of the pre-trained neural network. We have 6 combinations in our case. 
1. Early-Early: Early layer features of images and captions.
2. Early-Mid: Early layer features of images and mid layer features of captions.
3. Early-Late: Early layer features of images and late layer features of captions. 
4. Late-Early: Late layer features of images and early layer features of captions.
5. Late-Mid: Late layer features of images and mid layer features of captions.
6. Late-Late: Late layer features of images and late layer features of captions. 

Next, we performed PCA separately on the image and the text features. After reducing the number of components, while preserving 95% of the variance, we tried various algorithms like KMeans, DBSCAN and GMM. We performed a full analysis with GMM as results obtained with DBSCAN algorithm are poor and KMeans is a special case of GMM.

Feature reduction and clustering was explored with PCA, KMeans, DBSCAN, and GMM.  The purpose of this was to reduce features and visualize the high dimensional dataset. For GMM, we performed clustering with both, a full covariance matrix and a spherical covariance matrix. 

--- IMAGE ---

![Meme Image](/Screen Shot 2022-07-16 at 6.44.31 PM.png?raw=true "When memes go extreme. Example taken from [4]")




## Results

We take features obtained from early and later stage layers from ResNET-50 and early, middle and later stage layers from BERT. Using GMM for clustering, we conclude that the features from the 11th layer of the BERT produce the best results individually and results from the fully-connected layer(FC) of ResNET-50 give the best results without data fusion. The results are compiled in Table 1.


# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [Basic writing and formatting syntax](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/NesaraBE/NesaraBE.github.io/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
