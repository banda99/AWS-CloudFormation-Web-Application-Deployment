# CS4843 Assignment 2

## Infrastructure
### create.sh 
create.sh is a bash script used to create the stacks in cloudformation

### data.sh
data.sh is a bash script that creates the database stack in cloudformation

### database.yml & database2.yml
This creates the database instance thorugh the designated private subnet. They are labeled diffrently only by the the number two because they each create an instance using a specific private subnet group to be associated with the database stack. 

### servers.yml
This yaml file creates a Launch configuration with Auto-Scaling groups. WHen you create the auto scaling group that is associated with the imported names of the private subnets derived from the parameter file. Another security group is then created for the EIP, which is associated with the vpc created, with traffic control from port 80, to port 80. When the load balancer is created, a load balancer security is associated with it and the listener for the load balancer forwards the infomation. 

