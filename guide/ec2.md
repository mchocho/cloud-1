<h1>Step 2: This should be EC2 deploy</h1>

<p>
After setting our credentials up to CLI, we'll move onto creating the EC2 instance that will contain our WordPress application.
<br />
First we'll create our key pair for our instances. Open your terminal and run
</p>

```bash
aws ec2 create-key-pair --key-name "cloud-1-key-pair"
```

<p>
You'll want to save the public and private key in a safe location on your machine.
<br />
Next we'll create our security group for the instance.
</p>

```bash
aws ec2 describe-vpcs	#Pick a vpc-id to use

aws ec2 create-scurity-group --group-name cloud-1 --description "Security group for Wordpress instance" --vpc-id vpc-5e1234567 
```

<p>
In our for us to connect with our instance we'll add rules to our security group.
</p>

```bash
aws ec2 describe-security-groups	#grab cloud-1 security group id

aws ec2 authorize-security-group-ingress --group-id sg-1234567 --port 22 --protocol tcp --cidr 0.0.0.0/32 #SSH

aws ec2 authorize-security-group-ingress --group-id sg-1234567 --port 80 --protocol tcp --cidr 0.0.0.0/32 #HTTP
```
<p>
Next we'll need to find out the id of the AMI which we will use This command might take a while ☕
</p>

```bash
touch ami.json

aws ec2 describe-images < ami.json
```
<p>
Inspect the list and choose an image. For this demonstration we I'll go the image ami-00000eba05d89f9dd.
<br />
Finally we'll create and run our EC2 instance
</p>

```bash
aws ec2 describe-subnets		#grab a subnet id

aws ec2 run-instances --instance-type t2.micro --count 1 --key-name cloud-1 --image-id ami-00000eba05d89f9dd --security-group-ids sg-1234567 --subnet-id subnet-2ff123456 
```

<p>
If everything goes right our EC2 is up and running. Copy the public IP address and store it with your security group id, image id, and subnet id.
</p>

<hr />
<a href="../README.md">
&lt; Previous
</a>
|
<a href="rds.md" align="right">
Next &gt;
</a>