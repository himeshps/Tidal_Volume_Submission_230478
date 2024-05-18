# README-help for the submission

<h1>Starting off with the Dataset</h1>

I started off by searching for the dataset online, expecting that the dataset would be available at the citations of various scientific studies that have been conducted for various features involving tidal volume.

<h3>Sources</h3>

It was pretty difficult for me to figure out a source which could give me the data set involving the features with ample data points as needed to train the model. Therefore, I settled with a rather mathematical approach applying it on the analytical data I got from a [trusted medical source website](https://www.sciencedirect.com/science/article/pii/S1746809422003238?via%3Dihub) . A rather elaborate version of this could be found at this[ link](https://journals.lww.com/md-journal/fulltext/2023/11240/a_prospective_study_on_the_precision_of_height.32.aspx#) . Alongside these, I was constantly referring to [an article](https://www.researchgate.net/figure/CORRELATIONS-BETWEEN-BODY-HEIGHT-BODY-WEIGHT-BMI-AND-TSF_tbl2_26724686) specifically for correlation of BMI with different features. The data received from the sources after going through their journals was not tabulated or any csv form that might help me with the model. The exact methods I employed have been detailed ahead.

<h3>Feature Selection</h3>

The portion above is a concise bibliography to whatever I could find convincing after surfing properly investing quite some time into it. Later, the selection of features was an important step and finally I settled with six features which include Age, Height, Weight, Chest Circumference, BMI (staistically independent of weight and mass, I'll be delievering a proper explaination for the same) and correlating them with the tidal volume. In the second [link](https://journals.lww.com/md-journal/fulltext/2023/11240/a_prospective_study_on_the_precision_of_height.32.aspx#) mentioned above, one can find the various symptoms for respiratory problems included as well, though finally I decided not to include them for the reasons as mentioned. For the purpose of abstraction, I'll refer to my method of obtaining the data points as a statistical process until I detail it well. Given that the data was present in the form of (mean +- S.D) for almost all the features along with exact numerical value of the patients suffering with the specific respiratory symptoms, it would not have been possible for me to determine what exact data points they will correspond to, which happens to be a critical information in such models which are deemed to predict a biological feature. Therefore, I rather settled with creating a model which predicts better on the basis of the chosen features.

<h2>The Dataset Generation Method</h2>

My approach from this point was to employ the usage of a correlation matrix so that it helps me to convert the given data into multiple data points following multivariate normal and correlated distribution which in turn would have helped me in implementing the models and cpmparing their performances. To determine the generation of the dataset, I used python libraries and coded for the same as required by some statistical analysis. I have also added the Colab file for the dataset generation in the repository along with the dataset used by me. Kindly refer to it for any verification or critique upon my method of obtaining the dataset for the same.
