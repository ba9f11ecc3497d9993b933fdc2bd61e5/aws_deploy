# aws_deploy
deploy ec2 to an existing aws account and update dns in an existing route53 zone

# deploy_aws.yaml 
##### Overview :
an ansible playbook to deploy an ec2 instance in aws and update route 53 
- I do not plan on maintaining this playbook for everyone to use it, this is not the goal of the project. If know your way around AWS, I tried to make as easy as possible to use it. My goal is not to focus on the aws deployment but rather, keep my time for the chat server, the features and to make it usable for as many people as possible... that being said, feel free to use this playbook if you want.
##### requirements : 
- having ansible installed
- having an aws account
- owning a fully qualified domain
- having awscli installed locally on your machine for the user that will run the playbook
- having pre-existing resources in aws
  - a iam user with an ssh public key and appropriate permission to deploy ec2 instances and update route 53 records
  - a security group with port 22,80,443 to you, your friends or the whole world   
  - a hosted zone in route53   

##### notes :
- this playbook will automatically add the new deployed host to the inventory file staging/hosts so you can run the playbook temporary.chat.yaml without editing your inventory
- the aws_tag will also the fqdn of the server in route53
##### usage example :
`ansible-playbook -e "aws_region=us-east-1 aws_vpc=vpc-23ebcf46 aws_subnet=subnet-1d6b1a6a aws_ami=ami-0dba2cb6798deb6d8 aws_instance_type=t2.nano aws_sg=sg-008a34845ce896322 aws_ssh_key=luciano aws_tag=temporary.chat local_ssh_key_path=/home/luciano/.ssh/id_rsa aws_route53_zoneid=Z04750303W271V39JV6OR env=staging" deploy_aws.yaml`

# destroy_aws.yaml
##### description :
an ansible playbook to destroy an ec2 instance based on name tag. 
- I do not plan on maintaining this playbook for everyone to use it, this is not the goal of the project. If know your way around AWS, I tried to make as easy as possible to use it. My goal is not to focus on the aws deployment but rather, keep my time for the chat server, the features and to make it usable for as many people as possible... that being said, feel free to use this playbook if you want.
##### usage example :
`ansible-playbook -e "aws_region=us-east-1 aws_tag=temporary.chat" destroy_aws.yaml`


