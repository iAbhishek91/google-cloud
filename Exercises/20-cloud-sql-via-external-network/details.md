# Application connecting to cloud SQL over internet

## Secure connection using proxy

Step-1: Download cloud proxy and provide permission

wget https://dl.google.com/cloudsql/cloud_sql_proxy.linux.amd64 -O cloud_sql_proxy && chmod +x cloud_sql_proxy

Step-2: get the instance name: this is a name give every cloud SQL instance once it is ready.

For example: export SQL_CONNECTION=qwiklabs-gcp-01-812abaed72a5:us-central1:wordpress-db

Step-3 start the proxy

```sh
./cloud_sql_proxy -instances=$SQL_CONNECTION=tcp:3306 &
# 2020/10/05 22:02:53 Listening on 127.0.0.1:3306 for qwiklabs-gcp-01-812abaed72a5:us-central1:wordpress-db
# 2020/10/05 22:02:53 Ready for new connections
```

> Note: The proxy will listen on 127.0.0.1:3306 (localhost) and proxy that connects securely to your Cloud SQL over a secure tunnel using the machine's external IP address.

Step-4: connection to the application

using the external IP address of the vm.
