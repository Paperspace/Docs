# Experiment Builder interface

### Experiment Builder: A GUI for Running Jobs <a id="h_15322951121524587990731"></a>

You can run Experiments in Gradient without ever leaving your web browser! The Experiment Builder is a great way to learn more about how Jobs are structured and you can easily run your first GPU ob on Gradient without writing a single line of code!

![](../.gitbook/assets/image%20%281%29.png)

### Run an Experiment Using the Builder <a id="h_39323868261524588004147"></a>

Once you have logged in, navigate to [https://www.paperspace.com/console/jobs/builder](https://www.paperspace.com/console/jobs/builder) and click the first example, "Fast Style Transfer." The defaults are already provided, but it is worth looking at what parameters are provided.  

**MachineType.**  What type of instance to run your job on. We recommend starting with a GPU+.

**Container.** Experiments are run within a docker container. You can run a public or private container. Learn more [here](https://support.paperspace.com/hc/en-us/articles/360003415434).

**Workspace.** The workspace is the collection of code that is run. It can be a Git repository \(public or private\) or your local working directory \(if you are using the CLI\) which is uploaded to the docker container during the job running process.

**Command.** The command is the entry point to the container. This is the line of code that will kick off your job. It could be a bash script \`./run.sh\` or \`python main.py\` as just some examples. 

**Ports.** You have the option to attach a public IP automatically. Supports opening multiple ports simultaneously, separated by `:` . Learn more about opening ports [here](https://support.paperspace.com/hc/en-us/articles/360003412574).

Once you have examined the parameters, hit "Submit Job" and watch your job run!

### CLI Commands <a id="h_97332503391524588015509"></a>

The experiment builder also provides a nice summary of what command will be run. After you install the Paperspace CLI you could run this command directly from your command line and it would behave exactly the same way as the GUI builder!

![](https://support.paperspace.com/hc/article_attachments/360004107534/Screen_Shot_2018-04-23_at_8.06.41_PM.png)

