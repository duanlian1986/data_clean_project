###CODEBOOK

The orginal data files that were used in the script are: 
X_test.txt
subject_test.txt
y_test.txt
X_train.txt
subject_train.txt
y_train.txt
features.txt

The files ending with "_test.txt" contain information generated from 
30% volunteers' test data.
The files ending with "_train.txt" contain information generated from
70% volunteers' training data.

The files beginning with "X_" contain: data set
The files beginning with "subject_" contain: row identifies the subject who performed the activity for each window sample. 
Its range is from 1 to 30. 
The files beginning with "y_" contain: test labels

"features.txt" contains the variable names of the data sets
"features_info.txt" has information about the meanning of the variable names.

###Data Manipulations
1. Read in all files listed above
2. Change the column names of X_test and X_train to the variable names in features.txt
3. Change subject_test and subject_train column name to subject
4. Change y_test and y_train column name to activity 
5. Merge "_test.txt" data files to one data set
6. Merge "_train.txt" data files to one data set
7. Combine merged _test data set with merged _train data set
8. Select only the columns containing "mean" or "std" from the combined data set
9. Label the activities to the corresponding names in "activity_labels.txt" file.
10. Group the combined data set by activity and subject
11. Calculate the average values of each variable for each subject and each activity
12. Write out the data to a different .txt file named "test_train_mean.txt".

More information about the experimental details can be found in the README.txt
file of the original data.