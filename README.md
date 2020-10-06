
# aws deploy
#### description : 
I do not plan on maintaining this playbook for everyone to use it, this is not the goal of the project. If know your way around AWS, I tried to make as easy as possible to use it. My goal is not to focus on the aws deployment but rather, keep my time for the chat server, the features and to make it usable for as many people as possible... that being said, feel free to use this playbook if you want.
#### requirements : 
- having ansible installed
- having an aws account
- owning a fully qualified domain
- having awscli installed locally on your machine for the user that will run the playbook
- having pre-existing resources in aws
  - a iam user with an ssh public key and appropriate permission to deploy ec2 instances and update route 53 records
  - a security group with port 22,80,443 to you, your friends or the whole world   
  - a hosted zone in route53   

#### notes :
- this playbook will automatically add the new deployed host to the inventory file staging/hosts so you can run the playbook temporary.chat.yaml without editing your inventory
- the aws_tag is also the fqdn of the server
#### usage example :
`ansible-playbook -e "aws_region=us-east-1 aws_vpc=vpc-23ebcf46 aws_subnet=subnet-1d6b1a6a aws_ami=ami-0dba2cb6798deb6d8 aws_instance_type=t2.nano aws_sg=sg-008a34845ce896322 aws_ssh_key=luciano aws_tag=temporary.chat local_ssh_key_path=/home/luciano/.ssh/id_rsa aws_route53_zoneid=Z04750303W271V39JV6OR env=staging" deploy_aws.yaml`


# temporary.chat
#### description : 
a playbook to deploy a chat server where you can generate random rooms (public or private, expert mode will come later.)
#### requirements : 
- having ansible installed
- having a ubuntu server 20.04 LTS with ssh access
- having port 22,80 and 443 open
- having a domain name? (I will try very hard to make this optional as the goal is to make this accessible to as many as possible.)
#### usage example :
`ansible-playbook -i staging -e '{have_fqdn:true}' -e "my_fqdn=temporary.chat" deploy_chat.yaml`

# aws destroy
#### usage example :
`ansible-playbook -e "aws_region=us-east-1 aws_tag=temporary.chat" destroy_aws.yaml`

# the (ambitious) goals

- decentralize communications (less facebook chats!)
- offer a free service that will remain free and ad free ( temporary.chat )
- offer a paying service with more options/storage/features ( permanent.chat )
- offer the possibility to anyone to roll out their own instance of "temporary.chat" for free (with a different domain or simply an ip?)
- create an api expert mode with end to end encryption managed by the user

# the roadmap (oh god!)

##### UI:
 - Icons to buttons (especially menu button) 
 - Each row in the conversation should be wrapped in an element (not using br) and styled
 - Preview file before uploading
##### APP:
- replace all hard coded instances of "temporary.chat" so it can be deployed with any fqdn
- create self signed certificate when the server is only accessible via ip (+ put the fingerprint and ip in the html main page?)
- make a hackish solution to use dynamic dns + let's encrypt? 
- create api for expert users that want to manage their encryption
- make the random chatrooms optional? (only one room (for people who may want it))
- support other OS (centos, openbsd to start with)
- add database backend for text 
- preview urls shared in the room
- fix javascript upload on firefox mobile
- notifications on android/iphone? is it even possible for website? 
