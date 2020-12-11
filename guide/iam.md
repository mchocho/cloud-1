<h1>Step 1: Who is IAM?</h1>

<p>
AWS identity and access management (IAM) is a web service that helps you control who is authenticated and authorized to use permissions. In order to deploy our website with AWS services you'll need to <a href="https://portal.aws.amazon.com/gp/aws/developer/registration/index.html?nc2=h_ct&src=default">create an AWS root and IAM account</a>.
</p>

<p>
After you've created your account copy your Access key ID and Secret Acces key and store them safely on your machine. Open your terminal and run
</p>

```bash
aws configure

# AWS Access Key ID []: <<Enter your access key ID>>
# AWS Secret Access Key []: <<Enter your secret access key>>
# Default region name []: us-east-2
# Default output format []: json
```
<p>
Every instance we create, stop, or destroy using the CLI will be in the name of our IAM profile.
</p>

<hr />
<a href="../">
&lt; Previous
</a>

<a href="ec2.md" align="right">
Next &gt;
</a>
