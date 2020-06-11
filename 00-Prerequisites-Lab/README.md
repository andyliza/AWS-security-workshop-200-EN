# LAB 0 - Prerequisites

### Creating an EC2 Key Pair

First we need to create a key pair that will be used to establish an SSH
connection.

1)  Go to the *Key Pairs* in the EC2 instances console

![images](images/1b7a0e08bd10420fa37c1270cffe1f54.png)

2)  Click on the *Create Key Pair* button

![images](images/d3c32b52f680b2710b9bb1a93c1407c1.png)

3)  Key in *sec-keypair* in the name box.

![images](images/c4490616d6988656078799a2695d6b01.png)

4)  Now you will be able to see the key pair in the console and it will be in your *Downloads* folder.

![images](images/7324683f50d7dbe301fa0c476d84153a.png)

### Deploy the CloudFormation template for the sample application "Unicorn Adoption Site"

1) Download the cloudformation template from <a id="raw-url" href="https://raw.githubusercontent.com/andyliza/AWS-security-workshop-200-EN/master/CloudFormation/securityworkshop.template">this link</a>. Just simply right click on the link and select *Save Link As*. Store the file on your computer as we will need it in the next steps.

![images](images/rightclick.png)

2) Now go to the AWS Console and in the search bar type CloudFormation and press Enter. Make sure that you have any previous AWS sessions closed. Click on __Create Stack__

![images](images/cloudformation-upload.png)

3) Make sure that __Template is ready__ and __Upload a template file__ options are selected. Click on **Choose file** and upload the template that you downloaded in step **1)** of this section and click **Next**

![images](images/cloudformation-upload-2.png)

4) In the the form add a **Stack Name**, select the newly created __key__. The VPC CIDR, RDS Password and Username are already prepopulated for you. Once everything is filled in press **Next**

![images](images/cloudformation-upload-3.png)

5) In the next screen scroll to the bottom of the page and press **Next**.

![images](images/cloudformation-upload-4.png)

6) In the summary page click on **Create Stack**.

![images](images/cloudformation-upload-5.png)

7) Once the stack is deployed successfully click on the **Output** tab and take note the values listed there. You can copy them into a scratch pad.

![images](images/cloudformation-upload-6.png)

8) Go to the Cloud9 console and open the environment created by CloudFormation.

![images](images/cloud9.png)

9) In the Cloud9 environment drag and drop the Key Pair created at the beginning of this prerequisites lab and save it.

![images](images/cloud9keypair.png)

10) In the command prompt key in the following command:

```
chmod 400 [the name of your keypair]

ssh -i "[the name of your keypair]" ubuntu@[IP address of the webserver - can be found in the Cloudformation Output]

```
**:heavy_exclamation_mark: Replace the keypair name and IP address values with the ones that you use in the previous steps**

![images/](images/connecttoec2.png)

11) Once you are connected key in and execute the following commands:

```
cd /var/www/unicorn-app/SQLScripts/

mysql -h [The RDS endpoint given in the Cloudformation output ] -u admin -p < setup.sql

```
Once prompted for the Aurora MySQL server password, key in "securityworkshop" and wait for 7 seconds for the setup to completed.

![images/](images/sqlsetup.png)

12) Once the setup is complete and no error is prompted, edit the __param.yaml__ located in /var/www/unicorn-app and add the RDS endpoint displayed in the Outputs of Cloudformation

```
sudo nano /var/www/unicorn-app/param.yaml

```

![images/](images/param.png)

13) Press CTRL+X and 'Y' to Save the parameters

14) For the changes to take effect we need to restart the nginx and gunicorn3 services:

```
sudo systemctl restart gunicorn3
sudo systemctl restart nginx

```

15) Once the services are started in the Outputs of the CloudFormation template you will see the URL of our webapp.

![images](images/cloudformation-upload-6.png)

16) Click on it and test if you can add a unicorn.

![images](images/addunicorn.png)

17) If everything is successful you will see the unicorn in the listed

![images](images/list.png)

18) Feel Free to add more unicorns in the list :) so we can play later.


When you see that the operation has been completed successfully move to the [first lab (CloudTrail)](../01-CloudTrail-Lab/README.md)
