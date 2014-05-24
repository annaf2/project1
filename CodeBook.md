Human Activity Recognition Using Smartphones Tidy Dataset 
================================================================== 

Original Data Description
-------------------------
This script takes and modifies the  data Human Activity Recognition Using Smartphones Dataset
Version 1. It was collected from the accelerometers from the Samsung Galaxy S smartphone. The data comes from 
http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones 

The experiments have been carried out with a group of 30 volunteers (refferred in data set as numbers from 1 to 30 in 'subject'). Each person performed six activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) wearing a smartphone (Samsung Galaxy S II) on the waist. The sensor acceleration signal, which has gravitational and body motion components, was separated he features selected for this database come from the accelerometer and gyroscope 3-axial raw signals tAcc-XYZ and tGyro-XYZ. These time domain signals (prefix 't' to denote time) were captured at a constant rate of 50 Hz. Then they were filtered using a median filter and a 3rd order low pass Butterworth filter with a corner frequency of 20 Hz to remove noise. Similarly, the acceleration signal was then separated into body and gravity acceleration signals (tBodyAcc-XYZ and tGravityAcc-XYZ) using another low pass Butterworth filter with a corner frequency of 0.3 Hz.   

Subsequently, the body linear acceleration and angular velocity were derived in time to obtain Jerk signals (tBodyAccJerk-XYZ and tBodyGyroJerk-XYZ). Also the magnitude of these three-dimensional signals were calculated using the Euclidean norm (tBodyAccMag, tGravityAccMag, tBodyAccJerkMag, tBodyGyroMag, tBodyGyroJerkMag).   

Finally a Fast Fourier Transform (FFT) was applied to some of these signals producing fBodyAcc-XYZ, fBodyAccJerk-XYZ, fBodyGyro-XYZ, fBodyAccJerkMag, fBodyGyroMag, fBodyGyroJerkMag. (Note the 'f' to indicate frequency domain signal). 

These signals were used to estimate variables of the feature vector for each pattern:  
'-XYZ' is used to denote 3-axial signals in the X, Y and Z directions.

tBodyAcc-XYZ
tGravityAcc-XYZ
tBodyAccJerk-XYZ
tBodyGyro-XYZ
tBodyGyroJerk-XYZ
tBodyAccMag
tGravityAccMag
tBodyAccJerkMag
tBodyGyroMag
tBodyGyroJerkMag
fBodyAcc-XYZ
fBodyAccJerk-XYZ
fBodyGyro-XYZ
fBodyAccMag
fBodyAccJerkMag
fBodyGyroMag
fBodyGyroJerkMag

The set of variables that were estimated from these signals include: 

mean(): Mean value
std(): Standard deviation
bandsEnergy(): Energy of a frequency interval within the 64 bins of the FFT of each window.
angle(): Angle between to vectors.

Additional vectors obtained by averaging the signals in a signal window sample. These are used on the angle() variable:

gravityMean
tBodyAccMean
tBodyAccJerkMean
tBodyGyroMean
tBodyGyroJerkMean

There more features in the original data set, but for out purposes we only need these. Detailed description can be fount in file features_info.taxt of the original data set (see section Data Structure ).
Features are normalized and bounded within [-1,1]. Each feature vector is a row on the text file.

Objectives
--------------------
The purpose of the assignment is to transform the origignal data set to a tidy data set.
The tidy data set we obtain should comply with the following: 
* training and the test sets are merged to create one data set.
* only the measurements on the mean and standard deviation for each measurement are provided. 
* activity names are descriptive
* tidy data set is appropriatly labeled with descriptive activity names. 
* tidy data set has only the average of each variable for each activity and each subject.

Original data structure
-----------------------
The dataset includes the following files:

- README.txt:provides general info about data set
- features_info.txt: Shows information about the variables used on the feature vector.
- features.txt: List of all features.
- activity_labels.txt: Links the class labels with their activity name.
The following files are available for the train and test data. Their descriptions are equivalent.
- train/X_train.txt: Training set.
- train/y_train.txt: Training labels.
-train/subject_train.txt': Each row identifies the subject who performed the activity for each window sample. Its range is from 1 to 30. 
- train/Inertial Signals: directory that contains unprocessed information on acceleration and angular velocity vectors in standard units for each window and axis. For our purposes we only need the mean and standard deviation variables of processed variables, so these subfolders are not touched by the data transformation process.

The original data to be modified is obtained at 
https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip

Modifying Data
--------------------
First, we read the files with the data we need from original data set: 'features.txt', 'activity_labels.txt','train/X_train.txt','train/Y_train.txt','train/subject_train.txt', 'test/X_test.txt','testn/Y_test.txt','test/subject_test.txt'.  Note, that subfolders  "/Inertial Signals" are not read, as they do not contain information I need in the tidy data set.


I merge the training and the test sets to create one data set, according to the scheme: 

features | activitiy | subject     
X_test   | Y_test    |subject_test  
X_train  | Y_train   |subject_train  

The data contains 10299 rows and 563 variables: 561 feature variables, activity variable and subject variable. Feature variables were treated as numeric, according to the nature of fetures. Activities, represented by numbers in the original data set, were subsituted by corresponding activity from activity_labels.txt. At this point activity variable is represented as character and  subject variable as integer for the purpose of easier data transformations inside the script. The assignment did not require  the it to be presented, so I consider it as a transition data set. 
I labeled the variables with variable names from features.txt. The names were turned into more conventional R format: defices, commas and parenthis excluded, letters starting new word capitalised. However, I left short names used in original dataset (like Acc for acceleration) to make long variable names as compromse between variable name being  understandable and readable atthe same time. For the same reason feature names, including frequency intervals (like fBodyAccJerkBandsEnergy1,24) are not stripped of ",". As mentioned earlier this should not cause incinvinience, as the data set, that include these features is transitional.

For the new tidy data set I extracted only the measurements of the mean and standard deviation for each measurement. As a result 79 features were left, including mean for frequency data obtained by averaging the signals in a signal window sample, as this represent the mean parameter. However, variables representing angle between vectors are excluded, as they measure angle between vectors, even if the vector(s).(See full list in section Tidy Data Set.)

For these data set avarage of each feature for each activity and each subject were calculated, using aggregate() function. In complience with the nature of subject and activity, corresponding variables were turned into factors. 
Therefore 180 (6 activity levels and 30 subject levels) rows were left for the tidy data set. 


Tidy Data Set
--------------------

The tidy data set is exported to the file to the working directory under the name tidyData.txt (separator " ").
It consisits of 81 variable:
* subject: factor with levels from 1 to 30, representing subjects perfoming the experiment
* activity: factor with 6 levels (LAYING, SITTING, STANDING, WALKING, WALKING_DOWNSTAIRS, WALKING_UPSTAIRS), representing the activity performing by each subject
* 79 numeric feature variables, representing measurment taken for the subject during the activity:
tBodyAccMeanX               tBodyAccMeanY                tBodyAccMeanZ                
tBodyAccStdX                tBodyAccStdY                 tBodyAccStdZ                 
tGravityAccMeanX            tGravityAccMeanY             tGravityAccMeanZ             
tGravityAccStdX             tGravityAccStdY              tGravityAccStdZ              
tBodyAccJerkMeanX           tBodyAccJerkMeanY            tBodyAccJerkMeanZ            
tBodyAccJerkStdX            tBodyAccJerkStdY             tBodyAccJerkStdZ             
tBodyGyroMeanX              tBodyGyroMeanY               tBodyGyroMeanZ               
tBodyGyroStdX               tBodyGyroStdY                tBodyGyroStdZ                
tBodyGyroJerkMeanX          tBodyGyroJerkMeanY           tBodyGyroJerkMeanZ           
tBodyGyroJerkStdX           tBodyGyroJerkStdY            tBodyGyroJerkStdZ            
tBodyAccMagMean             tBodyAccMagStd               tGravityAccMagMean           
tGravityAccMagStd           tBodyAccJerkMagMean          tBodyAccJerkMagStd           
tBodyGyroMagMean            tBodyGyroMagStd              tBodyGyroJerkMagMean         
tBodyGyroJerkMagStd         fBodyAccMeanX                fBodyAccMeanY                
fBodyAccMeanZ               fBodyAccStdX                 fBodyAccStdY                 
fBodyAccStdZ                fBodyAccMeanFreqX            fBodyAccMeanFreqY            
fBodyAccMeanFreqZ           fBodyAccJerkMeanX            fBodyAccJerkMeanY            
fBodyAccJerkMeanZ           fBodyAccJerkStdX             fBodyAccJerkStdY             
fBodyAccJerkStdZ            fBodyAccJerkMeanFreqX        fBodyAccJerkMeanFreqY        
fBodyAccJerkMeanFreqZ       fBodyGyroMeanX               fBodyGyroMeanY               
fBodyGyroMeanZ              fBodyGyroStdX                fBodyGyroStdY                
fBodyGyroStdZ               fBodyGyroMeanFreqX           fBodyGyroMeanFreqY           
fBodyGyroMeanFreqZ          fBodyAccMagMean              fBodyAccMagStd               
fBodyAccMagMeanFreq         fBodyBodyAccJerkMagMean      fBodyBodyAccJerkMagStd       
fBodyBodyAccJerkMagMeanFreq fBodyBodyGyroMagMean         fBodyBodyGyroMagStd          
fBodyBodyGyroMagMeanFreq    fBodyBodyGyroJerkMagMean     fBodyBodyGyroJerkMagStd      
fBodyBodyGyroJerkMagMeanFreq
Detailed description is provided above in the section Original Data. 
	
Each of 180 rows represent avarage value (obtained from original data set)  of the corresponding feature for each subject and each activivty.
Features are normalized and bounded within [-1,1]. Observations are sorted first by activity then by subject. There are no NAs in the data.

