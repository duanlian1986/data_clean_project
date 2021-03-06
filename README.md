##README
This file is used to describe how run_analysis.R works.
run_analysis.R can be run as long as the Samsung data is in the working directory

##Script Description
###Load packages

library("dplyr")
library("reshape2")

### 1. The first task is to merges the training and the test sets to create one 
data set, steps 1.1-1.5 are for this purpose
### 1.1 read in files

X_test <- read.table("X_test.txt")
subject_test <- read.table("subject_test.txt")
y_test <- read.table("y_test.txt")
X_train <- read.table("X_train.txt")
subject_train <- read.table("subject_train.txt")
y_train <- read.table("y_train.txt")
features <- read.table("features.txt")

### 1.2 change column names

names(X_test) <- features$V2
names(X_train) <- features$V2
names(subject_test) <- "subject"
names(subject_train) <- "subject"
names(y_test) <- "activity"
names(y_train) <- "activity"

### 1.3 column bind subject_test, y_test, X_test

test <- cbind(subject_test, y_test, X_test)

### 1.4 colum bind subject_trian, y_train, X_train

train <- cbind(subject_train, y_train, X_train)

### 1.5 row bind test and train

test_train <- rbind(test,train)

### 2. The second task is to extracts only the measurements on the mean and std 
for each measurement

test_train_ms <- test_train[,c(1,2,grep("mean|std", colnames(test_train)))]

### 3. The third task is to use descriptive activity names to name the activities 
in the data set

test_train_ms$activity <- gsub("1","WALKING", test_train_ms$activity)
test_train_ms$activity <- gsub("2","WALKING_UPSTAIRS", test_train_ms$activity)
test_train_ms$activity <- gsub("3","WALKING_DOWNSTAIRS", test_train_ms$activity)
test_train_ms$activity <- gsub("4","SITTING", test_train_ms$activity)
test_train_ms$activity <- gsub("5","STANDING", test_train_ms$activity)
test_train_ms$activity <- gsub("6","LAYING", test_train_ms$activity)

### 4. The fourth task is to appropriately labels the data set with descriptive 
variable names, which I alreday did at step 1.2

### 5. The fifth task is from the data set in step4, create a second, independent 
tidy data set with the average of each variable for each activity and each subject.

test_train_group <- group_by(test_train_ms, activity, subject)
test_train_mean <- summarise_each(test_train_group, funs(mean))

### And finally, write out data to a .txt file
write.table(test_train_mean, file="test_train_mean.txt",row.names=FALSE)