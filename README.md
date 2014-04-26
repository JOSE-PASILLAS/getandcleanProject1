Introduction

This project was designed for the Coursera course Getting and Cleaning data, Johns Hopkins University.
The objective is to obtain the means.

Purpose 

The purpose of this project is to demonstrate your ability to collect, work with, and clean a data set. 
The goal is to prepare tidy data that can be used for later analysis. 

Content
1) A tidy data set.
2) A script for performing the analysis.
3) A code book that describes the variables, the data, and any transformations or work that you performed to clean up the data called CodeBook.md. 
4) A README.md in the repo with scripts. This repo explains how all of the scripts work and how they are connected.  

Script
--------------------------------------------------------------------------------------
## Load the labels
getActivityLabels<-function(){
    labelFilename <- file.path('UCI HAR Dataset', 'activity_labels.txt')
    labels <- read.table(labelFilename)
}
## Load features names
getFeatures<-function(d,f){
    featuresFilename <- file.path(d,f)
    features <- read.table(featuresFilename)
}
getIndexFeatures<-function(f){
    expresion<-"([Mm][Ee][Aa][Nn])|([Ss][Tt][Dd])"
    nfeatures<-sapply(f,function(y) grep(expresion,y))
}
# cleand and tidy features
cleanFeatures<-function(f,n){
    subfeatures<-f[n[[2]],2]
    subfetures<-tolower(subfeatures)
    subfetures<-gsub("[[:punct:]]","",subfeatures)
}

getData<-function(d,f,n){
    testpath<-file.path(d,f)
    read.table(testpath)[,n[[2]]]
}
getColumn<-function(d,f){
    path<-file.path(d, f)
    observations<-read.table(path)
}

# Get features name
features<-getFeatures("UCI HAR Dataset","features.txt")
nfeatures<-getIndexFeatures(features)
# Fix features name
subfeatures<-cleanFeatures(features,nfeatures)

### Loads and clean test data
directory<-"UCI HAR Dataset/test"
data<-getData(directory,"X_test.txt",nfeatures)
## Set the names of the columns
colnames(data)<-subfeatures
##Set test labels
data["activity"]<-getColumn(directory,"y_test.txt")
data["subject"]<-getColumn(directory,"subject_test.txt")

### Loads and clean train data
directory<-"UCI HAR Dataset/train"
data2<-getData(directory,"X_train.txt",nfeatures)
## Set the names of the columns
colnames(data2)<-subfeatures
##Set test labels
data2["subject"]<-getColumn(directory,"subject_train.txt")
data2["activity"]<-getColumn(directory,"y_train.txt")


##Merge train and test sets
combdata<-rbind(data,data2)

## Aggregate data by activity and subject
aggdata <-aggregate(combdata[,1:86], by=list(subject=combdata$subject,activity=combdata$activity), 
                    FUN=mean, na.rm=TRUE)

##Descriptive activity names
activities<-getActivityLabels()
aggdata$activity<-as.factor(aggdata$activity)
aggdata$activity <- factor(aggdata$activity, labels=as.vector(activities[[2]]))

##Write the table
write.table(aggdata,file="data.txt",row.names = FALSE)

--------------------------------------------------------------------------------------
