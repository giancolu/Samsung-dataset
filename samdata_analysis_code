## Check if "UCI HAR Dataset" folder exist in workin dir or download source from the web
if (!file.exists("./UCI HAR Dataset")) {
fileUrl <- "https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip" 
download.file(fileUrl, destfile = "UCI_HAR_Dataset.zip", method = "curl")
unzip("./UCI_HAR_Dataset.zip")
} else {
  cat("dir already exist")
}
## Run analysis on dataset
cat("I'm running the analysis on source dataset...")
cat("... samsung_dataset_1.csv (dataset1) and samsung_dataset_2.csv (dataset2) will be created") 
source("run_analysis.R")
