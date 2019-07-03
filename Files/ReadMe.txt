# README

NewsREEL Multimedia constitutes an evaluation task under the umbrella of the MediaEval Benchmark. Participants evaluate how well they can recommend news articles based on their texts and images.

## Dataset Overview

We consider three data sources:

1. item data
1. image data
1. access data

### Item Data

Item data covers a variety of aspects related to news articles and their images. The file `imagenewsreel-itemData.csv` conveys the following structure:

+ `id` 
+ `imageId` (reference to the image)
+ `text`
+ `publisher` (website publishing the article)
+ `URL` (link to the article; note the text merely captures the first lines of the article. You may scrape the whole text using the URL and a suited scraper)
+ `imageURL` (download the original image)
+ `stemmedText` (textual representation with merely the most essential terms left; note, this has been automatically generated)
+ `date` (publication date)
+ `articleId` (reference to the article)`

In JAVA itemData can be parsed using the following Apache Commons CSV format:
`CSVFormat format = CSVFormat.newFormat(';').withQuote('\"').withEscape('\\');`

The file `imagenewsreel-imagelabels.csv` includes an automatically generate annotation of images.

+ `labelId` (monotonically increasing reference)
+ `articleId` (reference to the article)
+ `position` (note, each article has ten annotations assigned. The position refers to the rank of the label in this list. The lower the position the annotation ranks, the higher the chance that it accurately describes the article's image)
+ `label` (annotation text)
+ `confidence` (confidence with which the label fits the image)
+ `configurationId` (the reference to the configuration of the automatic annotator)

The file `imagenewsreel-lablerconfigurations.csv` specifies the different configurations used to annotate the images.

+ `configurationId` (see `imagenewsreel-imagelabels.csv`)
+ `framework` (framework used for annotation -> either *tensorflow* or *keras*)
+ `model` (model used for annotation -> either *InceptionV3*, *ResNet50*, *VGG16*, or *VGG19*)
+ `annotationTask` (either *Imagenet* or *Imagenet and Human Images*. Note, that the latter distinguishes whether a human is present in the image or not such providing a binary label)

### Image Data

Image data consists of a compressed directory (`netlayers.tgz`) which hold the activation of the third-to-last layer of ImageNet with the corresponding image as input. The images can be linked to the file `imagenewsreel-itemData.csv` attribute `imageId`.

### Access Data

Access stats describe how frequently users read, encounter, and click recommendations articles. The data come summarised for individual weeks. Weeks *00*, *01*, *02* as well as *06*, *07*, and *08* include the statistics. The data in the remaining weeks is left blank. The files obey the following structure:

+ `publisher`
+ `articleId`
+ `impressions` (number of reads of the article)
+ `recommendations` (number times the article has been recommended)
+ `clicks` (number of times users clicked on a recommendation of this article)

## Data Statistics

In total, there are 51,397 images and articles in the dataset. Besides, we provide 1,691 unique labels assigned to the images by automatic annotators. The dataset entails the activation of ImageNet's third-to-last layer for each image. We observe 142 million impressions, 206 million recommendations, and 790 thousand clicks. The data amount to 8.6GB in size.
