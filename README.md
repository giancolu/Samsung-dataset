Samsung-dataset
===============
This dataset contain the Human Activity Recognition (HAR) database built from the recordings of 30 subjects performing activities of daily living while carrying a waist-mounted smartphone with embedded inertial sensors.

Preparation of the dataset for the analysis is performed with two R scripts. 

The first (samdata_analysis_code.R) performs thefollowing tasks:

1) checks for the presence of the source dataset in the working directory; 
2) downloads and unzips the source file from the UCI Machine Learning Repository website in the working directory if the source dataset doesn't exist;
3) run the second script.

The second script (run_analysis.R) performs the following tasks:

1. Merges the training and the test sets to create one data set.
2. Extracts only the measurements on the mean and standard deviation for each measurement. 
3. Uses descriptive activity names to name the activities in the data set
4. Appropriately labels the data set with descriptive activity names. 
5. Creates a second, independent tidy data set with the average of each variable for each activity and each subject. 


### Script 1 - samdata_analysis_code.R

Check if "UCI HAR Dataset" folder exists in working dir or download source from the web
```
if (!file.exists("./UCI HAR Dataset")) {
fileUrl <- "https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip" 
download.file(fileUrl, destfile = "UCI_HAR_Dataset.zip", method = "curl")
unzip("./UCI_HAR_Dataset.zip")
} else {
  cat("dir already exist")
}
```

Launch run_analysis.R (script 2) to prepare a tidy dataset from source data
```
cat("I'm running run_analysis.R to prepare a tidy dataset from source data...")
cat("... samsung_dataset_1.csv (dataset1) and samsung_dataset_2.csv (dataset2) will be created") 
source("run_analysis.R")
```

### Script 2 - run_analysis.R

#### CREATING UCI-Samsung Dataset 1:

Crate a dataset of subjects from "subjet_test" and "subject_train" datasets
```
subject.test <- read.table("UCI HAR Dataset/test/subject_test.txt", col.names = "subject.id")
subject.train <- read.table("UCI HAR Dataset/train/subject_train.txt", col.names = "subject.id")
```
Create a dataset of 561 features from "features.txt" and rename them to lower case  
```
features <- read.table("UCI HAR Dataset/features.txt")
feat1 <- tolower(features[,2])
```
Create a dataset of 6 activity labels from "activity_labels.txt" and chage them as factor (6 levels)
```
activity <- read.table("UCI HAR Dataset/activity_labels.txt")
f.activity <- as.character(activity[,2])
```
Create complete test and train datasets
```
x.test <- read.table("UCI HAR Dataset/test/X_test.txt", col.names = feat1) # features data
y.test <- read.table("UCI HAR Dataset/test/y_test.txt", col.names = "activity") # coded activity
test.db <- cbind(subject.test,y.test,x.test)
x.train <- read.table("UCI HAR Dataset/train/X_train.txt", col.names = feat1) # features data 
y.train <- read.table("UCI HAR Dataset/train/y_train.txt", col.names = "activity") # coded activity
train.db <- cbind(subject.train,y.train,x.train)
```
Merge train and test dataset
```
db <- rbind(train.db,test.db)
```
Replace coded activity with their labels according to 6 levels
```
db$activity <- as.factor(db$activity)
levels(db$activity) <- f.activity
```
Change as factor subject_id (30 levels)
```
db$subject.id <- as.factor(db$subject.id)
```
Select features that represent only mean and std and create dataset "dataset 1"
```
smean <- "mean...[xyz]"
sstd <- "std...[xyz]"
column <- colnames(db)
okmean <- grepl(smean,column)
okstd <- grepl(sstd,column)
dbmean <- db[okmean]
dbstd <- db[okstd]
dataset1 <- cbind(db[,1:2],dbmean,dbstd)
```
Optimize columns name according to R standard
```
newcol <- sub("...",".",(names(dataset1)),fixed=T)
names(dataset1) <- newcol
```
Export "samsung_dataset_1.csv"
```
write.csv(dataset1, file = "samsung_dataset_1.csv")
```

#### CREATING UCI-Samsung Dataset 2:

Aggregate data of dataset 1 to show the average of each variable for each activity and each subject
```
dataset2 <- aggregate(dataset1[,3:50],list(subject = dataset1$subject.id, activity = dataset1$activity),mean)
```
change columns name according to the new created variable
```
col <- names(dataset2[,3:50])
col1 <- paste("avg",col, sep = ".")
names(dataset2) <- c("subject","activity",col1)
```
Export "samsung_dataset_2.csv"
```
write.csv(dataset2,"samsung_dataset_2.csv")
```


 
