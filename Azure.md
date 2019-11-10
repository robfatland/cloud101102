# Azure

## 101

- Standard Azure training site is [here](https://docs.microsoft.com/en-us/learn/azure/). 
- [Azure Quickstart launch](https://portal.azure.com/#blade/Microsoft_Azure_Resources/QuickstartCenterBlade?feature.RMFAEmailA=blade/Microsoft_Azure_Resources/QuickstartCenterBlade)
- The Azure [portal](https://portal.azure.com/#home)

From Quickstart above I selected "deploy a virtual machine" and selected Linux. Used the cheap machine, 
$0.07/hour; and so on with defaults. Created a resource group called rob5_VM and named the machine rob5-VM. 
Hopefully the username is rob5. I used `PuttyGen` to generate an RSA key; and pasted that into the configuration
box. The VM came up and (having saved the `PuttyGen` RSA key to a `.ppk` file) I was able to log in using `Putty`.
I edited a text file so I have some identifiable content on there. For reference I could also use a `.pem` 
file where the command would be 

```
ssh rob5@111.222.33.44 -i rob5-VM.pem
```

...but it was not clear how to create the `.pem` from `PuttyGen`. 

## 102

From 'learn Azure ML' top search result I find a Microsoft page that $200 test account. UW NetID 
authentication works fine. I accept terms and click through to the learning resources. I'm going to 
**Experiment using Drag and Drop Designer**. The "classic" version is deprecated; off we go with 
the latest greatest. 

* [Drag and Drop Intro](https://docs.microsoft.com/en-us/azure/machine-learning/service/tutorial-designer-automobile-price-train-score)
  * Created a Machine Learning Service workspace... takes a few minutes to deploy... notification bell gets me there
  * Ooops I was supposed to set Workspace Edition = Enterprise, not Basic. Do over.
* [Python SDK approach](https://docs.microsoft.com/en-us/azure/machine-learning/service/tutorial-1st-experiment-sdk-setup)

