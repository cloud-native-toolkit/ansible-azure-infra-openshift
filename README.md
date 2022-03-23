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

1. Output will show the inventory of what was created, such as the below.

    ```
    arch_type: 'Quickstart'
    inventory:
        Last_Update: Wed 23 Mar 2022 12:02:16 AEDT
        aro:
            console: https://console-openshift-console.apps.bsragndk.australiaeast.aroapp.io/
            master_nodes:
                subnetId: /subscriptions/abcdef12-abcd-1234-bcde-abcdef123456/resourceGroups/recloud-rg/providers/Microsoft.Network/virtualNetworks/recloud-vnet/subnets/master-subnet
                vmSize: Standard_D8s_v3
            name: recloud-aro
            pod_cidr: 10.128.0.0/14
            service_cidr: 172.30.0.0/16
            state: Succeeded
            version: 4.9.9
            worker_nodes:
            -   count: 1
                diskSizeGb: 128
                name: recloud-aro-l48j7-worker-australiaeast1
                subnetId: /subscriptions/abcdef12-abcd-1234-bcde-abcdef123456/resourceGroups/recloud-rg/providers/Microsoft.Network/virtualNetworks/recloud-vnet/subnets/worker-subnet
                vmSize: Standard_D4s_v3
            -   count: 1
                diskSizeGb: 128
                name: recloud-aro-l48j7-worker-australiaeast2
                subnetId: /subscriptions/abcdef12-abcd-1234-bcde-abcdef123456/resourceGroups/recloud-rg/providers/Microsoft.Network/virtualNetworks/recloud-vnet/subnets/worker-subnet
                vmSize: Standard_D4s_v3
            -   count: 1
                diskSizeGb: 128
                name: recloud-aro-l48j7-worker-australiaeast3
                subnetId: /subscriptions/abcdef12-abcd-1234-bcde-abcdef123456/resourceGroups/recloud-rg/providers/Microsoft.Network/virtualNetworks/recloud-vnet/subnets/worker-subnet
                vmSize: Standard_D4s_v3
        inputs:
            cluster_name: recloud-aro
            location: australiaeast
            rg_name: recloud-rg
            secret_file_path: ./pull-secret.txt
            subnet_prefix: 23
            subscription_default: true
            subscription_id: abcdef12-abcd-1234-bcde-abcdef123456
            vnet_cidr: 10.0.0.0/22
            vnet_name: recloud-vnet
        prereqs:
            features: []
            providers:
            -   namespace: Microsoft.RedHatOpenShift
                state: Registered
            -   namespace: Microsoft.Storage
                state: Registered
            -   namespace: Microsoft.Compute
                state: Registered
            -   namespace: Microsoft.Authorization
                state: Registered
        resource_group:
            id: /subscriptions/abcdef12-abcd-1234-bcde-abcdef123456/resourceGroups/recloud-rg
            location: australiaeast
            name: recloud-rg
            state: Succeeded
            type: Microsoft.Resources/resourceGroups
        subnets:
        -   aro_type: master
            cidr: 10.0.0.0/23
            id: /subscriptions/abcdef12-abcd-1234-bcde-abcdef123456/resourceGroups/recloud-rg/providers/Microsoft.Network/virtualNetworks/recloud-vnet/subnets/master-subnet
            name: master-subnet
            privateLinkServiceNetworkPolicies: Disabled
            state: Succeeded
            type: Microsoft.Network/virtualNetworks/subnets
        -   aro_type: worker
            cidr: 10.0.2.0/23
            id: /subscriptions/abcdef12-abcd-1234-bcde-abcdef123456/resourceGroups/recloud-rg/providers/Microsoft.Network/virtualNetworks/recloud-vnet/subnets/worker-subnet
            name: worker-subnet
            privateLinkServiceNetworkPolicies: Enabled
            state: Succeeded
            type: Microsoft.Network/virtualNetworks/subnets
        vnet:
            cidr: 10.0.0.0/22
            id: /subscriptions/abcdef12-abcd-1234-bcde-abcdef123456/resourceGroups/recloud-rg/providers/Microsoft.Network/virtualNetworks/recloud-vnet
            name: recloud-vnet
            resource_group: recloud-rg
            state: Succeeded
            type: Microsoft.Network/virtualNetworks
