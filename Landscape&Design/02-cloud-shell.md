# Cloud Shell

- Its a CLI tool(similar to Linux bash shell) to interact with GCP.
- Its comes with GCP SDK to interact with the GCP APIs.
- It also has inbuilt access to kubectl.
- Small VM(compute engine) which allow you to access GCP resources.
- It is always accessed through browser.
- 5GB of persistent disk
- Language support: Java, Go, Python Node.JS, PHP, & Ruby
- Built in authorization for access to res and instances.
- After one hour of inactivity cloud shell instance is recycled. only /home directory persist.

## How to open cloud shell

from GCP console, click on **activate could shell**.

## Customize cloud shell

select the "ranch" icon on top of the terminal. Then select terminal preferences.
Also we can use TMux (to multiplex and work on multiple window as well)

## Operation

- Cloud shell opens the current activated project as a directory. Projects are like users on this VMs. (we can **store up to 5 gb** of data)
  - execute `pwd` and the output will be `/home/name`.
- We can also change the project mentioned.
- From cloud shell we can launch the code editor. From the menu above cloud shell.
- In build **Web preview** functionality.

## What we can do using cloud editor

- It will open up the home folder(pwd) in a text editor like vscode.
- We can create,edit,delete a file.
