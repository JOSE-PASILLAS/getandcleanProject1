Introduction
One of the most exciting areas in all of data science right now is wearable computing. Companies like Fitbit, Nike, and Jawbone Up are racing 
to develop the most advanced algorithms to attract new users. The data linked to from the course website represent 
data collected from the accelerometers from the Samsung Galaxy S smartphone. 
The experiments have been carried out with a group of 30 volunteers within an age bracket of 19-48 years. Each person performed six activities 
(WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) wearing a smartphone (Samsung Galaxy S II) on the waist. 
Using its embedded accelerometer and gyroscope, we captured 3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz. 
The experiments have been video-recorded to label the data manually. The obtained dataset has been randomly partitioned into two sets, where 
70% of the volunteers was selected for generating the training data and 30% the test data [1]. 

Attribute Information [1]:

For each record in the dataset it is provided: 
- Triaxial acceleration from the accelerometer (total acceleration) and the estimated body acceleration. 
- Triaxial Angular velocity from the gyroscope. 
- A 561-feature vector with time and frequency domain variables. 
- Its activity label. 
- An identifier of the subject who carried out the experiment.

Data information:
- Number of instances=10299
- Number of attributes=561
- Missing values=0
- Donation data=2012/12/10

Data transformations performed for this project:
- Subsetting only to those features related to mean or standard deviation.
- Clean and tidy features. Remove uppercases, and no alfanumeric symbols.
- Add to test and train data their correponding subject and activity labels.
- Merge test set and train set.
- Aggregate the data based in activity and subject.




[1]http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones#