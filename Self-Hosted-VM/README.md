# Setting Up a self-hosted Virtual Machine for Azure DevOps Pipeline Agent using Vagrant.

This Vagrant setup provides an Ubuntu 18.04 LTS virtual machine configured with Docker, Java, Maven, Trivy, and SonarQube. It serves as a self-host VM for running various tools and services needed in the project's Azure DevOps pipeline.

## Prerequisites

Before you begin, ensure you have the following installed on your host machine:

- [Vagrant](https://www.vagrantup.com/)
- [VirtualBox](https://www.virtualbox.org/)

## Getting Started

1. **Clone the Repository**

   Clone this repository to your local machine:

   ```bash
   git clone "https://github.com/Godfrey22152/Train-Ticket-Reservation-System-Application.git"
   cd Self-Hosted-VM
   ```

2. **Start the Vagrant VM**

   Start the Vagrant VM by running:

   ```bash
   vagrant up
   ```

   This command provisions the VM and installs Docker, Java, Maven, Trivy, and SonarQube.

3. **Accessing SonarQube**

   Once the VM is up and running, you can access SonarQube from your browser at:

   ```
   http://localhost:9000
   ```

   Use the default credentials:
   - Username: admin
   - Password: admin

4. **Stopping the Vagrant VM**

   You can stop the Vagrant VM with:

   ```bash
   vagrant halt
   vagrant destory -f
   ```

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

## License

This project is licensed under the [MIT License](LICENSE).
