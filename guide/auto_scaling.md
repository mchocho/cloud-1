<h1>Step 6: Auto Scaling</h1>

<img src="https://i.imgur.com/ExBrcOw.jpeg" align="center" width="350px" height="230px" />

<p>
We're almost there. Our application is up and running with a load balancer to help distribute our incoming traffic. Next we will enable <a href="">auto scaling</a> for our EC2 incstance to ensure we have the correct number of instances available to handle the load for the application.
</p>

```bash
aws autoscaling create-auto-scaling-group --auto-scaling-group-name cloud-1 --max-size 5 --min-size 2 --desired-capacity 2 --instance-id i-0e69 --target-group-arns "arn:aws:elasticloadbalancing:region:123456789012:targetgroup/my-targets/1234567890123456"
```

<p>
And that's it. To verfify that our auto scaling group has launched run
</p>

```bash
aws autoscaling describe-auto-scaling-groups --auto-scaling-group-names cloud-1
```

<hr />
<a href="load_balance.md">
&lt; Previous
</a>
|
<a href="CDN.md" align="right">
Next &gt;
</a>