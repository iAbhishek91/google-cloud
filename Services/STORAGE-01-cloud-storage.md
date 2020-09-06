# Storage

- known as cloud storage.
- It keeps **unstructured data**.
- Its a **binary object** storing system.
- Very similar to S3. and hence their name are globally unique.
- These unique keys are in form of URL and work well with web technologies.
- accessed using clod storage API.
- We can create bucket and store objects.

- we need to define **storage class**, default storage class are used.
- there are four different type storage classes.
  - *Multi-regional* (99.95% available)
    - High performance obj storage
    - Use cases: content storage and delivery (which are accessed very very frequently)
    - saved at least in two locations separated by 160 KM. Need to choose a geography.
    - Most costlier.
    - No data transfer cost
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
    - Use cases: access those data at most **once a year**.
    - very store low cost, highly durable.
    - data transfer per GB cost is highest.

- They are **immutable**, means they do not change in place. Instead we create new **versions**. Bucket comes with versioning settings.
- Versioning are optional, but if you turn on versioning on the bucket, it keeps history of the data. If you don't turn on versioning, new values always overrides old.
- We can see the archived state of an object or permanently delete an objects.
- Bucket have object **lifecycle management** rules, which are applied to each object on that bucket. This feature helps storing junk versions. For example: delete everything which are older than 365 days, or delete obj created before Jan 5 2020 or keep 3 month old data.

- Its a multi region service. Choose a location which are closer to users.

- High performance. millisecond access time
- High durability. meant for long term data storage.
- High availability. 99.0% - 99.95%
- fully managed.
- scalable service by google, don't require capacity management(ahead of time).

- Always **encrypts** your data on server side before saving to disk. (no extra cost for encryption)
- In transit the data is encrypted using Https.

- **security**:
  - by default the permission of IAM are inherited form projects, to bucket to objects.
  - Finer level of access are provided by defining ACL. ACL defines who have access to which object and what level of access they have. Each ACL have two piece of information: scope(who can access - users or groups) & permissions(what action can be performed for example read or write).

- **Use cases**:
  - web site content
  - distributing large data object to end users via internet direct downloadable.
  - data for archival and disaster recovery.

- different to **bring data to cloud storage**
  - gsutil command from cloud sdk.
  - drag and drp in the GCP console.
  - *storage transfer service* is for uploding huge amount of data. allows batch uploads.
  - Transfer appliance: New in beta

- **Integration with other GCP services**:
  - Biq query & cloud SQL, can import & export tables.
  - App engine: obj storage, logs, datastore backups.
  - compute engine: start up script, general obj storage.

- **Price**: Based on gigabyte of data stored per month.
