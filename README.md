## This data set results show when 30 participants or subjects wore human activity recognition sensors (gyroscope and accelerometer)
## Activity was walking, walking upstairs, walking downstairs, sitting, standing and laying.
## Data was collected and analyzed using time-series graphs.
## Data sets results show mean and standard deviation of each frequency, gravitational and body movements
## calculated from accelerometer and gyrosensor per identified subject (participant).

## Clean

## 1. Read data sets and merge.

## 2.  Read train datasets

## 3. Modify column names

## 4.  Merge yTrain, subjectTrain, and xTrain

## 5. Read test data sets

## 6. Modify column names for test datasets

## 7. Merge xTest, yTest and subjectTest 

## 8.  Combine training and test data to create a final data set

## 9. Create a vector for the column names, which will be used to select the desired mean() & stddev() columns

##10. Extract only the measurements on the mean and standard deviation for each measurement. 

##11. Create a logical vector that contains TRUE values for the id, mean and standard deviations only.

##12. Subset table based on the logical vector to keep only desired columns

##13. Use descriptive activity names to name the activities in the data set

##14. Merge dataset to include descriptive activitynames.

##15. Update the colNames vector to include the new column names after merge.  Appropriately label the data set with descriptive activity names. 

##16. Cleaning up the variable names for tidy data. 

##17. Create a second, independent tidy data set with the average of each variable for each activity and each subject. 

##18. Summarizing the table to include just the mean of each variable for each activity and each subject

##19.  Merging data to include descriptive activity names

##20. Export the tidyData set 

