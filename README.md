This data set results show when 30 participants or subjects wore human activity recognition sensors (gyroscope and accelerometer)<br>
Activity was walking, walking upstairs, walking downstairs, sitting, standing and laying.<br>
Data was collected and analyzed using time-series graphs<br>
Data sets results show mean and standard deviation of each frequency, gravitational and body movements<br>
calculated from accelerometer and gyrosensor per identified subject (participant).<br>

1. Clean <br>
      rm(list=ls())<br>
2. Read train data sets and merge <br>
      features     = read.table('./features.txt',header=FALSE);<br>
      activityType = read.table('./activity_labels.txt',header=FALSE); <br>
      subjectTrain = read.table('./train/subject_train.txt',header=FALSE);<br>
      xTrain       = read.table('./train/x_train.txt',header=FALSE); <br>
      yTrain       = read.table('./train/y_train.txt',header=FALSE); <br>

3. Modify column names<br>
      colnames(activityType)  = c('activityId','activityType');<br>
      colnames(subjectTrain)  = "subjectId";<br>
      colnames(xTrain)        = features[,2]; <br>
      colnames(yTrain)        = "activityId";<br>

4.  Merge yTrain, subjectTrain, and xTrain<br>
      trainingData = cbind(yTrain,subjectTrain,xTrain);
5. Read test data sets<br>
      subjectTest = read.table('./test/subject_test.txt',header=FALSE); <br>
      xTest       = read.table('./test/x_test.txt',header=FALSE); <br>
      yTest       = read.table('./test/y_test.txt',header=FALSE); <br>

6. Modify column names for test datasets<br>
      colnames(subjectTest) <-"subjectId";<br>
      colnames(xTest)       = features[,2]; <br>
      colnames(yTest)       = "activityId";<br>
7. Merge xTest, yTest and subjectTest <br>
      testData = cbind(yTest,subjectTest,xTest);<br>

8.  Combine training and test data to create a final data set<br>
      finalData = rbind(trainingData,testData);<br>

9. Create a vector for the column names, which will be used to select the desired mean() & stddev() columns<br>
      colNames  = colnames(finalData); <br>

10. Extract only the measurements on the mean and standard deviation for each measurement by creating a logical vector that contains TRUE values for the id, mean and standard deviations only.<br>
    logicalVector = (grepl("activity..",colNames) | grepl("subject..",colNames) | grepl("-mean..",colNames) &<br> <p>!grepl("-meanFreq..",colNames) & !grepl("mean..-",colNames) | grepl("-std..",colNames) & !grepl("-std()..-",colNames));<br>

11. Subset table based on the logical vector to keep only desired columns<br>
    finalData = finalData[logicalVector==TRUE];<br>

12. Use descriptive activity names to name the activities in the data set by merging dataset to include descriptive activity names.<br>
      finalData = merge(finalData,activityType,by='activityId',all.x=TRUE);<br>

13. Update the colNames vector to include the new column names after merge.  Appropriately label the data set with descriptive<br> activity names. <br>
      colNames  = colnames(finalData);<br> 
      
14. Cleaning up the variable names for tidy data. <br>
      colNames[i] = gsub("\\()","",colNames[i])<br>
      colNames[i] = gsub("-std$","StdDev",colNames[i])<br>
      colNames[i] = gsub("-mean","Mean",colNames[i])<br>
      colNames[i] = gsub("^(t)","time",colNames[i])<br>
      colNames[i] = gsub("^(f)","freq",colNames[i])<br>
      colNames[i] = gsub("([Gg]ravity)","Gravity",colNames[i])<br>
      colNames[i] = gsub("([Bb]ody[Bb]ody|[Bb]ody)","Body",colNames[i])<br>
      colNames[i] = gsub("[Gg]yro","Gyro",colNames[i])<br>
      colNames[i] = gsub("AccMag","AccMagnitude",colNames[i])<br>
      colNames[i] = gsub("([Bb]odyaccjerkmag)","BodyAccjJerkmagnitude",colNames[i])<br>
      colNames[i] = gsub("JerkMag","JerkMagnitude",colNames[i])<br>
      colNames[i] = gsub("GyroMag","GyroMagnitude",colNames[i])<br>
      colnames(finalData) = colNames;<br>

15. Create a second, independent tidy data set with the average of each variable for each activity and each subject. <br>
      finalDataNoActivityType  = finalData[,names(finalData) != 'activityType'];<br>
16. Summarizing the table to include just the mean of each variable for each activity and each subject<br>
      tidyData    = aggregate.data.frame(finalDataNoActivityType[,names(finalDataNoActivityType) != <p>c('activityId','subjectId')],by=list(activityId=finalDataNoActivityType$activityId,subjectId =</p> <p>finalDataNoActivityType$subjectId),mean);</p>

17.  Merging data to include descriptive activity names<br>
      tidyData    = merge(tidyData,activityType,by='activityId',all.x=TRUE);<br>

18. Export the tidyData set <br>
      write.table(tidyData, './tidyData.txt',row.names= FALSE, sep='\t') <br>
