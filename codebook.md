fileUrl<-"https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip"
temp <- tempfile()
download.file(fileUrl,temp)
list.files <- unzip(temp,list=TRUE)

library(plyr)
library(Hmisc)

#column names
features <- read.table(unz(temp, list.files$Name[2]))
a<-as.data.frame(t(features))
colnames(a) <- as.character(unlist(a[2,]))
name <- a[c(-1,-2),]

#activity and desc
activity <- read.table(unz(temp, list.files$Name[1]))
activity <- rename(activity, c("V1"="act_id", "V2"="activity"))

#test data
subject_test <- read.table(unz(temp, list.files$Name[16]))

test_data <- read.table(unz(temp, list.files$Name[17]))
#2947

test_label <- read.table(unz(temp, list.files$Name[18]))
test_label <- rename(test_label, c("V1"="act_id"))

#attaching desc to activity
test_m <- merge(test_label,activity, by.x="act_id", by.y="act_id", all=TRUE)
test_m <- cbind(subject_test,test_m)
test_m <- rename(test_m, c("V1"="subject"))


#Training data
subject_train <- read.table(unz(temp, list.files$Name[30]))
train_data <- read.table(unz(temp, list.files$Name[31]))
#7352

train_label <- read.table(unz(temp, list.files$Name[32]))
train_label <- rename(train_label, c("V1"="act_id"))

#attaching desc to activity
train_m <- merge(train_label,activity, by.x="act_id", by.y="act_id", all=TRUE)

train_m <- cbind(subject_train,train_m)
train_m <- rename(train_m, c("V1"="subject"))

act_data <- rbind(test_m,train_m)

##Merging training and test data
data <- rbind(test_data,train_data)

new_name <- colnames(name)

colnames(data) <- new_name
names(data)

#data with activity

data_all <- cbind(act_data,data)

data_all <- subset(data_all, select=-c(act_id))


data_all <- data_all[ , !duplicated(colnames(data_all))] 

names(data_all)=tolower(names(data_all))

mean <- data_all[,grep("mean",names(data_all), value=TRUE)]
std <- data_all[,grep("std",names(data_all), value=TRUE)]

active <- subset(data_all, select=c(subject,activity))

meanstd <- cbind(active,mean,std)

names(meanstd) = gsub("\\(|\\)", "",names(meanstd))
names(meanstd) = gsub("-", "",names(meanstd))

names(meanstd)

library(dplyr)
grp <- group_by(meanstd, subject, activity)
a<-summarise(grp,mean=mean(tbodyaccmeanx))

d <- melt(data=tt, id = c("subject","activity"),measure.vars = colnames(tt))



library(reshape2)
tt <- subset(meanstd, subject ==10)#, select=c(subject, activity,tbodyaccmeanx))
tt_act <- group_by(tt, activity)
summarize(tt_act, mean=mean(names(tt_act)))
Enter file contents here
