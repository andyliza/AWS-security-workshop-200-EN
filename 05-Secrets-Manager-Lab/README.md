# LAB 5 - AWS Secrets Manager
#### To create and store your secret

1) Sign in to the AWS Secrets Manager console

2) On either the service introduction page or the secrets list page,
    choose **Store a new secret**.

3) On the **Store a new secret** page, choose **Credentials for Database**, in
   the username type *admin and in the password box type techshift2019. Choose
   the security created in the previous lab called techshiftkey2019* and select
   the database created in the previous lab.

![iamges](images/62ee37a962c8d96713af8b33f510fe6d.png)

4)  Give the *Secret* a name – *techshift/demo/aurora*. Add a description and
    press *Next*.

![iamges](images/8625b77cdb1bb9b3ac03fb8c97b92836.png)

5)  Enable automatic rotation for 30 days using a Lambda function and name it
    *aurora-secret-rotation-lambda* and press *Next*.

![iamges](images/6b319d5df7d49e8c19e7b662969e2954.png)

6)  In the review page press *Store*.

![iamges](images/5394a066ef14f52afd154cf9e8bdf262.png)

#### To retrieve your secret in the AWS Secrets Manager console

1) On the secrets list page, choose the name of the new secret that you created
    in the previous section.

>   The details page for your secret appears.

2) In the **Secret value** section, choose **Retrieve secret value**.

![iamges](images/retrieve.png)

4) Once you can see the values of the secret click on **Edit**

![iamges](images/edit.png)

5) Add a new key-pair for the database called __dbname__ and the value __unicorn__ and click **Add**.

![iamges](images/add.png)

5) Once you are done click **Save**.

#### To use the secret from Secrets Manager in your code

1) Go to the Cloud9 console and open the environment created by CloudFormation.

![images](images/cloud9.png)

2) In the Cloud9 environment drag and drop the Key Pair created at the beginning of this prerequisites lab and save it.

![images](images/cloud9keypair.png)

3) In the command prompt key in the following command:

```
chmod 400 [the name of your keypair]

ssh -i "[the name of your keypair]" ubuntu@[IP address of the  - can be found in the Cloudformation Output]

```
**:heavy_exclamation_mark: Replace the keypair name and IP address values with the ones that you use in the previous steps**

![images/](images/connecttoec2.png)

4) Once you are connected to the instances go to the **/var/www/unicorn-app**

```
cd /var/www/unicorn-appear

```
and open up **app.py**

```
sudo nano app.py

```
5) In the file you will notice that there are some commented lines using #. Go ahead and uncomment them as instructed in the file and comment the following two lines:

```
#param=yaml.load(open('param.yaml'))

```
and

```
app.config['SQLALCHEMY_DATABASE_URI'] = 'mysql://'+param['mysql_user']+':'+param['mysql_password']+'@'+param['mysql_host']+'/'+param['mysql_db']

```
See a sample here

![images/](images/codemodif.png)





Proceed to the [next lab (WAF Lab)](../06-WAF-Lab/README.md)
