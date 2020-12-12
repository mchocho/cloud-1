<h1>Step 5: Let's build a fence</h1>

<p align="center">
	<img src="https://i.imgur.com/c4kfrzQ.jpeg" width="450px" height="320px" />
</p>

<p>
Now that we finally managed to get the WordPress app up & running, we'll need to add the <a href="">load balancer</a>
</p>

```bash
aws ec2 describe-security-groups 	#grab the securtiy group id

aws ec2 describe-subnets

aws elbv2 create-load-balancer --name cloud-1 --security-groups sg-CLOUD-1SGID --subnets subnet-b7d581c0 subnet-8360a9e7
```

<p>
Remember, the 2 subnets you specify will have to be in different availibility zone. If successful the ouput will include the Amazon Resource Name (ARN) of the load balancer, save this value.
<br />
Next we'll create a target group and link it to the vpc.
</p>

```bash
aws elbv2 create-target-group --name cloud-1 --protocol HTTP --port 80 --vpc-id vpc-0598c7d356EXAMPLE
```

<p>
The resulting output includes the ARN of the target group, save this value.
<br />
Next we'll register the instances with the target group.
</p>

```bash
aws elbv2 register-targets --target-group-arn targetgroup-arn --targets Id=i-cloud-1-instance1234567890abcdef0 Id=i-cloud-1-db-instance1234567890abcdef0
```

<p>
Lastly we'll create a listener for the load balancer to forward requests to the target groups
</p>

```bash
aws elbv2 create-listener --load-balancer-arn loadbalancer-arn --protocol HTTP --port 80 --default-actions Type=forward,TargetGroupArn=targetgroup-arn
```

<p>
The output should contain the ARN of the listener. We can verify the health of the target group. 
</p>

```bash
aws elbv2 describe-target-health --target-group-arn targetgroup-arn
```

<hr />
<a href="wordpress.md">
&lt; Previous
</a>
|
<a href="auto_scaling.md" align="right">
Next &gt;
</a>