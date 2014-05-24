Human Activity Recognition Using Smartphones Tidy Dataset 
================================================================== 
Data
-------------------------
This script takes and modifies the  data collected from the accelerometers from the Samsung Galaxy S smartphone to a tidy data set. The data comes from 
http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones 

The original data to be modified is obtained at 
https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip 

Directory description
-------------------------
The directory consisits of three files:
* README.md: provides directory description (you are reading it right now :))

* CodeBook.md: provides detailed variables description of the data set and modification steps

* run_analisys.R: the script that runs on the data set. The goal is to modify original data set to provide a tidy data set, according to the rules, described in Codebook.md 

Running the script
-------------------------
To obtain a tidy data set for Human Activity Recognition Using Smartphones Data you need to run run_analisys.R. After running the file a tidyData.txt (sep=" ") will appear in your working directory. 

The script uses data.table package. Make sure you have it installed. 

If the R working directory does not contain directory "UCI HAR Dataset",  the script downloads and unzips the file with data. Otherwise proceeds with existing directiry. If you have the "UCI HAR Dataset" directory, it should stay unmodified after being unzipped from Dataset.zip. Otherwise the script will through errors.

WARNING TO FELLOW COURSERA REVIEWERS! Make sure you have the unmodified "UCI HAR Dataset" in your WORKING DIRECTORY. Or you will end up waiting the huuuge file you already have to load again, which is not fun.

