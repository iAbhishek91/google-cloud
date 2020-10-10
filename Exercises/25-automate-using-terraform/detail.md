# terraform and GCP automation

**Step-1**: in could shell editor create a folder and do everything there
**Step-2**: create a file provider.tf

```tf
provider "google" {}
```

**Step-3**: Create a network.tf

```tf
# Create the mynetwork network
resource "google_compute_network" "mynetwork" {
name                    = "mynetwork"
auto_create_subnetworks = true
}

# Add a firewall rule to allow HTTP, SSH, RDP, and ICMP traffic on mynetwork
resource "google_compute_firewall" "mynetwork-allow-http-ssh-rdp-icmp" {
name = "mynetwork-allow-http-ssh-rdp-icmp"
network = google_compute_network.mynetwork.self_link
allow {
    protocol = "tcp"
    ports    = ["22", "80", "3389"]
    }
allow {
    protocol = "icmp"
    }
}
```

**Step-4**: Create a folder under the main folder called : "instance"
**Step-5**: Create a file main.tf

```tf
variable "instance_name" {}
variable "instance_zone" {}
variable "instance_type" {
  default = "n1-standard-1"
  }
variable "instance_network" {}

resource "google_compute_instance" "vm_instance" {
  name         = "${var.instance_name}"
  zone         = "${var.instance_zone}"
  machine_type = "${var.instance_type}"
  boot_disk {
    initialize_params {
      image = "debian-cloud/debian-9"
      }
  }
  network_interface {
    network = "${var.instance_network}"
    access_config {
      # Allocate a one-to-one NAT IP to the instance
    }
  }
}
```

**Step-6**: update mynetwork.tf

```tf
# Create the mynetwork network
resource "google_compute_network" "mynetwork" {
name                    = "mynetwork"
auto_create_subnetworks = true
}

# Add a firewall rule to allow HTTP, SSH, RDP, and ICMP traffic on mynetwork
resource "google_compute_firewall" "mynetwork-allow-http-ssh-rdp-icmp" {
name = "mynetwork-allow-http-ssh-rdp-icmp"
network = google_compute_network.mynetwork.self_link
allow {
    protocol = "tcp"
    ports    = ["22", "80", "3389"]
    }
allow {
    protocol = "icmp"
    }
}

# Create the mynet-us-vm instance
module "mynet-us-vm" {
  source           = "./instance"
  instance_name    = "mynet-us-vm"
  instance_zone    = "us-central1-a"
  instance_network = google_compute_network.mynetwork.self_link
}

# Create the mynet-eu-vm" instance
module "mynet-eu-vm" {
  source           = "./instance"
  instance_name    = "mynet-eu-vm"
  instance_zone    = "europe-west1-d"
  instance_network = google_compute_network.mynetwork.self_link
}
```

**Step-7**: format and deploy

```sh
terraform fmt
terraform init
terraform plan
terraform apply # type yes
```
