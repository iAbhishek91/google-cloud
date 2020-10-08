# Deploy app | error reporting | log

> app.yaml file instruct the runtime, and how to deploy the app, and the location of the other files.

```sh
# Clone a git repo which you want to deploy
# This repo already have app.yaml and .gcloudignore file defined theses are important for deploying services to app engine.
# App engine uses the start script from package.json to start the app, if entrypoint is not mentioned in app.yaml
# Port should be 8080
git clone https://github.com/iAbhishek91/devops-project-1.git
cd devops-project-1

# install and build the application
npm i yarn -g # optional if yarn is not already installed
yarn # download all the dependencies
yarn build # webpack build with help of babel
yarn start # start the webserver, this for test.

# deploy the app in app engine
# only "gcloud app deploy" also works as app.yaml is the default file.
# run this command from the folder root folder of the project
gcloud app deploy app.yaml --quite
# Enter the region code is asked for, nearest to you.

gcloud app browse
```

## Introduce an error and validate in error reporting and debugging

```sh
# redeploy once again
gcloud app deploy app.yaml --quite
```

Now automatically we can see the errors and stack trace  and perform necessary action.

## Delete a deployment

To delete the previous deployment. BE VERY CAUTIOUS as nothing is irreversible.

- Disable the application from settings.
- Delete all the version that do not have traffic allocation.
- Delete the storage bucket assigned for the app engine.
