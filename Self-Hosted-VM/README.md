# Setting Up a self-hosted Virtual Machine for Azure DevOps Pipeline Agent using Vagrant.
This vagrantfile serves as a self-host VM for running various tools and services needed in the project's Azure DevOps pipeline.

## **The Vagrantfile is configured to:**
1. Use the Ubuntu 23.04 base box.
2. Allocate 4 GB of RAM to the VM.
3. Forward port 9000 to allow access to SonarQube from the host machine.
4. Provision the VM with necessary software including Docker, Java, Maven, Trivy, and SonarQube. 

## Prerequisites

Before you begin, ensure you have the following installed on your host machine:

- [Vagrant](https://www.vagrantup.com/)
- [VirtualBox](https://www.virtualbox.org/)

## Setup Instructions

### Step 1: **Clone the Repository**

   Clone this repository to your local machine:

   ```bash
   git clone "https://github.com/Godfrey22152/Train-Ticket-Reservation-System-Application.git"
   cd Train-Ticket-Reservation-System-Application/Self-Hosted-VM
   ```

### Step 2: **Start the Vagrant VM**

   Start the Vagrant VM by running:

   ```bash
   vagrant up

   ```
### Step 3: **Accessing SonarQube**

   Once the VM is up and running, you can access SonarQube from your browser at:

   ```
   http://localhost:9000
   ```

   Use the default credentials:
   - Username: admin
   - Password: admin

### Step 4: SSH into the VM

If you need to access the VM via SSH, use the following command:

```sh
vagrant ssh
```

### Step 5: **Stop or Destroy the Vagrant VM**

   You can stop the Vagrant VM with:

   ```bash
   vagrant halt
   vagrant destory -f
   ```

## Provisioning Details

The provisioning script performs the following steps:

1. Updates and upgrades the system packages.
2. Installs Docker and starts the Docker service.
3. Installs Java (OpenJDK 17).
4. Installs Maven.
5. Installs Trivy, a vulnerability scanner for containers.
6. Runs SonarQube using a Docker container.

## Customization

### Adjusting Memory Allocation

If needed, adjust the memory allocation for the VM in the Vagrantfile:

```ruby
config.vm.provider "virtualbox" do |vb|
  vb.memory = "4096" # Adjust memory (in MB) as needed
end
```

### Installing SonarQube

I installed SonarQube using a Docker image that allow access to multi-branch scan `mc1arke/sonarqube-with-community-branch-plugin`. If you prefer to install SonarQube using the official documentation guidelines or a different Docker image, modify the provisioning script accordingly.

### Adding Additional Tools

To add more tools or customize the VM further, edit the provisioning script in the Vagrantfile and re-provision the VM with:

```bash
vagrant reload --provision
```

## Troubleshooting

- **Network Issues**: Ensure that port `9000` is accessible on your host machine.
- **Permissions**: If you encounter permission issues with Docker, ensure your user is added to the Docker group within the VM or adjust permissions as needed in the provisioning script.
- **Permission Denied (Public Key) Error**: Ensure your SSH keys are properly configured if you encounter permission issues when pushing to a remote Git repository.
- **Port Forwarding Issues**: Ensure port 9000 is not being used by another application on your host machine.

For additional help, refer to the [Vagrant documentation](https://www.vagrantup.com/docs).

## License

This project is licensed under the [MIT License](LICENSE).
