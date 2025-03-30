#Create VPC
Under the region where you choose to create your vertual private cloud give it a name tag for future refference
Assign ipv4 address
Create 2 Subnets under your VPC
Create route table under the subnets
Configure Internet getway for routetable to access your resources and set them to target under the same VPC
#Create Database instance 
Under amazon aurora and RDS database service select database image to create database under same VPC.
Choose mariadb 10.6 or more for this project.
set inbound and outbound rule after creating security groups
Edit security group in action button and add rules to allow custom ports via internat gateway.
Allow port 3306 and port 80 to access database via ec2 instance.

This is how you connect to ec2 instance you will create later and access database via this ec2 instance
#create EC2 instance
Under the same vpc and subnets create ec2 instance with the existing security group or create securirty group and edit inbound rules .
Create Load balancer from load balancer section under same vpc as before, which you need to create ec2 instance under the same ELB.
#Create EC2 instance under the same ELB under VPC in the region you opted to create vpc where mariadb database instance located .
Using Ubuntu:
# EC2 instance Configuration
Select the ubuntu image in the region for which you have opted for VPC subnets and internet gateway and Elastic Load Balancer
#Allow Custoom ports for http and https access: port 80 and port 443 and port 22 for ssh.(You can allow other ports and redirect there using proxy in Nginx.
Go to security group-> Actions edit invound and outbound rules add rules the choose http, https, ssh and set custom allow ip 0.0.0.0/0
#connect databse instance to ec2 instace to access databases under the db instance .
To do so Go to Connected compute Resources -> Actions -> Setup Ec2 Connections.
#configure database access by allowing specific ip's in security groups of db instance under load balance in your vpc.
In EC2 instance inbound rules allow port 3306, port 80, port 443 etc set allow access from anywhere in the begining to avoid conflicts while connecting Database.

Go to Elastic IP and create one elastic IP and associate that to EC2 instance
#install mariaDb server in ec2 instance
in order to access databse in db instance install mariaDB server in your ec2 instance.
Use SSH to connect to your EC2 instance or connect directly via connect option in UI if you have select allow ip from anywhee.

 Then update Package repository:
 
 `sudo apt update -y  # For Ubuntu`

 Install mariadb with under command

 `sudo apt install -y mariadb-server`

 Then start maria db service by;
```
 sudo systemctl start mariadb
 sudo systemctl enable mariadb
```
 Then Secure mariaDB installation via:

 `sudo mariadb_secure_installation`

Then verify installation:
`sudo su -`

 `mariadb -u root -p`

 The terminal will prompt you to enter the password for the root user that you set during the mysql_secure_installation step.
 Once entered correctly, you should be logged into the MariaDB shell, ready to execute SQL queries.

 #connect to mariadb instance created earlier

 to do so command in the given below format
`sudo su -`
 `mariadb -h url-to-your-mariadb-resource -P 3306 -u name-od-database -p`
 it will prompt you for password
 Enter the password you created during creation of mariadb database.
 then it will open the mariadb server in terminal to run query in mariadb database under amazon aurora rds.

 #run querys to create database 
 create database db-name;
 choose db-name;
 it will select the databse you created recently with the name you provided.
 then run the sceema you are provided in this project and add some rows to specific tables like admin, users, 
 games(trx,wingo, 5d, k3) and point_list in order to access the admin user and running the project successfully.
 then set params in mariadb server to run events and procedures.

 #configure Nodejs and FTP to run this project in various way you know or follow under guide to do so.
 # Node Hello World

Simple node.js app that servers "Cloudscape"

Great for testing simple deployments on Cloud

## Step 1: Install NodeJS and NPM using nvm
Install node version manager (nvm) by typing the following at the command line.

```bash
sudo su -
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash
```
Activate nvm by typing the following at the command line.

```bash
. ~/.nvm/nvm.sh
```

Use nvm to install the latest version of Node.js by typing the following at the command line.

```bash
nvm install node
```

Test that node and npm are installed and running correctly by typing the following at the terminal:

```bash
node -v
npm -v
```

## Step 2: Install Git and clone repository from GitHub
To install git, run below commands in the terminal window:

```bash
sudo apt-get update -y
sudo apt-get install git -y
```

Just to verify if system has git installed or not, please run below command in terminal:
```bash
git — version
```

This command will print the git version in the terminal.

Run below command to clone the code repository from Github:

```bash
git clone https://github.com/iamcrypto/cloudscape.git
```

Get inside the directory and Install Packages

```bash
cd cloudscape
npm install
```
Then set environmental variable in .env
To Do so run;
vim .env after changing directory to project directory: Here Cloudscape

add there env variables and press Escape to exit.
Then press ":" and "wq"for write and quit. 

it will take you to the terminal.
Then go to project directory

Start the application
To start the application, run the below command in the terminal:
 you must set the server port to be 80.
```bash
npm start
```
To check the Deployment:
open the url to ELB in any browsers address Bar.


 
 











