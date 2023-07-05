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

## Creating a user interface
