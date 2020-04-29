# Lab 6: Reliable Communication

## Overview

In your final assignment you are going to build a reliable communication library in Switchyard that will consist of 3 agents. At a high level, a **blaster** will send data packets to a **blastee** through a **middlebox**. As you should all know by know, IP only offers a best-effort service of delivering packets between hosts. This means all sorts of bad things can happen to your packets once they are in the network: they can get lost, arbitrarily delayed or duplicated. Your communication library will provide additional delivery guarantees by implementing some basic mechanisms at the blaster and blastee. Let's move on to the details. 


## Your Tasks

In the source directory for this exercise, you can find the starter files: `middlebox.py`, `blastee.py` and `blaster.py`.

Your reliable communication library will implement the following features to provide additional guarantees: 
1. ACK mechanism on blastee for each successfully received packet
2. A fixed-size sliding window on blaster
3. Coarse timeouts on blaster to resend non-ACK'd packets

Further details will be discussed in each Task.

> [!NOTE]
> The sentences marked with ✅ are related to the content of your report. Please pay attention.

### Task 1: Preparation

Initiate your project with our template.

[Start the task here](preparation.md)

### Task 2: Middlebox 

Implement the features of middlebox.

[Start the task here](middlebox.md)

### Task 3: Blastee 

Implement the features of blastee.

[Start the task here](blastee.md)

### Task 4: Blaster 

Implement the features of blaster.

[Start the task here](blaster.md)

### Task 5: Running your code 

Make sure that your blaster, blastee and middlebox function correctly.

[Start the task here](deploy.md)

> [!WARNING]
> Please carefully read the [FAQ](faq.md) section, for more specific details regarding the implementations.

## Handing it in

### Report

We will provide a template of your lab assignment report [here](https://box.nju.edu.cn/d/123a70ac8ff34595b18f/). You need to submit the report in your repository named `<学号><姓名>_lab_6`. The format of your report can be Microsoft Doc or PDF. An example is `123456789拾佰仟_lab_6.pdf`.

### Submit to NJU GitLab

To submit your work, you need to do the following things.

1. Modify your code and complete your report.

2. When you have done your work, put your report and code in the folder `lab_6` then commit them. Tag the commit named `<学号/lab_6>` which you want to submit. An example is `123456789/lab_6`. Finally your project will look like

   ```
   switchyard
     ├─docs/
     ├─.../
   + ├─lab_6/
   + │ ├─123456789拾佰仟_lab_6.pdf
   + │ ├─middlebox.py
   + │ ├─middlebox_params.txt
   + │ ├─blastee.py
   + │ ├─blastee_params.txt
   + │ ├─blaster.py
   + │ ├─blaster_params.txt   
     │ ├─...
   + │ └─start_mininet.py
     ├─.gitignore
     └─...
   ```

  > [!WARNING]
  > The file names in your submission have to **exactly** match the file names above. Otherwise, you will lose points!

3. Submit your work by pushing your local repository to your remote repository **with your tags** by running the command `git push origin --tags`.

  > [!WARNING]
  > **Only** commit your **source code** to your local repository. If there are some generated files that are not source code, ignore them by adding them in the file `.gitignore`.
