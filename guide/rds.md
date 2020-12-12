<h1>Step 3: RDS</h1>

<p>
Before we jump into our WordPress instance and build the site, we'll need to setup an SQL database.
<br />
We will use Amazon's <a href="https://awscli.amazonaws.com/v2/documentation/api/latest/reference/rds/index.html">RDS</a> service to create and host a scalable MySQL server.
<p>

<p>
Lets start off by creating a subnet group for our db instance.
</p>

```bash
aws ec2 describe-subnets	#grab 2 subnets from different zone

aws rds create-db-subnet cloud-1 --db-subnet-group-description "Cloud-1 db subnet group" --subnet-ids ["subnet-01234567A", "subnet-01234567B"]
```

<p>
Then we'll create the instance for our databse
</p>

```bash
aws ec2 describe-security-groups 	#grab the sg id

aws rds create-db-instance cloud-1 --db-instance-class db.t2.mirco --engine mysql --master-username admin --master-user-password farewll42@WTC --db-subnet-group-name cloud-1 --availability-zone us-east2 --storage-encrypted --vpc-security-group-ids '["sg-12345A"]'
```

<p>
If everything goes well you should have an rds instance up and running run describe-rds-instances to verify it's running.
</p>

<hr />
<a href="ec2.md">
&lt; Previous
</a>
|
<a href="wordpress.md" align="right">
Next &gt;
</a>
