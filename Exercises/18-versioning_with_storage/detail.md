# Versioning

```sh
# see the version status of the bucket
gsutil versioning get gs://bucket-name

# set versioning on if not
gsutil versioning set on gs://bucket-name

# Now update same file (same name), multiple time.
gsutil copy file1 gs://bucket-name/file1
gsutil copy file1 gs://bucket-name/file1

# Now see all the version of the same file
gsutil ls -a gs://bucket-name/file1 #without -a versions are not printed
# gs://bucket-name/file1#1601677788379752
# gs://bucket-name/file1#1601712919019631
# gs://bucket-name/file1#1601713182182476

# access the specific version
gsutil cp  gs://bucket-name/file1#1601677788379752 file1

# details about each version object
# "stat" commands works only for objects and not for bucket
# "generation" attribute save the version of the object.
# "metageneration" it increases every time the file, basically its a number of versions are stored.
gsutil stat gs://bucket-number/file1

# delete the file
gsutil rm gs://bucket-name/file1

# now you will NOT be able to access the file
gsutil du gs://bucket-name/file1 # 404 not found
# the older versions are still there, need to access them using specific version
gsutil du gs://bucket-name/file#1601677788379752

# list all the files with versions, this will list all the files which do not have live version
gsutil ls -a gs://bucket-name/

## -------------------- METADATA -----------------------
# to set metadata -- prefix each metadata key with "x-goog-meta"
gsutil setmeta -h "x-goog-meta-name:abhishek" gs://bucket-name/obj-name

# list all the version of the file
# NOTE: that generation remain same, but meta-generation is increased.
gsutil ls -a gs://bucket-name/file1

```
