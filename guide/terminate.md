<h1>Terminating your instance</h1>

<p align="center">
	<img src="https://i.imgur.com/Hnr5wON.jpeg" width="450px" height="320px"  />
</p>

<p>
You need to be able to shut down your vpc instances or else things might get pricey.
Amazon will not disable your instances for you and may proceed to charge you for the resources
you consume.
</p>

<br />

If you want to <a href="https://awscli.amazonaws.com/v2/documentation/api/latest/reference/autoscaling/update-auto-scaling-group.html">remove all instances created by the autoscaling group</a> run:

```bash
# Terminate all instances created by the autoscaling group
aws autoscaling update-auto-scaling-group --auto-scaling-group-name cloud-1 --min-size 0 --max-size 0 --desired-capacity 0

# The instances attached to the autoscaler should be written off as terminating.
aws ec2 describe-instances

```

To <a href="https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/stop-instances.html">stop [1]</a> and <a href="https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/terminate-instances.html">terminate</a> your ec2 instances run:

```bash
# Find remaining instances
aws ec2 describe-instances

# Stop the ec2 instance. Amazon won't charge for a stopped instance[1].
aws ec2 stop-instances --instance-ids i-0e42

# Terminate (delete) your ec2 instance
aws ec2 terminate-instances --instance-ids i-0e42

```

To <a href="https://awscli.amazonaws.com/v2/documentation/api/latest/reference/rds/stop-db-instance.html">stop</a> and <a href="https://awscli.amazonaws.com/v2/documentation/api/latest/reference/rds/delete-db-instance.html">delete</a> your RDS instance run:

```bash
# Stop your RDS instance
aws rds stop-db-instance --db-instance-identifier cloud-1-mysql-db

# Delete your RDS instance
aws rds delete-db-instance --db-instance-identifier cloud-1-mysql-db

```

Don't forget to check if there might be any instances running that you aren't aware of.
If you're having issues you can always use the <a href="https://console.aws.amazon.com/ec2/">AWS Console</a> 

<hr />
<a href="CDN.md">
&lt; Previous
</a>
|
<a href="../README.md">Home</a>