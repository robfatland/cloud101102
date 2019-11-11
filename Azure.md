# Azure

## 101

- Standard Azure training site is [here](https://docs.microsoft.com/en-us/learn/azure/). 
- [Azure Quickstart launch](https://portal.azure.com/#blade/Microsoft_Azure_Resources/QuickstartCenterBlade?feature.RMFAEmailA=blade/Microsoft_Azure_Resources/QuickstartCenterBlade)
- The Azure [portal](https://portal.azure.com/#home)


From Quickstart above I selected "deploy a virtual machine" and selected Linux. Used the cheap machine, 
$0.07/hour; and so on with defaults. Created a resource group called rob5_VM and named the machine rob5-VM. 
Hopefully the username is rob5. I used `PuttyGen` to generate an RSA key; and pasted that into the configuration
box. The VM came up and (having saved the `PuttyGen` RSA key to a `.ppk` file) I was able to log in using `Putty`.


I edited a text file `rob5.txt` so I have some identifiable content on there. 


### Digression on using `bash` rather than `PuTTY` for `ssh` login


Note if I make the file me-read-only I can also use a `.pem` file to login from the bash prompt.
First in `PuttyGen` at the top select *Conversions* and *Export OpenSSH Key*. When saving be sure
to append a `.pem` file extension. 


From Windows I run a `bash` shell as administrator but this installs in a "Linux file system" on my 
Windows machine where I have standard permissions. If the above `.pem` file is saved somewhere in my
Windows User space (i.e. not in the `bash` file system) I am not permitted to change the file mode.
So I typically copy the `.pem` file into my Linux home directory with a command that looks something
like this (again: In the bash shell window)...

```
cd \mnt\c\Users\rob5\Documents
mv rob5-VM.pem ~
cd ~
chmod 400 rob5-VM.pem
ls -al
```

That last command allows you to verify that the permissions on the `.pem` file are set properly. 
Now given that we have set the username to be `rob5` and the VM is at ip address `111.222.33.44`
we can at last log in to the virtual machine: 


```
$ ssh -i rob5-VM.pem rob5@111.222.33.44 
```

Sure enough I found the `rob5.txt` file here as it should be. 

### Image Create and Restore

The verb for creating an image on Azure is `Capture`. The console makes both `Stop` and `Capture` easy clicks.
Note the option to preserve the ip address is presented as a check box. The `Capture` makes the VM unusable
in a sort of mutually exclusive status trade. I checked the box to delete the VM. When this is done I see the
image (in the resource group listing) and an additional six resources where I remark on *type* for each:

```
rob5-VM-image-1234567890         machine image
rob5-VM-ip                       public ip address 
rob5-VM-nsg                      network security group
rob5-VM663                       network interface
rob5-VM_OsDisk_etcetc            30GB unattached SSD drive (about $1.20 / month)
rob5_VM-vnet                     virtual network
rob5vmdiag                       storage account for retaining diagnostics for resources
```

I created a snapshot of the disk and deleted the disk; so replace row 5 above with 

```
rob5-VM_snapshot
```

Now to restore the image. 


## 102

From 'learn Azure ML' top search result I find a Microsoft page that $200 test account. UW NetID 
authentication works fine. I accept terms and click through to the learning resources. I'm going to 
**Experiment using Drag and Drop Designer**. The "classic" version is deprecated; off we go with 
the latest greatest. 

* [Drag and Drop Intro](https://docs.microsoft.com/en-us/azure/machine-learning/service/tutorial-designer-automobile-price-train-score)
  * Created a Machine Learning Service workspace... takes a few minutes to deploy... notification bell gets me there
  * Ooops I was supposed to set Workspace Edition = Enterprise, not Basic. Do over.
* [Python SDK approach](https://docs.microsoft.com/en-us/azure/machine-learning/service/tutorial-1st-experiment-sdk-setup)

