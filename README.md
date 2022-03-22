# IBM Quickstart Reference Architecture on Azure

## Software Dependencies

The module depends upon the following software components being installed on the build machine.

### Command-Line Tools

This module depends upon the following command line tools being installed onto the build machine. The module assumes the build machine is a Mac or Linux operating system.

- Ansible version 2.12.2 or higher (follow the guide [here](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html))
- Azure CLI version 2.34.1 or higher (follow the guide [here](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest))

## Limitations

- This automation has been built and tested on MacOS. It should also work on Linux based build machines, but may not work on Windows based build machines.
- Change the shell parameter in the defaults to use a different shell and path for the command line shell or the azure az binary.

## Bill of Materials

This architecture consists of the following bill of materials:

| Item | Description |
|------------------ | ------------------------------------------------------------------------------- |
| Resource Group | Provides a means of grouping like resources in Azure. In this case the VNet, subnets and OpenShift cluster. |
| Virtual Network | Provides a private network environment within the Azure cloud for hosting the other services.  |
| Worker Subnet | Provides network interface for the OpenShift worker nodes.  |
| Master Subnet | Provides network interface for the OpenShift master nodes  |
| ARO | Azure Red Hat OpenShift (ARO) |

## Example Usage

1. Install Ansible 
1. Install Azure CLI
1. Login to Azure CLI

    $ az login

1. Clone repo

    $ git clone https://github.com/cloud-native-toolkit/ansible-azure-infra-openshift.git

1. Modify the variables in quickstart.yaml

    $ cd ansible-azure-infra-openshift/
    $ vi ./quickstart.yaml

1. Run Ansible playbook

    $ ansible-playbook ./quickstart.yaml