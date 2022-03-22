# IBM Quickstart Reference Architecture on Azure

## Software Dependencies

The module depends upon the following software components being installed on the build machine.

### Command-Line Tools

This module depends upon the following command line tools being installed onto the build machine. The module assumes the build machine is a Mac or Linux operating system.

- Ansible version 2.12.2 or higher (follow the guide [here](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html))
- Azure CLI version 2.34.1 or higher (follow the guide [here](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest))

### Module Dependencies

For the Ansible Azure galaxy collection:
- azure.azcollection version 1.11.0 or higher
- msrest
- msrestazure (# pip3 install msrestazure)
- azure-mgmt-compute
- azure-mgmt-storage
- azure-mgmt-resource
- azure-mgmt-network
- azure-keyvault-secrets
- azure-storage-blob
- azure.mgmt.network.version
Note that if using Ansible through homebrew on MacOS, this above packages need to be installed using the Ansible python package (/usr/local/Cellar/ansible/5.3.0/libexec/bin/pip3 install msrestazure)

## Limitations

- This automation has been built and tested on MacOS. It should also work on Linux based build machines, but may not work on Windows based build machines.

## Bill of Materials

This architecture consists of the following bill of materials:

| Item | Description |
|------------------ | ------------------------------------------------------------------------------- |
| Virtual Network | Provides a private network environment within the Azure cloud for hosting the other services.  |
| Worker Subnets | Provides network interface for the OpenShift worker nodes.  |

## Example Usage

1. Install Ansible 
1. Install Azure CLI
1. Login to Azure cli
1. Clone repo
1. Run Ansible playbook