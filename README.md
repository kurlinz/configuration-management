# Recruitmemt Assignment: Configuration Management

## TASK 2: Configure a linux Machine with ansible

1. Prepare a linux machine
2. Create a playbook which do the following
   - Each new user should have a script called nice-script.sh in their home directory (hint: use "skeleton directory"). The script should list all mounted filesystems.
     - Create the script with the correct command (locally).
     - Copy the script to the remote machine into the correct directory

   - Creates a user with:
     - Username: john
     - Home: /better-place/john (create /better-place before if needed) User ID: 1234
   - User john should be able to run the following command with sudo without a need to provide his password: whoami
   - Install packages:
     - Tmux
     - vim
   - Install Terraform CLI 

## STEPS
1. install ansible on the host machine, and confirm version
2. Provision the linux service to be configured on aws
3. Configure ansible to connect to server ( Create hosts file)
4. Create playbook
5. Run Playbook and push to git repository

## Requirements
1. VS code
2. AWS account
3. Github Account

## Step 1. install ansible on the host machine

![Screenshot 2023-06-04 at 3 02 08 PM](https://github.com/kurlinz/python-app/assets/123019485/6ba0158d-a747-4fa0-b903-cac919a92843)

### check version
![Screenshot 2023-06-03 at 6 54 33 PM](https://github.com/kurlinz/configuration-management/assets/123019485/2f40f8df-40dc-4b96-9d64-0a52be00b83c)

Ansible is written in python, so ansible also needs python to run and for some customer functionality you can write them in python which could be an advange. we can see python was also fetched during installation.

## Step 2: Provision the linux service to be configured on aws

In cases where we would be required to provision more than one infrastructure, an infrastructure as code (IAC) is always ideal, but since we are working with just one server it is quicker to provision through the AWS UI.

Provisioning an EC2 instance through AWS console is qucik fast and easy.

1. First we login to the AWS console, navigate to EC2 instances and just pick from the list shown, for this project we would be using and Ubuntu Linux server of 
   - virtual server type "t2.micro"
   - AMI "ami-01dd271720c1ba44f"
   - Public DNS name "ec2-54-154-131-8.eu-west-1.compute.amazonaws.com"
   - Public IP "54.154.131.8"

![Screenshot 2023-06-04 at 2 31 25 PM](https://github.com/kurlinz/python-app/assets/123019485/29629608-4b4e-4b4a-b706-e67f6e8f9d7a)

The server is provisioned on a default VPC in "eu-west-1" region, a an already defined security group which just allows ssh connection on port 22.
i would be using an already existing key to connect to the server.

Public DNS name
![Screenshot 2023-06-04 at 3 07 27 PM](https://github.com/kurlinz/python-app/assets/123019485/22556386-c9f6-4ce1-9723-62d96e32aa4d)

## Step 3: Configure ansible to connect to server ( Create hosts file)
We create the hosts file which tells ansible which and how to connect to the remote server.

We create a directory and cd into the directory.
```
    mkdir configuration-management
    cd configuration-management
 ```
inside this directory we would be creating all other needed files.

* Open Visual studio code and create the file named "hosts"

* Inside the file we specify the target server, which can use either the IP address or the DNS host name, either eould work. Provide the path to the private key in our host machine for ansible to connect to the server and the user name. I would be grouping the instance and Variable for easy reusability and incase more needs to be added anytime.

![Screenshot 2023-06-04 at 3 31 02 PM](https://github.com/kurlinz/python-app/assets/123019485/244f539b-0ec1-4493-81ed-af971e210e48)

To test the connection, we ping the server
```
    ansible ec2 -i hosts -m ping
```

![Screenshot 2023-06-04 at 3 35 25 PM](https://github.com/kurlinz/python-app/assets/123019485/f26a9166-2a12-4350-b923-69aa3b2170a1)

We can remove the connection check if we dealing with large numbers of servers and can't be confirming "yes for all of them.
* we can add server information to local machine to get rid of interractive confirmation to connect and vice versa
```
  ssh-keyscan -H 54.74.236.227 >> ~/.ssh/known_hosts
```
* we can disbale the ssh key check all together, most preferably for ephemeral infrastructure ( servers that are dynamically created and destroyed), create ansible config file in **~/.ansible.cfg** or working directory and set **host_key_checking = false** on the host machine for a large number of infrastructure


## Step 4: Create playbook

Ansible requires minimum of 2 files, a host file and at least one play book.

We create the play book **my-playbook.yaml** and the shell script file **nice-script.sh** that list all mounted filesystems in the configuraton-management directory.
![Screenshot 2023-06-04 at 3 59 30 PM](https://github.com/kurlinz/python-app/assets/123019485/725799ef-3590-4ee2-9a2a-ae672c562a3e)

After creating playbook which can be referenced in the repository, we simply run with the cmd
```
      ansible-playbook -i hosts my-playbook.yaml
```
![Screenshot 2023-06-04 at 4 02 38 PM](https://github.com/kurlinz/python-app/assets/123019485/8a658e80-12dd-4d1c-8bc8-4103509ef2c3)

The playbbok was successful!!!

All Files pushed to git repository.












