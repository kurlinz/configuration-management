# configuration-management

Ansible is written in python, so ansible also needs python to run and for some customer functionality you can write them in python which could be an advange. we can see python was also fetched during installation.


1. install ansible on the host machine

![Screenshot 2023-06-03 at 6 53 13 PM](https://github.com/kurlinz/configuration-management/assets/123019485/a97b263e-31ed-4220-83b2-3e651974d816)


3. check version
![Screenshot 2023-06-03 at 6 54 33 PM](https://github.com/kurlinz/configuration-management/assets/123019485/2f40f8df-40dc-4b96-9d64-0a52be00b83c)

5.  Provision the linux service to be configured on aws
* showing the instance typr, AMI ID, 
* SOURCE amazon/ubuntu/images/hvm-ssd/ubuntu-jammy-22.04-amd64-server-20230516
* DESCRIPTION Canonical, Ubuntu, 22.04 LTS, amd64 jammy image build on 2023-05-16
* DNS NAME ec2-54-74-236-227.eu-west-1.compute.amazonaws.com
* create key and change permission to "400"


7.  create a git repository
  
9.  pull repository into local machine, cd into the repository
  
11.  create a host file
12.  connect ansible to the server
13.  add server information to local machine to get rid of interractive confirmation to connect
* ssh-keyscan -H 54.74.236.227 >> ~/.ssh/known_hosts
local host machine public keyn ia already registered in server from key genaration during creation 

Or we can disbale the ssh key check all together. most preferably for ephemeral infrastructure ( servers that are dynamically created and destroyed)

