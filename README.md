<div align="center">
   <h1>☁️ Cloud-1</h1>
   <h4>This subject will make you build your first simple cloud infrastructure.</h4>
</div>

## Table of Contents

- [Introduction](#introduction)
- [Schema](#schema)
- [Install](#install)
- [Getting started](#started)
- [Guide](#guide)
- [Documentation](#documentation)
- [Contributors](#contributors)

### `Introduction`

In this project you will have to install a simple wordpress website on a cloud infrastructure.
<br />

We will be using the Amazon AWS CLI to create an configure our website. This will be acheived using the <a href="https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/index.html">EC2</a>, <a href="https://awscli.amazonaws.com/v2/documentation/api/latest/reference/elbv2/index.html">elbv2</a>, <a href="https://awscli.amazonaws.com/v2/documentation/api/latest/reference/rds/index.html">rds</a>, and <a href="https://docs.aws.amazon.com/cli/latest/reference/autoscaling/index.html">autoscaling</a> commands.

### `Schema`

<img src="https://i.imgur.com/n1SIBM3.png" align="center" />

### `Install`

Download and install <a href="https://www.python.org/downloads/">Python</a>

* On Linux run

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

* On windows open your terminal as administrator and run

```bash
choco install awscli -y
```

### `Getting started`

In order to deploy our website with AWS services you'll need to <a href="https://portal.aws.amazon.com/gp/aws/developer/registration/index.html?nc2=h_ct&src=default">create an AWS root and IAM account</a>.
Copy your Access key ID and Secret Access key and store them safely on your machine.


### `Guide`

This guide is cut into six sections. By following these steps you will end up with a running scalable instance of a wordpress application.
You can <a href="./guide/iam.md">start here</a>

### `Documentation`

Some further notes are provided for the commands we'll use for this project

* <a href="#">IAM</a>
* <a href="#">EC2</a>
* <a href="#">RDS</a>
* <a href="#">elbv2</a>
* <a href="#">Autoscaling</a>

### `Contributors`

* <a href="https://github.com/PhethulwaziD">P. Donga</a>
* <a href="https://github.com/mnchabeleng">M. Nchabeleng</a>
* <a href="https://github.com/samofoke">S. Mofokeng</a>

<hr />
<a href="./guide/iam.md" align="right">
Next &gt;
</a>