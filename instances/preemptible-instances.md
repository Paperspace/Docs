# Preemptible Instances

## What is a preemptible instance?

A preemptible instance is a machine instance that is provided at a lower cost but can be interrupted by the cloud provider at any time. For comprehensive information, see this [GCP article](https://cloud.google.com/compute/docs/instances/preemptible). For experimentation, testing, and short-lived computations preemptible instances offer a lower cost alternative to traditional Paperspace instances. Paperspace runs your job or notebook on a preemptible instance if that option is selected.

## How much does a preemptible job or notebook cost?

A job or notebook will be substantially cheaper if ran on a preemptible instance. Savings can range from [20-65%](https://support.paperspace.com/hc/en-us/articles/360007742114) depending on the instance type.

![](https://support.paperspace.com/hc/article_attachments/360023958893/mceclip0.png)

![](https://support.paperspace.com/hc/article_attachments/360023958973/mceclip1.png)

## What is a preemptible job?

A preemptible job is one running on a VM that is preemptible. The job costs less to run but can be preempted at any time, even within the first few minutes. Preemptible instances are always shut down after 24 hours, therefore long-running jobs should not be run on preemptible instances. If your job gets preempted you will still have access to the artifacts and logs associated with that job. You may rerun the job by hitting rerun in the job runner.  Adding auto-save commands to your code is suggested. 

## What is a preemptible notebook?

A preemptible notebook is one running on a VM that is preemptible. The notebook costs less to run but can be preempted at any time, even within the first few minutes. You will lose access to the notebook while the machine gets preempted, but you can relaunch the notebook on another machine by hitting start in the notebook runner. Adding auto-save commands to your code is suggested. 

