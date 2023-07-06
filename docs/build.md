# Building apps for FoodPort

To build applications for [FoodPort](http://10.148.57.4/), you must have access to the Microsoft Azure [FoodPort Portal](https://portal.azure.com/#home) and have the necessary permissions for creating a new **virtual machine (VM)** image.
Contact Adam Koziol ([adam.koziol@inspection.gc.ca](mailto:adam.koziol@inspection.gc.ca)) to obtain these necessary permissions.

## How apps work on FoodPort

When a user runs a command on FoodPort (e.g. assembling a bacterial genome), a batch VM is created based upon a pre-existing VM image which contains the necessary software and dependencies for executing this command.
If there are any files that are needed as input for the software inside of the batch VM (e.g. `.fastq.gz`), these are placed inside of a blob container and mounted to the batch VM using [BlobFuse](https://learn.microsoft.com/en-us/azure/storage/blobs/blobfuse2-what-is).
Once mounted, these files are available to be used by the batch VM for processing, analysis, etc.
Finally, a Shell command is executed within the batch VM to perform the desired task.
All of this happens beneath the FoodPort web interface.

Therefore, the requirements for building an application on FoodPort are:

- A VM image containing the necessary software and dependencies for executing the desired command(s).
- A web user interface for users to submit their command(s).

## Creating a VM image

To create a new VM image:

1. In the Microsoft Azure [FoodPort Portal](https://portal.azure.com/#home), navigate to [Virtual machines](https://portal.azure.com/#view/HubsExtension/BrowseResource/resourceType/Microsoft.Compute%2FVirtualMachines).
2. In the top-left corner of the window, click 'Create' and choose 'Azure virtual machine'.
3. Under the Basics tab, change the following:
      - Subscription: `CFDC-FoodPort-Sub`
      - Resource group: `CFDC-FoodPort-Batch-rg`
      - Virtual machine name: `name_of_new_image`
      - Region: `(Canada) Canada Central`
      - Image: `Ubuntu Server 20.04 LTS - x64 Gen2`
      - Security type: `Standard`
        - (The image must be selected first)
      - Size: `Standard_D4ds_v5`
      - Authentication type: Password
        - Username: `[username]`
        - Password: `password`
      - Public inbound ports: `None`
4. Under the Networking tab, change the following:
      - Virtual network: `CFDC-FoodPort-vnet`
      - Subnet: `CFDC-FoodPort-BatchNodes-snet (10.148.57.32/27)`
      - Public IP: `None`
5. Under the Tags tab, change the following:
      - Name: `TechContact`
      - Value: `email_address_of_contact`
6. Under the Review + create tab, click 'Create' and wait for the VM image to be created.

## Developing in VMs

To add software and other dependencies to your new VM image, the process is as follows:

1. Spin up a new VM based upon the previously created VM image.
2. Connect to the new VM.
3. Install software and other dependencies.
4. Capture the VM as a new version of the VM image.

### Spinning up a new VM

### Connecting to a new VM

### Installing software and other dependencies in a new VM

### Capturing a new VM as a VM image version

## Creating a user interface
