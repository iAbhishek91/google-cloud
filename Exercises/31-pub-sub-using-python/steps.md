# Python

```sh
sudo apt-get update

sudo apt-get install virtualenv

virtualenv -p python3 venv

source venv/bin/activate

pip install --upgrade google-cloud-pubsub

git clone https://github.com/googleapis/python-pubsub.git

cd python-pubsub/samples/snippets

export GLOBAL_CLOUD_PROJECT=$GOOGLE_CLOUD_PROJECT

#publisher.py is a script that demonstrates how to perform basic operations on topics with the Cloud Pub/Sub API. View the content of publisher script:
cat publisher.py

python publisher.py -h

python publisher.py $GLOBAL_CLOUD_PROJECT create MyTopic

python publisher.py $GLOBAL_CLOUD_PROJECT list

python subscriber.py $GLOBAL_CLOUD_PROJECT create MyTopic MySub

python subscriber.py $GLOBAL_CLOUD_PROJECT list-in-project

python subscriber.py -h

gcloud pubsub topics publish MyTopic --message "Hello"
gcloud pubsub topics publish MyTopic --message "Publisher's name is Abhishek Das"
gcloud pubsub topics publish MyTopic --message "Publisher likes to eat Badam"
gcloud pubsub topics publish MyTopic --message "Publisher thinks Pub/Sub is awesome"

python subscriber.py $GLOBAL_CLOUD_PROJECT receive MySub
```
