<h1>Step 4: Putting it all together</h1>

<p>
Now that our required instances are running and sentinal, <a href="https://aws.amazon.com/getting-started/hands-on/deploy-wordpress-with-amazon-rds/4/">it's time to run wordpress</a>.
<br />
Let's start off with an SSH into our EC2 instance:
</p>

```bash
aws ec2 describe-instances 		#grab the public DNS name

ssh -i cloud-1-key-pair.pem ec2-user@<<PUBLIC_DNS_NAME>>
```

<p>
Then we'll download and install mysql.
</p>

```bash
sudo su

yum install mysql -y
```

<p>
Setup your MySQL hostname to the RDS ip address.
</p>

```bash
aws rds describe-db-instances	#Find your RDS IP

export MYSQL_HOST=<<enpoint>> 	#replace <<enpoint>> with your RDS IP
```

<p>
Next we'll setup the credentials for our DB.
</p>

```bash
mysql --user=admin --password=farewell42WTC wordpress
```

<p>
Now that we're connected to the DB, we'll create a database for our application.
</p>

```bash
CREATE USER 'wordpress' IDENTIFIED BY 'wordpress-pass';
GRANT ALL PRIVILEGES ON wordpress.* TO wordpress;
FLUSH PRIVILEGES;
Exit
```

<p>
Now, let's install and run apache.
</p>

```bash
yum install httpd -y

service httpd start
```

<p>
Use the describe-instances command from earlier to get your EC2 Public DNS (IPv4) address and enter it in your browser.
<br />
Next we will <a href="https://aws.amazon.com/getting-started/hands-on/deploy-wordpress-with-amazon-rds/5/">download and configure WordPress</a>.

```bash
wget https://wordpress.org/latest.tar.gz

tar -xzf latest.tar.gz

cd wordpress

cp wp-config-sample.php wp-config.php
```

<p>
Open the wp-config.php file with a text editor.
</p>

```bash
vim wp-config.php

* DB_NAME: wordpress
* DB_USER: admin
* DB_PASSWORD: farewell42WTC
* DB_HOST: <<DB HOSTNAME>>
```
<p>
We can also <a href="https://api.wordpress.org/secret-key/1.1/salt/">generate unique keys and salts for the authentication process with this link</a>.
<br />
Next we will deploy WordPress.
</p>

```bash
sudo yum install -y httpd24 php72 mysql57-server php72-mysqlnd

cp -r wordpress/* /var/www/html/

service httpd restart

chkconfig httpd on

chkconfig --list httpd #httpd should be on in runlevels 2, 3, 4, and 5
```

<p>
If you see the WordPress welcome page, that means the installation was successful.
</p>

<hr />
<a href="rds.md">
&lt; Previous
</a>
|
<a href="load_balancer.md" align="right">
Next &gt;
</a>