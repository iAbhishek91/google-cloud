# Cloud Shell

- Its a CLI tool(similar to Linux bash shell) to interact with GCP.
- Under the hood it uses GCP SDK to interact with the GCP APIs.
- this is a small VM which allow you to access GCP resources.

## How to open cloud shell

from GCP console, click on **activate could shell**.

## Customize cloud shell

select the "ranch" icon on top of the terminal. Then select terminal preferences.
Also we can use TMux (to multiplex and work on multiple window as well)

## Operation

- Cloud shell opens the current activated project as a directory. Projects are like users on this VMs. (we can store up to 5 gb of data)
  - execute `pwd` and the output will be `/home/name`.
- We can also change the project mentioned.
- From cloud shell we can launch the code editor. From the menu above cloud shell.

## What we can do using cloud editor

- It will open up the home folder(pwd) in a text editor like vscode.
- We can create,edit,delete a file.
