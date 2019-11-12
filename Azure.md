# Azure

## 101

- Standard Azure training site is [here](https://docs.microsoft.com/en-us/learn/azure/). 
- [Azure Quickstart launch](https://portal.azure.com/#blade/Microsoft_Azure_Resources/QuickstartCenterBlade?feature.RMFAEmailA=blade/Microsoft_Azure_Resources/QuickstartCenterBlade)
- The Azure [portal](https://portal.azure.com/#home)


### Instance Create, Capture, Delete, Restore

From Quickstart above I selected "deploy a virtual machine" and selected Linux. Used a cheap D1 machine, 
$0.07/hour; and so on with defaults. Created a resource group called `rob5_VM` and named the machine `rob5-VM`. 
Username is `rob5`. I used `PuttyGen` to generate an RSA key; and pasted that into the configuration
box. The VM came up and (having saved the `PuttyGen` RSA key to a `.ppk` file) I was able to log in using `Putty`.
To do this use the navigation pane to `SSH > auth > Select file` and `Session` with `Host` set to 
`username@111.222.33.44` and finally `Open`. At the prompt click `Yes` and an `ssh` window should open 
with a command prompt. 


Once logged in to the Azure VM I edited a text file `rob5.txt` to create an identifiable bit of content. 


#### Digression on using `bash` rather than `PuTTY` for `ssh` login


If I have and prefer a `bash` shell on my Windows machine I authenticate using a `.pem` file.
This file must have correct permissions; so we have this procedure: 


- In `PuttyGen` use *Conversions* and *Export OpenSSH Key*. Append a `.pem` file extension. 
- From Windows run the `bash` shell as administrator
  - In my case `bash` has created a Linux file system that is *not* within my Windows User space.
  - I typically write the `.pem` file within my Windows User space
  - Key point: `bash` is not permitted to change file permissions in my Windows User space
  - In `bash` I will need to copy the `.pem` file to my Linux home directory `~`

```
# cd \mnt\c\Users\rob5\Documents
# mv rob5-VM.pem ~
# cd ~
# chmod 400 rob5-VM.pem
# ls -al
# ssh -i rob5-VM.pem rob5@111.222.33.44 
```


In practice I have now logged into the Azure VM twice: Once from `PuTTY` using the `.ppk` file and
once from `bash` using the `.pem` file. Both sessions see the test file `rob5.txt`. 


### Image Create and Restore

To be convinced that my work on the Azure VM is safe I wish to delete and then restore the VM. Before 
doing so I create a machine image using the `Capture` function on the Azure portal. The VM page on
the portal features both `Stop` and `Capture` buttons. On `Stop` there is an option to preserve the 
ip address. `Capture` stops the VM as well; and I checked the box to automatically delete the VM
once image creation is done. Finished: I now see the
image in the resource group listing and six other resources:


```
rob5-VM-image-1234567890         machine image
rob5-VM-ip                       public ip address
rob5-VM-nsg                      network security group
rob5-VM663                       network interface
rob5-VM_OsDisk_etcetc            30GB unattached SSD drive (about $3.60 / month)
rob5_VM-vnet                     virtual network
rob5vmdiag                       storage account for retaining diagnostics for resources
```


I created a snapshot of the disk and deleted the disk. However this proves to be unnecessary: 
The `image` includes the snapshot of the 30GB root disk. 


To restore the image I first identify it in the resource group, select it, click Start; and fill in the
various form elements. This requires a new key and selecting an instance type. Once it starts up I log in 
and my test file is there as anticipated. 


Having done this I ran through it again to reinforce the process. Create to Login to Capture (with auto-delete)
takes a couple of minutes all told. This time I deleted the disk before re-starting the VM. Leaving the disk
alone makes it a zombie: It will persist and cost $0.12 / GB / month. By default at 30GB this is 
$3.60/month/zombie. 


The initial and repeat tests check out.  Deleting the resource group is a fast way of cleaning up. 


## 102


From 'learn Azure ML' top search result I find a Microsoft page that $200 test account. UW NetID 
authentication works fine. I accept terms and click through to the learning resources. I'm going to 
**Experiment using Drag and Drop Designer**. The "classic" version is deprecated; off we go with 
the latest greatest. 


* [Drag and Drop Intro](https://docs.microsoft.com/en-us/azure/machine-learning/service/tutorial-designer-automobile-price-train-score)
  * Created a Machine Learning Service workspace... takes a few minutes to deploy... notification bell gets me there
  * Ooops I was supposed to set Workspace Edition = Enterprise, not Basic. Do over.
* [Python SDK approach](https://docs.microsoft.com/en-us/azure/machine-learning/service/tutorial-1st-experiment-sdk-setup)

