# Use Marketplace

## Scenario

Deploy a Jenkins instance from Cloud market place.

## Steps

- Navigate to cloud marketplace
- Find the Jenkins deployment name: Jenkins certified by Bitnami
- Click on deploy

- Navigate to deployment manager.
- Collect the initial username and password

- navigate to compute engine - launch the external IP to access Jenkins.
- validate that storage is also used to save the state of the Jenkins.

- to admin Jenkins, ssh in the compute engine.
- sudo /opt/bitnami/ctlscript.sh stop | restart - to restart or stop jenkins (this script is provided by bitnami)
