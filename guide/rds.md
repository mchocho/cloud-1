<h1>Step 3: RDS</h1>

<p>
Before we jump into our WordPress instance and build the site, we'll need to setup an SQL database.
<br />
We will use Amazon's <a href="https://awscli.amazonaws.com/v2/documentation/api/latest/reference/rds/index.html">RDS</a> service to create and host a scalable MySQL server.
<p>

<p>
Lets start off by creating a subnet group for the DB instance.
</p>

```bash
aws ec2 describe-subnets	#grab 2 subnets from different zone

aws rds create-db-subnet-group --db-subnet-group-name cloud-1 --db-subnet-group-description "Cloud-1 db subnet group" --subnet-ids '["subnet-02a5b878", "subnet-2025824b"]'
```

<p>
Next we'll create a security group for the instance.
</p>

```bash
aws rds create-db-security-group --db-security-group-name cloud-1 --db-security-group-description "DB security group for cloud-1"
```

<p>
Let's add rules to our security group so the EC2 instance can connect with the DB server.
</p>

```bash
aws ec2 describe-security-groups #Grab cloud-1 security group id

aws ec2 authorize-security-group-ingress --group-id sg-1234567 --port 3306 --protocol tcp

```

<p>
Then we'll create the instance for the databse.
</p>

```bash
aws ec2 describe-security-groups 	#grab the sg id

aws rds create-db-instance --db-instance-identifier cloud-1-mysql-db --db-name wordpress --db-instance-class db.t2.micro --engine mysql --master-username admin --master-user-password "farewell42WTC" --db-subnet-group-name cloud-1 --availability-zone us-east-2b --allocated-storage 20 --vpc-security-group-ids sg-0c4b0ef20959f96fa
```

<p>
If everything goes well you should have an RDS instance up. To verify that the instance is run use the command describe-rds-instances.
</p>

<hr />
<a href="ec2.md">
&lt; Previous
</a>
|
<a href="wordpress.md" align="right">
Next &gt;
</a>
