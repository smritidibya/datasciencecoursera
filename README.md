# Download zip files from given URL
# Unzip all the datafiles
# Read features data for labels
# Read train, test data with acitvity label, subject id, activity data for
# Both test and train data

# From feature data, create the column names

# A
# Add activity description to subject_train data and merge with subject id
# Add activity description to subject_test data and merge with subject id
# Combine test and train data with subject id, activity description

# B
# Combine test and train data

# Combine data created in A and B. This will be interim dataset with 10299 row and 563 variable

# Delete duplicate column from interim dataset

# Limit final dataset with subject id, activity description and mean and std for all different variable
# Dimension for final dataset prior to sumamrizing is 10299 rows and 88 columns
# clean-up variable names by removing (), _ as well converting all the letters to lower case

# Create tidy data using melt and dcast and get mean by each subject, activity and measurement.

