# README-help for the submission

DISCLAIMER :: In case you encouter an error while trying to open the jupytr notebooks on the repository or the ones mentioned in the markdown below, kindly refer to this [nbviewer](https://nbviewer.org/github/himeshps/Tidal_Volume_Submission_230478/tree/main/).

The final model and files for the dataset are listed below : <br>
Final Model : [Link](https://github.com/himeshps/Tidal_Volume_Submission_230478/blob/main/TidalVolume_Final_Model.ipynb) <br>
Final Combined Dataset : [Link](https://github.com/himeshps/Tidal_Volume_Submission_230478/blob/main/FinalCombinedDataset.csv) <br>
Screenshot of the model's prediction : [Link](https://github.com/himeshps/Tidal_Volume_Submission_230478/blob/main/Model%20Working%20Screenshot.png) <br>

The [drive link](https://drive.google.com/drive/folders/1YyJbl091QCw7k1wY9SFvYxwHfPAfLXCW?usp=drive_link) used by me, It is not as helpful for verification as the repo itself, I have dropped the link because I have mounted the drive a lot many times in the notebook for loading the dataset.

Additionally, kindly treat the [FinalCombinedDataset](https://github.com/himeshps/Tidal_Volume_Submission_230478/blob/main/FinalCombinedDataset.csv) commit as the final CSV file containing the dataset I had generated for the training of the model. The dataset_male/female CSV commits were generated as well, the only reason to work on them was that I wanted to increase the number of datapoints. Similar explanation follows up for the augmented datasets you may see on this repository.

<h1>Starting off with the Dataset</h1>

I started off by searching for the dataset online, expecting that the dataset would be available at the citations of various scientific studies that have been conducted for various features involving tidal volume.

<h3>Sources</h3>

It was pretty difficult for me to figure out a source which could give me the data set involving the features with ample data points as needed to train the model. Therefore, I settled with a rather mathematical approach applying it on the analytical data I got from a [trusted medical source website](https://www.sciencedirect.com/science/article/pii/S1746809422003238?via%3Dihub) . A rather elaborate version of this could be found at this[ link](https://journals.lww.com/md-journal/fulltext/2023/11240/a_prospective_study_on_the_precision_of_height.32.aspx#) . Alongside these, I was constantly referring to [an article](https://www.researchgate.net/figure/CORRELATIONS-BETWEEN-BODY-HEIGHT-BODY-WEIGHT-BMI-AND-TSF_tbl2_26724686) specifically for correlation of BMI with different features. The data received from the sources after going through their journals was not tabulated or any csv form that might help me with the model. The exact methods I employed have been detailed ahead.

<h3>Feature Selection</h3>

The portion above is a concise bibliography to whatever I could find convincing after surfing properly investing quite some time into it. Later, the selection of features was an important step and finally I settled with six features which include Age, Height, Weight, Chest Circumference, BMI (staistically independent of weight and mass, I'll be delievering a proper explaination for the same) and correlating them with the tidal volume. In the second [link](https://journals.lww.com/md-journal/fulltext/2023/11240/a_prospective_study_on_the_precision_of_height.32.aspx#) mentioned above, one can find the various symptoms for respiratory problems included as well, though finally I decided not to include them for the reasons as mentioned. For the purpose of abstraction, I'll refer to my method of obtaining the data points as a statistical process until I detail it well. Given that the data was present in the form of (mean ± S.D) for almost all the features along with exact numerical value of the patients suffering with the specific respiratory symptoms, it would not have been possible for me to determine what exact data points they will correspond to, which happens to be a critical information in such models which are deemed to predict a biological feature. Therefore, I rather settled with creating a model which predicts better on the basis of the chosen features.

<h2>The Dataset Generation Method</h2>

I started off with the raw data at my disposal obtained from the sources listed above. Given the fact that the data was mostly present in the (mean ± S.D) format, I had to obtain such data point distribution that strictly follows the same. This is not my inability to find the dataset, rather I would back this as a creative approach to cater the efficiency of the model. Using the notebooks in the repository, I tried to develop a mutivariate normal distribution such that all the features were correlated with one another so that I could ensure that the each data point was close to the real dataset constituents. I do not mean to say that the real-world data would also follow a normal distribution, it most likely will not but using a correlation matrix method ensures that the biological correlations between the features stays intact and the multivariate normal distribution caters the regression models and also ensures that the spread of the datapoints was within a range obeying the mean and the standard deviations given to us. 

The way the data was presented on the website facilitated the creation as well, the perks being the fact that the correlation values for the features(along with the plots) and the ranges for the spread of the data points was provided already which made verification slightly easier. The process to find the correlation coefficient values was rather straightforward. Given the fact that I could get most from the source itself, for the rest I employed the usage of calculating a mean correlation value given that the pair of concerned features showed different behaviour against one another in different age groups (which mind you, was not an issue as the dataset is spread over a range of 12-98 years of age, the feature of age here is just for an example though has been used directly in the code too ).

The next step for me was to increase the size of the dataset ( n=300 ) to ( n=600 ) or roughly double it. A few python libraries provide us with the methdods that help us achieve the same using the covariance matrix develop using the means and the standard deviations provided. The code for the same can be found in the [this commit](https://github.com/himeshps/Tidal_Volume_Submission_230478/blob/main/FinalAugmentedMaleDatasetGenerator.ipynb) . Once again, in case there is any error while opening the file, kindly use the nbviewer in the disclaimer right at the top. Therefore, now I had obtained a dataset with 600 datapoints and 6 features which followed a multivariate normal distribution and the features were correlated well too. <br>
Lastly, an additional step was the combination of both male and female datasets by the gender coding in the form of bits 0 and 1. Thus, it gave me a dataset of 288 datapoints for the training of the model. Therefore, this culminated the process of dataset retrieval from the source.

<h1> Working with the model </h1>

The chronology to follow in the jupytr notebooks is as follows.<br>
[TidalVolumePrediction](https://github.com/himeshps/Tidal_Volume_Submission_230478/blob/main/TidalVolumePrediction.ipynb) is the initial notebook I had created to compare and validate all the models I had chosen against one another. This notebook consists of the models like Linear Regression, Random Forest regression, Gradient Boost regression and support vector machine. <br>
At this point, I wish to address a question which might be raised, I have not chosen a neural network modelling for the submission and the size of my dataset provides an explaination to that, it is obvious that the neural network will end up memorizing the datapoints and would perform poorly on a new data whereas the regression models fare well in doing it when the relationships are not that complex amoungst the features. I personally did not find any reason convincing enough to train neural networks for the same and that surely does not imply that I do not have an experience with them. The fortnight around the spring camp was based on them and I have gained enough knowledge about it there. <br>
Now, I had chosen r^2 value and the mean squared error (also the mean absolute error) as the metrics to compare the models.<br>
Where the r squared value captures the variance covered by the developed model, mean errors take care of the absolute errors in the prediction made.<br>
The r squared value for the model turned out to be 0.77 which was fairly accurate with a mean absolute error of around 23-25 ml for a mean of 510 ml in either dataset predictions which lowered the margin of variability and this is evident in the prediction plot I have included in the notebook itself. <br>
After this comparison of the models, it was the time for me to see if the predictions made can be refined and made more accurate any further. That is where, I tried to implement regularisation( L1,L2 and Elastic-net) to see if there is a significant increase/change in the accuracy of the predictions made. t turned out that the methods did not change the accuracy substantially and I had to stick with the original model itself. I had also implemented a few ensemble method but they threw the same ballpark efficiency in prediction and I did not have a solid evidence to choose them over the existing model.Additionally to check how the correlation matrix and the relations defined by it have had a say in the correlations between the feature , I checked the variance Inflation factor which give me an idea that a further refinement to the regression model might not be feasible as the features are already heavily correlated on each other.All of this is covered in [this notebook](https://github.com/himeshps/Tidal_Volume_Submission_230478/blob/main/ModifyingLinearRegression.ipynb).<br>
Hence, finally settling with the regression model as linked initially in this markdown file.

Yay! A working model that can predict tidal volume based on the respective features.
[picture](https://github.com/himeshps/Tidal_Volume_Submission_230478/blob/main/Model%20Working%20Screenshot.png)
