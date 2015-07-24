fileUrl <- URL name
temp <- name of location to be downloaded
list.files <- list of all the files in zip files

library(plyr)
library(dplyr)
library(reshape2)

features <- column names for measurements change

activity <- actvity name and description(act_id, activity)

#test data
subject_test <- subject_id
test_data <- test data for measurements
test_label <- activity data for subject(act_id)

test_m <- attaching desc to activity
test_m <- this contains subject id, activity, activity description,

#train data
subject_train <- subject_id
train_data <- test data for measurements

train_label <- activity data for subject(act_id)

train_m <- attaching desc to activity
train_m <- this contains subject id, activity, activity description,

act_data <- combined test and train data with subject id and activity

data <- combined test and train data with measurements

new_name <- column names
data <- data with column names of measurements

data_all <- data with subject id, actvity description and measurements with unique columns

mean <- keeping all the means
std <- keeping all the std
active <- keeping subject id and activity description

meanstd <- combine data with subject id, activity description and measurements

melted and summarize data by subject, activity and mean of each measurements
