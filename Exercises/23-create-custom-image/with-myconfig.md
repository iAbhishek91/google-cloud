# create a custom template

1. Create VM of any type | dont delete the boot disk on restart

```sh
sudo apt -y update
sudo apt-get install -y git npm
sudo mkdir workspace
sudo cd workspace
sudo git clone https://github.com/iAbhishek91/display-hostname.git
sudo cd display-hostname
sudo yarn
sudo chmod +x start.sh
sudo cp display-hostname.service /etc/systemd/system/
sudo systemctl daemon-restart
sudo systemctl enable display-hostname
sudo systemctl start display-hostname
```

2; Reset the VM and check the service is still running.

3; delete the VM.

4; Create a custom Image

Navigate to Compute Engine >> Images >> Create images

- name: Display-hostname-image
- source: Disk
- Select the disk: which was attached as boot-disk to the previous VM.
- Location: Regional (europe-west2)(it can be multi regional as well)
- Click create

Create  a VM with this image and try.
