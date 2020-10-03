# Cloud Storage

- It keeps **unstructured data**.
- Its a **binary object/BLOB** storing system.
- Very similar to S3. and like S3 their name are globally unique.
- These unique keys are in form of URL and work well with web technologies.
- accessed using cloud storage API.
- We can create bucket and store objects.

- we need to define **storage class**, default storage class are used.
- there are five different type storage classes.
  - *Multi-regional* (99.95% available)
    - High performance obj storage
    - Use cases: content storage and delivery (which are accessed very very frequently)
    - saved at least in two locations separated by 160 KM. Need to choose a geography.
    - Most costlier.
    - No data transfer cost
    - As of date Possible only for US, Europe and Asia pac
  - *Regional* (99.9% available)
    - High performance obj storage
    - Use cases: In-region analytics & transcoding. (closer to processing units like kubernetes engine, analytics and data processing center)
    - Specific to single GCP region.
    - Cheaper than multi region
    - less redundancy
    - No data transfer cost
  - *Nearline* (99% available)
    - Used for backup and archival storage. (in frequently access data)
    - Use cases: Long tail content, (updated or read mostly **once a month or less**), Continuously add data, but access later for analysis.
    - Low cost, highly durable solution.
    - data transfer per GB cost is higher.
  - *Coldline* (99% available)
    - Used for backup and archival storage.
    - Use cases: access those data at most **once a year**. Currently they suggest **once in a quarter**.
    - very store low cost, highly durable.
    - data transfer per GB cost is highest.
  - *Archive* ()
    - Used to store for long term storage.
    - not used until a year **once in a year**
    - very store low cost, highly durable.
    - data transfer per GB cost is highest.

- **Versioning**:
  - They are **immutable**, means they do not change in place. Instead we create new **versions**. Bucket comes with versioning settings.
  - Versioning are optional, but if you turn on versioning on the bucket, it keeps history of the data.
  - With versioning, every object has a generation number.
  - we can list the versions of objects, restore an objects to an older state, or delete a version. *when versioning is ON, rm operation, deletes only the current live version of the object*
  - Versioning can be changed at any time. When versioning is stopped, bucket holds all the existing objects, but stops accumulating version of objects.
  - Versioning can be applied on the bucket and not on objects.
  - Since versioning keep multiple copies of objects they are charged.
  - Version of the file are independent of the original file. *ie, the old version exists without any link to original file*
  - How version info are saved for the object? using special fields **generations** *version number* and **metagenerations** *number of time the versioning is triggered*. Check the value using `gsutil stat gs://bucket-name/file1`
  - versioning work best in complement with lifecycle feature.
  - **Pre-Condition** are criteria set which allow certain operation on the object if generation or meta-generation value works.
    - Pre-condition comes with performance(double latency in introduced) and billing cost based on mutating the data. $0.004 per 10000 operation
  - adding metadata to a object increases the version. `gsutil setmeta -h "METADATA_KEY:METADATA_VALUE" gs://bucket-name/file1`

- Bucket have object **lifecycle management** configuration (set of rules), which are applied to all the object on that bucket. This feature helps storing junk versions.
  - rules can be defined: delete everything which are older than 365 days, OR delete obj created before Jan 5 2020 OR keep 3 month old data OR downgrade storage class on object older than a year.
  - Changes on lifecycle management can take 24 hours to take effect.
  - Inspection(validation of lifecycle rules) occurs in asynchronous batches. Hence rules will not applied immediately.

- **Change notification**
  - used to notify an application, when an object is created or updated or deleted from the bucket through a watch request.
  - Completing a watch request, creates a new notification channel.
  - there can be different type of channels: but as of now its only webhook.
  - However its recommended to use cloud pub/sub, its cheaper, and easier to setup and faster.

- We can see the archived state of an object or permanently delete an objects.
- Its a multi region service. Choose a location which are closer to users.
- High performance. millisecond access time
- High durability. meant for long term data storage.
- High availability. 99.0% - 99.95%
- High consistency - after an upload immediately objects are available for download, there are not delays. Its true for all the operations and metadata as well.
  - Strongly consistent operations:
    - read after write
    - read after metadata update
    - read after delete
    - bucket listing
    - object listing
    - granting access to resources
- fully managed.
- scalable service by google, don't require capacity management(ahead of time).
- Buckets are cant be nested.
- no minimum size, unlimited storage. (limit is defined by regions)
- Buckets stores objects. *Note : even folders are objects, which points to multiple object, giving a feel of hierarchical storage*
- Can't be indexed, unlike file system.
- access using single API.
- **Custom encryption keys**, as available for persistent disk of VM instances.
- **Directory sync**: Sync between a directory of a VM with that of bucket is possible. *Note: This way we can use cloud storage as persistent disk for VM*.

- Always **encrypts** your data on server side before saving to disk. (no extra cost for encryption)
- In transit the data is encrypted using Https.

- **migration**:
  - migration of bucket from regional to multi-regional is not possible and vice-versa.
  - migration of bucket from regional to nearline or coldline is possible. Same for multi-regional.

- **security**:
  - by default the permission of **IAM** are inherited form projects, to bucket to objects. *IAM provides access to all storage in general, but ACL defines who can access a bucket specifically, with what level of access(owner, viwer).*
  - Finer level of access are provided by defining **ACL**. ACL defines who have access to which object and what level of access they have. Each ACL have two piece of information: scope(who can access - users or groups) & permissions(what action can be performed for example read or write).
    - object level permission
    - max ACL rules are 100/bucket.
    - permissions: allUsers (any user in the internet) | anyAuthenticatedUser(all google users) | specific person
    - we use ACL when we need customize access to each object in the bucket. *For single set of permissions switch to uniform access*.
    - By default when an object is uploaded, it gets the ACLs from the bucket. However we can modify them.
    - ACL have two parts: scope(to whom), and permission (what actions).
      -Permissions: OWNER, WRITER, READER. if we assign WRITER, READER is automatically assigned. This is commonly known as concentric permissions.
      - Scope: user - google ac | google group | svc account | allAuthenticatedUsers | allUsers |,  domain - cloud identity | g suite| , project
  - **Signed URL** - provide access to objects for limited period of time to a object in a bucket.
    - limited access signed using a private key (of a service account)
    - time limit is provided.
    - anyone can access the URL for limited period of time with out authentication.
  - **Signed policy documents** - defines what type of documents can be upload.

- **Use cases**:
  - web site content
  - distributing large data object to end users via internet direct downloadable.
  - data for archival and disaster recovery.

- **access to cloud storage**
  - gsutil command from cloud sdk.
  - drag and drp in the GCP console.
  - Below mechanism supports Huge data upload/imports:
    - *storage transfer service* is for importing huge amount of online data. allows batch uploads. Need to provide a storage source: this can be AWS S3, or any other web source or another GCP bucket)
    - *Offline media import*: 3rd party provider uploads the data from physical media(like usb, tapes, hard drives).
    - *Transfer appliance*: is hardware devices that can used to upload peta bytes of data directly in cloud storage. Steps are rack, capture and ship your data to GCP.

- **Integration with other GCP services**:
  - Biq query & cloud SQL, can import & export tables.
  - App engine: obj storage, logs, datastore backups.
  - compute engine: start up script, general obj storage.

- **Price**: Based on gigabyte of data stored per month and storage class.
