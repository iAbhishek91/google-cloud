# Application connecting to cloud SQL using private IP

Both the application and the SQL is located in the same project and region.


## Create a MySQL database instance

- Name: mysql-db
- Password: ******
- Location: Region and zones
- Database Version: My SQL5.7

Once the DB instance is created **enable private connection** >> from connection >> select the private connection radio button >> manage service network connection >> click Enable API button >> allocate and connect.

Also we can **configure the VM and storage**, navigate to "machine & storage options" and adjust as required.

- Machine Type: db-n1-standard-1 *determines the network throughput*
- Storage Type: SSD
- Storage Class: 10GB *determines disk throughput*
- vCPU and Memory: 1 and 3.75

Create the database:

- name: wordpress
- collation: utf8_general_ci(default)
- wordpress: utf8_general_ci(utf8)
- Type: User
