CodeBook
========

### Data source
Jorge L. Reyes-Ortiz, Davide Anguita, Alessandro Ghio, Luca Oneto.
Smartlab - Non Linear Complex Systems Laboratory
DITEN - UniversitÃ  degli Studi di Genova, Genoa I-16145, Italy.
activityrecognition '@' smartlab.ws
www.smartlab.ws 

### Source dataset information
The experiments have been carried out with a group of 30 volunteers within an age bracket of 19-48 years. Each person performed six activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) wearing a smartphone (Samsung Galaxy S II) on the waist. Using its embedded accelerometer and gyroscope, we captured 3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz. The experiments have been video-recorded to label the data manually. The obtained dataset has been randomly partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data.

For each record in the sorce dataset it is provided:
- Triaxial acceleration from the accelerometer (total acceleration) and the estimated body acceleration.
- Triaxial Angular velocity from the gyroscope.
- A 561-feature vector with time and frequency domain variables.
- Its activity label.
- An identifier of the subject who carried out the experiment.

The features selected for this database come from the accelerometer and gyroscope 3-axial raw signals tAcc-XYZ and tGyro-XYZ. These time domain signals (prefix 't' to denote time) were captured at a constant rate of 50 Hz. Then they were filtered using a median filter and a 3rd order low pass Butterworth filter with a corner frequency of 20 Hz to remove noise. Similarly, the acceleration signal was then separated into body and gravity acceleration signals (tBodyAcc-XYZ and tGravityAcc-XYZ) using another low pass Butterworth filter with a corner frequency of 0.3 Hz. Subsequently, the body linear acceleration and angular velocity were derived in time to obtain Jerk signals (tBodyAccJerk-XYZ and tBodyGyroJerk-XYZ). Also the magnitude of these three-dimensional signals were calculated using the Euclidean norm (tBodyAccMag, tGravityAccMag, tBodyAccJerkMag, tBodyGyroMag, tBodyGyroJerkMag). Finally a Fast Fourier Transform (FFT) was applied to some of these signals producing fBodyAcc-XYZ, fBodyAccJerk-XYZ, fBodyGyro-XYZ, fBodyAccJerkMag, fBodyGyroMag, fBodyGyroJerkMag. (Note the 'f' to indicate frequency domain signals). These signals were used to estimate variables of the feature vector for each pattern: '-XYZ' is used to denote 3-axial signals in the X, Y and Z directions.

### Cleaned dataset for analysis
Cleaned datasets for the analysis were created by two scripts (samdata_analysis_code.R and run_analysis.R, see **README.md** file for an explanation of the scripts). The scripts end up with two datasets (**dataset 1** and **dataset 2**).
#### Dataset 1
This dataset results from the following transformations of source data:
1. Merging the training and the test sets
2. Extracting only the measurements on the mean and standard deviation for each measurement. 
3. Using descriptive activity names to name the activities in the dataset
4. Appropriately labeling the dataset with descriptive activity names. 

This dataset is focused only on the features that represents mean and standard deviation and excludes Euclidean transformed signals and additional vectors obtained by averaging the signals in a signal window sample. 

The dataset contains 10299 records and the following 50 columns:
1. subject_id: the id of subject that performed the activity
2. activity: the type of activity that the subject performed
3. tbodyacc.mean.x
4. tbodyacc.mean.y
5. tbodyacc.mean.z
6. tgravityacc.mean.x
7. tgravityacc.mean.y
8. tgravityacc.mean.z
9. tbodyaccjerk.mean.x
10. tbodyaccjerk.mean.y
11. tbodyaccjerk.mean.z
12. tbodygyro.mean.x
13. tbodygyro.mean.y
14. tbodygyro.mean.z
15. tbodygyrojerk.mean.x
16. tbodygyrojerk.mean.y
17. tbodygyrojerk.mean.z
18. fbodyacc.mean.x
19. fbodyacc.mean.y
20. fbodyacc.mean.z
21. fbodyaccjerk.mean.x
22. fbodyaccjerk.mean.y
23. fbodyaccjerk.mean.z
24. fbodygyro.mean.x
25. fbodygyro.mean.y
26. fbodygyro.mean.z
27. tbodyacc.std.x
28. tbodyacc.std.y
29. tbodyacc.std.z
30. tgravityacc.std.x
31. tgravityacc.std.y
32. tgravityacc.std.z
33. tbodyaccjerk.std.x
34. tbodyaccjerk.std.y
35. tbodyaccjerk.std.z
36. tbodygyro.std.x
37. tbodygyro.std.y
38. tbodygyro.std.z
39. tbodygyrojerk.std.x
40. tbodygyrojerk.std.y
41. tbodygyrojerk.std.z
42. fbodyacc.std.x
43. fbodyacc.std.y
44. fbodyacc.std.z
45. fbodyaccjerk.std.x
46. fbodyaccjerk.std.y
47. fbodyaccjerk.std.z
48. fbodygyro.std.x
49. fbodygyro.std.y
50. fbodygyro.std.z

### Dataset 2
This dataset derives from "dataset 1" by averaging each variable for each activity and each subject. It contains 180 records and the same column names of the "dataset 1" with the "avg" prefix.
