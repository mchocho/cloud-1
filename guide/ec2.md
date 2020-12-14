<h1>Step 2: This should be EC2 deploy</h1>

<p>
After setting our credentials up with the CLI, we'll move onto creating the EC2 instance that will contain our WordPress application.
<br />
First we'll create our key pair for our instances. Open your terminal and run
</p>

```bash
touch cloud-1-key-pair.pem

aws ec2 create-key-pair --key-name cloud-1-key-pair --query 'KeyMaterial' --output text > cloud-1-key-pair.pem

```

<p>
It's crucial that you save the permission content of the response in a pem file.
<br />
Next we'll create our security group for the instance.
</p>

```bash
aws ec2 describe-vpcs	#Pick a vpc-id to use

aws ec2 create-security-group --group-name cloud-1 --description "Security group for Wordpress instance" --vpc-id vpc-d079c6bb
```

<p>
In order for us to connect with our instance we'll add rules to our security group. <a href="http://checkip.amazonaws.com/">Include your IP address</a> in the cidr to gain access to the instance.
</p>

```bash
curl ifconfig.me -s #Grab IP address

aws ec2 describe-security-groups	#Grab cloud-1 security group id

aws ec2 authorize-security-group-ingress --group-id sg-1234567 --port 22 --protocol tcp --cidr 197.90.166.46/32 #SSH

aws ec2 authorize-security-group-ingress --group-id sg-1234567 --port 80 --protocol tcp --cidr 197.90.166.46/32 #HTTP inbound

aws ec2 authorize-security-group-egress  --group-id sg-1234567 --port 80 --protocol tcp --cidr 197.90.166.46/32 #HTTP outbound
```
<p>
Next we'll need to find out the id of the AMI to use.
<br />
<h3>Note! This command might take a while ☕</h3>
</p>

```bash
touch ami.json

aws ec2 describe-images > ami.json

...

less ami.json
```
<p>
Inspect the list and choose an image. <strike>For this demonstration we I'll go with ami-00000eba05d89f9dd.</strike> It's been noted that Amazon changes their image ids periodically. An Amazon ECS Linux based AMI is recommended. If you're not sure of a particular image, search for it in the <a href="https://aws.amazon.com/marketplace/search/results?page=1&filters=fulfillment_options&fulfillment_options=Ami&ref_=header_nav_dm_ami">marketplace</a>
<br />
Finally we'll create and run the EC2 instance
</p>

```bash
aws ec2 describe-security-groups	#Grab cloud-1 security group id

aws ec2 describe-subnets			#Grab a subnet id

aws ec2 run-instances --instance-type t2.micro --count 1 --key-name cloud-1-key-pair --image-id ami-00000ebaEXAMPLE --security-group-ids sg-1234567EXAMPLE --subnet-id subnet-2ff123EXAMPLE 

aws ec2 describe-instances			#Grab the Public DNS
```

<p>
If everything goes well the EC2 instance should be up and running. Copy the public IP address and store it with your security group id, image id, and subnet id.
</p>

<hr />
<a href="iam.md">
&lt; Previous
</a>
|
<a href="rds.md" align="right">
Next &gt;
</a>