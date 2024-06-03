# Folder description

This folder contains files used for performing tasks prior to the formal analysis or and mre object containing data related to a metagenomic analysis. The folder contains the subsequent .Rmd files:

- 000_s3_bucket_initialization.Rmd

- 001_metadata_check.Rmd

- 002_datatransfer.Rmd

- 003_metadata_vars_selection.Rmd

# .Rmd files description

The function of each of these files is the following one:

**000_s3_bucket_initialization.Rmd**: It is used to create a new bucket in AWS s3.

The code of this file uses a function named `init_bucket` from a package named `MISTRALDM` to create a bucket in S3 services from AWS. To execute this function, a bucket name and a folder structure need to be defined.

**001_metadata_check.Rmd**: It is used to perform a check of both clinical and technical metadata, clean them and create a single file containing a combination of both types of metadata to later save it to s3.

The code performs the following tasks:

- First, two dataframes are created importing a .cvs file containing experiment metadata from AWS s3 using `aws.s3` package (those files need to have been already loaded to the bucket). These two dataframes are the following ones:
  - A dataframe with clinical metadata (meta) and
  - A dataframe with technical metadata (lims)
  
- Then, both dataframes are cleaned in terms of elimination of empty columns, changing of column names, creation of new columns, fixing of writing errors.

- Both dataframes are merged in a new dataframe and some variables are reorded.

- Finally, the newly created dataframe is stored in the same s3 folder using `aws.s3` package.
  
**002_datatransfer.Rmd**: It is used to perform a data transfer of the raw data from a datatransfer bucket to the project bucket and also to a backup bucket.

**003_metadata_vars_selection.Rmd**: It is used to define categorical, numerical and longitudinal samples, store them to .txt files and save them to s3.

The code performs the following tasks:

- First, the variables are defined and the metadata file is loaded from s3 as a dataframe.

- Then, the numerical, categorical and longitudinal variables are defined, following a certain format, and three dataframes corresponding to each variable type are created.

- Finally, both the metadata file and the variable dataframes are saved to s3 into a different folder. This way, the metadata .csv file is saved both in the metadata folder from the current project and to the metagenome/WMGS/Metadata folder from the same project.

