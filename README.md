# coursera-getdata-project

Course Project for Coursera Data Science Getting And Cleaning Data class.

This README seeks to accomplish two goals:

- explain how the run_analysis.R script works.
- facilitate evaluation of the Course Project.


## Explanation of the run_analysis.R Script

The `run_analysis.R` script aims to accomplish the following goals:

1. Merges the training and the test sets to create one data set.
2. Extracts only the measurements on the mean and standard deviation for each measurement. 
3. Uses descriptive activity names to name the activities in the data set
4. Appropriately labels the data set with descriptive variable names. 
5. From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.

Please see the `run_analysis.R` script for a detailed description of the implementation of each step used to accomplish the goals.  Here is a high level description of the steps in the script used to accomplish each goal.

To accomplish goal 1, the run_analysis.R script performs the following steps:

1. Creates a "data" directory in which to download the raw data and save the tidy data
2. Downloads and extract the raw data from the internet
3. Reads in the `X_test.txt`, `y_test.txt`, and `subject_test.txt` files into data frames and contatenate the columns into a single data frame.
4. Reads in the train data also.
5. Concatenates the rows of the test and train data.

To accomplish goal 2, the run_analysis.R script performs the following steps:

1. Reads the feature labels from `features.txt`.
2. Filter the feature labels to only those containing 'mean' or 'std' in the name (excluding those containing 'angle', which are angle measurements, not means or standard deviations.
3. Create the corresponding column names (e.g. "V1", "V2") for the filtered feature names
4. Select the columns from the data set that match the selected features.

To accomplish goal 3, the run_analysis.R script performs the following steps:

1. Read in the activity labels and corresponding numeric codes from `activity_labels.txt`.
2. Transform the numeric activity column into a factor column using the numbers and labels read in from `activity_labels.txt`

To accomplish goal 4, the run_analysis.R script performs the following steps:

1. Use the `setnames` function of the `data.tables` library to change the column names of each "V1", "V2", etc., column to the corresponding label previously read in from `features.txt`.

To accomplish goal 5, the run_analysis.R script performs the following steps:

1. melt the data using the "subject" and "activity" columns as ids and all the descriptive column names from goal 4 as the measure variables.
2. Use `dcast` to cast the melted data frame, summarizing each measure variable by the measurements in each subject and activity group.
3. The new data frame was written to a file, "HAR-subject-activity-mean.txt" using the command:

        write.table(mean.data, file="HAR-subject-activity-mean.txt", row.name=FALSE)

   It can be read using the command:

        read.table("HAR-subject-activity-mean.txt", header=TRUE)