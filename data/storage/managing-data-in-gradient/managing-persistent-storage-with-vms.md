# Managing Persistent Storage with VMs

{% hint style="warning" %}
This feature is only available in the hosted gradient Gradient version. [Contact Sales](https://info.paperspace.com/contact-sales) to learn more.
{% endhint %}

If you are using both a Paperspace Linux VM and Gradient you can share files between them through Persistent Storage. Learn more about Persistent Storage [here](../#persistent-storage).

Once you have set up either a Gradient Jupyter Notebook or a Job you will have access to Persistent Storage in `/storage`.  
  
Persistent Storage is kept in two regions based on your machine type:

1. East Coast \(NY2\)
2. GCP West

### From Your \(Terminal Only/SSH\) VM

To access the same folder in your Paperspace VM simply log on and type `ls /` into the terminal and you will see the storage folder.  Typing `ls /storage` will show you what folders you have in storage.  If you have Notebooks or Jobs set up in only one region then you will only see one folder.  If you have it set up in two different regions, you will see two folders.  Typing `ls /storage/storagefoldername` will show you the contents of that folder.  

![](https://support.paperspace.com/hc/article_attachments/360007661754/mceclip1.png)

###  From a Linux Desktop 

For users that are using a desktop environment such as our [Machine Learning in a Box Template](https://support.paperspace.com/hc/en-us/articles/115002305973-Machine-Learning-in-a-Box), you will be able to see Persistent Storage in your `/storage` folder.  Simply click on the "Home" Folder on your desktop.  Then click on "Computer" near the bottom in the left pane:

![](https://support.paperspace.com/hc/article_attachments/360007649753/mceclip1.png)

Click on storage and you will see your folders containing all your files. 

![](https://support.paperspace.com/hc/article_attachments/360007592874/mceclip2.png)

