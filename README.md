# README-help for the submission

DISCLAIMER :: In case you encouter an error while trying to open the jupytr notebooks on the repository or the ones mentioned in the markdown below, kindly refer to this [nbviewer](https://nbviewer.org/github/himeshps/Tidal_Volume_Submission_230478/tree/main/).

Additionally, kindly treat the Augemented_tidal_volume_(female/male)_dataset commits as the final CSV files containing the dataset I had generated for the training of the model. The dataset_male/female CSV commits were generated as well, the only reason to work on them was that I wanted to increase the number of datapoints.

<h1>Starting off with the Dataset</h1>

I started off by searching for the dataset online, expecting that the dataset would be available at the citations of various scientific studies that have been conducted for various features involving tidal volume.

<h3>Sources</h3>

It was pretty difficult for me to figure out a source which could give me the data set involving the features with ample data points as needed to train the model. Therefore, I settled with a rather mathematical approach applying it on the analytical data I got from a [trusted medical source website](https://www.sciencedirect.com/science/article/pii/S1746809422003238?via%3Dihub) . A rather elaborate version of this could be found at this[ link](https://journals.lww.com/md-journal/fulltext/2023/11240/a_prospective_study_on_the_precision_of_height.32.aspx#) . Alongside these, I was constantly referring to [an article](https://www.researchgate.net/figure/CORRELATIONS-BETWEEN-BODY-HEIGHT-BODY-WEIGHT-BMI-AND-TSF_tbl2_26724686) specifically for correlation of BMI with different features. The data received from the sources after going through their journals was not tabulated or any csv form that might help me with the model. The exact methods I employed have been detailed ahead.

<h3>Feature Selection</h3>

The portion above is a concise bibliography to whatever I could find convincing after surfing properly investing quite some time into it. Later, the selection of features was an important step and finally I settled with six features which include Age, Height, Weight, Chest Circumference, BMI (staistically independent of weight and mass, I'll be delievering a proper explaination for the same) and correlating them with the tidal volume. In the second [link](https://journals.lww.com/md-journal/fulltext/2023/11240/a_prospective_study_on_the_precision_of_height.32.aspx#) mentioned above, one can find the various symptoms for respiratory problems included as well, though finally I decided not to include them for the reasons as mentioned. For the purpose of abstraction, I'll refer to my method of obtaining the data points as a statistical process until I detail it well. Given that the data was present in the form of (mean ± S.D) for almost all the features along with exact numerical value of the patients suffering with the specific respiratory symptoms, it would not have been possible for me to determine what exact data points they will correspond to, which happens to be a critical information in such models which are deemed to predict a biological feature. Therefore, I rather settled with creating a model which predicts better on the basis of the chosen features.

<h2>The Dataset Generation Method</h2>

I started off with the raw data at my disposal obtained from the sources listed above. Given the fact that the data was mostly present in the (mean ± S.D) format, I had to obtain such data point distribution that strictly follows the same. This is not my inability to find the dataset, rather I would back this as a creative approach to cater the efficiency of the model. Using the notebooks in the repository, I tried to develop a mutivariate normal distribution such that all the features were correlated with one another so that I could ensure that the each data point was close to the real dataset constituents. I do not mean to say that the real-world data would also follow a normal distribution, it most likely will not but using a correlation matrix method ensures that the biological correlations between the features stays intact and the multivariate normal distribution caters the regression models and also ensures that the spread of the datapoints was within a range obeying the mean and the standard deviations given to us. 

The way the data was presented on the website facilitated the creation as well, the perks being the fact that the correlation values for the features(along with the plots) and the ranges for the spread of the data points was provided already which made verification slightly easier. 

The next step for me was to increase the size of the dataset ( n=300 ) to ( n=600 ) or roughly double it. A few python libraries provide us with the methdods that help us achieve the same using the covariance matrix develop using the means and the standard deviations provided. The code for the same can be found in the [this commit](https://github.com/himeshps/Tidal_Volume_Submission_230478/blob/main/FinalAugmentedMaleDatasetGenerator.ipynb) . Once again, in case there is any error while opening the file, kindly use the nbviewer in the disclaimer right at the top. Therefore, now I had obtained a dataset with 600 datapoints and 6 features which followed a multivariate normal distribution and the features were correlated well too.
