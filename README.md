**Download Instructions**


 These are the instructions to download and run the code from the paper &quot;A General Approach for Improving Deep Learning-based Medical Relation Extraction using a Pre-trained Model and Fine-tuning&quot;, by Tao Chen, Mingfen Wu and Hexi Li.

1. Request access to the N2B2 (previously called i2b2) corpus of annotated medical data from [https://portal.dbmi.hms.harvard.edu/](https://portal.dbmi.hms.harvard.edu/). Once your request is completed (this might take a few days), please download the corpus.

1. Download the Bert-Base model from the official website: [https://github.com/google-research/bert](https://github.com/google-research/bert). Please download using the highlighted link below, the other versions won&#39;t work with the code. Once downloaded, unzip the directory.

![](RackMultipart20210319-4-1jtwwnq_html_f3c62d1f35ad0c8c.png)

1. Clone the repository with the original code from [https://github.com/chentao1999/MedicalRelationExtraction](https://github.com/chentao1999/MedicalRelationExtraction) into your local computer. If you use the git command line, you can use the following command:
 &quot;git clone [https://github.com/chentao1999/MedicalRelationExtraction.git](https://github.com/chentao1999/MedicalRelationExtraction.git)&quot;


2. Open the directory on your computer where the code was downloaded. In the &quot;pretrained bert model&quot; subdirectory, paste the unzipped directory with the pre-trained BERT models

![](RackMultipart20210319-4-1jtwwnq_html_2c5f6ac151fa2200.png)

![](RackMultipart20210319-4-1jtwwnq_html_aeea793b7331c213.png)

1. Open the corpus/i2b2 subdirectory, and paste the annotations and the groundtruth folders you&#39;ve downloaded from i2b2.

![](RackMultipart20210319-4-1jtwwnq_html_e8d210099465a800.png)

1. Zip the root folder, the main directory that contains the code for this project. Your code is ready to pasted into your virtual machine.

**Setting up the machine**

1. For this project, I used Deep Learning Base AMI (Ubuntu 18.04) Version 24.0, with a t2.2xlarge instance, running in São Paulo.
2. To create a new aws machine, go to the aws console and, on the right menu bar, select &quot;Instances&quot;. Then, select &quot;Launch Instance&quot;.


![](RackMultipart20210319-4-1jtwwnq_html_b8838f4305965332.png)

1. Type in &quot;Sagemaker&quot; in the search bar, and select the Deep Learning Base AMI (Ubuntu 18.04) Version 24.0.


![](RackMultipart20210319-4-1jtwwnq_html_d17c18a17baa837c.png)

1. Finish creating your virtual machine. For mine, I used the t2.2xlarge.

1. To connect to your machine, go to the aws console website, go to &quot;instances&quot;, select your instance and press connect. It will give you the ssh command you need to connect to your virtual machine using the command line. Please note that you will need to check this command periodically: your public DNS will probably change whenever you restart the machine.

![](RackMultipart20210319-4-1jtwwnq_html_ca11f0db469712cb.png)

1. Still on your local computer, open and command prompt, cd to the directory where you keep you access key, paste and run the ssh command you&#39;ve copied. If it asks you if you&#39;re sure if you want to connect, type &#39;yes&#39;.


![](RackMultipart20210319-4-1jtwwnq_html_d73f22f9023ba276.png)

1. If you see the information about the AMI, you&#39;ve connected to the aws


![](RackMultipart20210319-4-1jtwwnq_html_15aed0167cead7f7.png)

1. Please run the following command:  pip3 install tensorflow==1.14. This will downgrade your tensorflow (which is 2.0 or above) to the version of tensorflow used in the code.


1. Run the following code on the command line on your virtual machine:  jupyter notebook --port 8080. This will create a Jupyter Notebook, which is a local website that allows us to see and access files. If this is your first time using the Jupyter notebook, it will also give you an access token. This will allow us to access the remote files from our local machine.

![](RackMultipart20210319-4-1jtwwnq_html_2d3daae033773d52.png)

1. On your local computer, create a tunnel to the jupyter notebook: open a new command line window, go to the directory where you have your access key file to your aws machine, and run:

ssh -i &quot;key.pem&quot; -L 8080:localhost:8080 ubuntu@address

Where &quot;key&quot; is the name of your access key file and ubuntu@address is the username and address that you use to connect to your aws machine. For example, [ubuntu@ec2-54-235-229-89.compute-1.amazonaws.com](mailto:ubuntu@ec2-54-235-229-89.compute-1.amazonaws.com).

![](RackMultipart20210319-4-1jtwwnq_html_2d56ce964420d000.png)

![](RackMultipart20210319-4-1jtwwnq_html_26f66aa9f98ff701.png)

1. On your local computer, using Google Chrome, go to localhost:8080. This is the jupyter notebook from your aws machine, tunneled to your computer. Please put in the token, if required. You will then be able to acces the on the folder of your virtual machine.

![](RackMultipart20210319-4-1jtwwnq_html_85c36615fc6e4858.png)

1. On your local computer, zip the main folder with your code, the pre-trained BERT model and the i2b2 corpus. Then, upload the folder into Jupyter notebook.


1. On your aws machine, unzip the file: if it is called Medical.zip, for example, use the command unzip Medical.zip. If it says you don&#39;t have the zip command, download it with sudo apt-get install unzip

1. You now have all the files you need in your aws machine to run the code.

**Running the Code**

**Training:**

1. To run the training code, in your aws machine, using the command line, go to the root directory where your downloaded code is, for example, cd Medical. Type in the command dir to make sure that files data\_process\_i2b2.py and run\_i2b2.py are in that directory.

1. Create a new tmux session: this will allow you to access the code that&#39;s running even if you turn of your local computer or end the remote connection session. To do this, run the command: tmux new -s mywindow

1. Run the following command to process the data, it should only take a few minutes to finish:python3 run\_i2b2.py train

1. Run the following command to train the data. It should take about 54 hours. In order to check the status, just connect to your aws machine through ssh and run the command tmux a -t mywindow and it will take you to the same session that you were in before. Please keep your aws machine connected and running.

1. Once it&#39;s finished, it will print in your session that the training has been completed.

![](RackMultipart20210319-4-1jtwwnq_html_43e47806d06f575f.png)

1. If you will not immediately start testing, please stop your aws machine so you won&#39;t be charged until you use it again.


**Testing:**

1. In order to test the code, in your virtual machine, acess your tmux session with tmux a -t mywindow if it is still running. If it&#39;s not, create a new one with tmux new -s mywindow.

2. Using the command line, go to the directory where your code is and run the following command: python3 run\_i2b2.py test.

3. You will get some warnings, but, unless there is an error, it will continue testing. This could take a few hours.

4. Once you are able to write commands again, the testing should be finished.

5. Zip the results directory: inside the directory where your code is, run zip -r result.zip result. This will create a zipped folder with the results of your trained model.

6. If you want to download the trained model, run another Jupyter notebook with the command jupyter notebook –port 8080 and access it on your computer like you did when you uploaded your data. You can then download the results file to your local computer.


![](RackMultipart20210319-4-1jtwwnq_html_84b46840016153d3.png)
