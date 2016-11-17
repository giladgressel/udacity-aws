## What is AWS

AWS provides many services, most important of which is the `EC2 (Elastic Cloud Computing)` service.
EC2 instances are virtual machines managed by AWS that you access and manage via remote ssh (termnial)

Each EC2 instance acts as a dedicated Linux OS (we will be using `Ubuntu 14.04` since it works best with `AWS GPU's`)

## Do I need a GPU?

### Short answer: No.

### Long answer: 
You should begin by using one of the below instances that provide
excellent processing power, especially considering that the size of the dataset for
P2 is relatively small.

AWS also limits GPU access to new customers.  If your account is new, your limit is `Zero` and you
need to request a limit increase which may take a few days.

Please visit http://aws.amazon.com/contact-us/ec2-request to request an adjustment to this limit

Luckily you can use one of the below instance types which provide what is called an EBS volume (Elastic Block Store).

In short, once you get your GPU instance, you will be able to detach your EBS volume that has TensorFlow and Jupyter installed and all your data
and attach it to the GPU instance and not loose as step! (Tutorial for that is coming soon)

You maybe tempted to use a c3 class instance but rememeber that EBS volumes are detachable and can be re-used on your GPU instance

# Instance Specfications and Pricing

|Instance|Memory|Compute units|Cores|
|---|---|---|---|
|c4.large|3.75 GB|8 units|2|
|c4.xlarge|7.5 GB|16 units|4|


|Instance|Linux On-Demand|
|---|---|
|c4.large|$0.105/hr|
|c4.xlarge|$0.209/hr|

Based upon how much you are willing to spend you can choose one of the above instances.  To keep cost down, remember to `Stop` the instance when you are not using it.  Don't `terminate` it since that is the same as `deleting you data`

## Launching Your First AWS Instance
Once you have singed up for AWS and are logged into your account, click the blue `Lauch Instance` button

Scroll down to the bottom of the page with the list of Amazon Machine Images or AMI's and select the `Ubuntu 14.04`

Select the `c4.large` or `c4.xlarge` and continue.  You will not have to change any thing from the next screen.  Click `add storage`.

Change the `8GB` to `20GB`.  Do not go crazy with storage.  `20GB` is more than plenty for this course and larger EBS volumes cost money.

Click `tag instance`.  The tag is just a name that will appear in the dashboard and can alwasy be chagned later.  Click `configure security group`.

In the security group, ensure `create new group` is selected.  Port `22` should be auto-filled in by AWS.  Ensue that `MyIP` is selected from the drop down.  This is extra security ensuring that only your IP can remote access your instance.

### Note:
if your IP changes very frequently; like once a day, do no select that, rather select `anywhere`.  If your IP does change frequently but you still want the extra security please see http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-network-security.html

Click `review and launch`, then `launch`.  Enter a keypair name and `download` the keypair.  

### Note about keypairs

Key pairs are for passwordless SSH access using Public Key encryption.  DO Not loose this key since it's a big hassle to recove your data. 

# Accessing your first AWS instance

Back in the `EC2` dashboard, after the instance is in `running` state.  Note the public IP or hostname for you instance.

For windows users to access your instance via SSH please see http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/putty.html

For Mac / Linux users
```
$ mv ~/Downloads/<your-key.pem> ~/.ssh/
$ chmod 400 ~/.ssh/<your-key.pme>
$ ssh -i ~/.ssh/<your-key.pem> ubuntu@IP-of-instance
```
# Setting Up TensorFlow on your new instance
