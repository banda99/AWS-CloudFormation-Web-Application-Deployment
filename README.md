# CS4843 Assignment 2
In assignment 2 we were asked to deploy a highly available web application using AWS CloudFormation by writing the code that creates and deploys the infrastructure. This is achieved by using a internet gateway  that allows us to connect and access a virtual private cloud  where traffic flows and is associated to an elastic load balancer and requests access oto the NAT's gateway entrances which contain the public subnets that grant you access to the private subnets where the web application is located.

## Infrastructure
### create.sh 
create.sh is a bash script used to create the stacks in cloudformation

### data.sh
data.sh is a bash script that creates the database stack in cloudformation

### database.yml & database2.yml
This creates the database instance thorugh the designated private subnet. They are labeled diffrently only by the the number two because they each create an instance using a specific private subnet group to be associated with the database stack. In the parameter section, a database instance identifier is used to associate the identifier with a name with the rules "[a-zA-Z][a-zA-z0-9]*". Similiar to the instance identifier the DatabaseName parameter and the DatabaseUser(MaxLength 16, MinLength1) parameter follows the same naming rules. Next, the DatabasePassword follows a similiar set of rules as those mentioned prior with the minimum kength requierment being 8 and the maximum being 64. The MultiAZDatabase creates a Multi-AZ MySQL database instance. The database subnet group is created and associate dwiht the two private subnets that were created when network.yml was run. Last, the database is finally created with the values of the parameters. 

### servers.yml
This yaml file creates a Launch configuration with Auto-Scaling groups. When you create the auto scaling group that is associated with the imported names of the private subnets derived from the parameter file. Another security group is then created for the EIP, which is associated with the vpc created, with traffic control from port 80, to port 80. When the load balancer is created, a load balancer security is associated with it and the listener for the load balancer forwards the infomation.

### serv.json
This file contains the parameters that are referenced in servers.yml including the EvvironmentName, the key, and the ami.

### network.yml
This file creates a vpc, public and private subnets which are spread out over two availability zones. Elastic Ip's are allocated to NAT Gateways. Each NAT gateway has its own public subnet. When the public route table is created, it is associated with the default route 0.0.0.0/0 . Next, private Route tables are created and associated with the public subnets. 

###net-param.json
This file contains the parameters for network,yml which include the EvironmentName, the VPC's cidr, and the 2 public and 2 private subnets IP's
