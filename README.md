# getting-and-cleaning-data-course-project
==================================================================
Human Activity Recognition Using Smartphones Dataset
==================================================================
Jorge L. Reyes-Ortiz, Davide Anguita, Alessandro Ghio, Luca Oneto.
Smartlab - Non Linear Complex Systems Laboratory
DITEN - Università degli Studi di Genova.
Via Opera Pia 11A, I-16145, Genoa, Italy.
activityrecognition@smartlab.ws
==================================================================

The experiments have been carried out with a group of 30 volunteers within an age bracket of 19-48 years. Each person performed six activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) wearing a smartphone (Samsung Galaxy S II) on the waist. Using its embedded accelerometer and gyroscope, we captured 3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz. The experiments have been video-recorded to label the data manually. The obtained dataset has been randomly partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data. 

The sensor signals (accelerometer and gyroscope) were pre-processed by applying noise filters and then sampled in fixed-width sliding windows of 2.56 sec and 50% overlap (128 readings/window). The sensor acceleration signal, which has gravitational and body motion components, was separated using a Butterworth low-pass filter into body acceleration and gravity. The gravitational force is assumed to have only low frequency components, therefore a filter with 0.3 Hz cutoff frequency was used. From each window, a vector of features was obtained by calculating variables from the time and frequency domain. See 'features_info.txt' for more details. 

For each record it is provided:
======================================

- Triaxial acceleration from the accelerometer (total acceleration) and the estimated body acceleration.
- Triaxial Angular velocity from the gyroscope. 
- A 561-feature vector with time and frequency domain variables. 
- Its activity label. 
- An identifier of the subject who carried out the experiment.

=============================================================


License:
========
Use of this dataset in publications must be acknowledged by referencing the following publication [1] 

[1] Davide Anguita, Alessandro Ghio, Luca Oneto, Xavier Parra and Jorge L. Reyes-Ortiz. Human Activity Recognition on Smartphones using a Multiclass Hardware-Friendly Support Vector Machine. International Workshop of Ambient Assisted Living (IWAAL 2012). Vitoria-Gasteiz, Spain. Dec 2012

This dataset is distributed AS-IS and no responsibility implied or explicit can be addressed to the authors or their institutions for its use or misuse. Any commercial use is prohibited.

Jorge L. Reyes-Ortiz, Alessandro Ghio, Luca Oneto, Davide Anguita. November 2012.
Contact GitHub API Training Shop Blog About
© 2016 GitHub, Inc. Terms Privacy Security Status Help

======================================================



Work done by the script:
========================
1) Merges the training and the test sets to create one data set:

The script will download and unzip the data from "https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip" into the work directory.
Will merge by rows the tables in the files subject_train.txt and subject_test.txt into one table;
Will merge by rows the tables in the files Y_train.txt and Y_test.txt into one table;
Will merge by rows the tables in the files X_train.txt and X_test.txt into one table;
Finally, it will merge by columns the three above tables into one single table, called "allData".

2) Extracts only the measurements on the mean and standard deviation
for each measurement:

The script will load the table from features.txt;
Will calculate a vector "posMeanStd" with the position which the columns names (of the table loaded from file features.txt) have "mean" or "std" on it;
Will subset the "allData" table keeping the first two columns and the columns corresponding to the vector "posMeanStd". Creating a new table called "meanAndStd".

3) Uses descriptive activity names to name the activities in the data set:

Load the table from activity_labels.txt;
Merge this table with the table "meanAndStd".

4) Appropriately labels the data set with descriptive variable names:

The script will perform a series of modifications to the columns names of the table "meanAndStd":
Converte all "-" into "_";
Removing "()";
Removing redudante names (e.g BodyBody to Body);
Changing "Acc" to "Acc_";
Changing "Body" to "Body_";
Changing "Gyro" to "Gyro_";
Changing "Jerk" to "Jerk_";
Changing "meanFreq" to "mean_Freq";
Change the names of the first two columns to Activity_ID and Subject.

5）Creates a second, independent tidy data set with the average of each variable for each activity and each subject.

All the columns from "meanAndStd" table with the exception of the first two and the last one, will be considered measure Variables;
Meting "meanAndStd" using the measure variables defined and as Id the columns "Subject", "Activity_ID" and "Activity_Name". Creating a new variable dataMelt.
Then the script will Cast the "dataMelt" using the formula : Subject + Activity_Name ~ variable. And the aggregate function mean.

Finally, the script will save the new tidy data into a file called tidyData.txt.
