# Git repo

https://github.com/chintan-parmar/TechChallengeApp

Branch: servian_aws

#Prerequisites setup

1. Clone Git Repo to your local

2. Download and setup AWS CLI with your preferred region.
 - Make sure your IAM access has admin privileges for TechchallengeAPP purpose

3. Create & Download AWS keypair that will used to create instances in your preferred AWS region.

https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html

4. OPTIONAL - Create Default VPC (Network stack) if not available

  - check if VPC is Available
# Command:
   aws ec2 describe-vpcs --region ap-southeast-2

  - Create Vpc (Default network stack for TechChallenge)

#  Command:
  aws ec2 create-default-vpc --region ap-southeast-2



# Create and setup TechChallenge via AWS cloudformation (Infrastructure as Code)  

1. Navigate to "aws" Directory within your local repo

2. Create Stack

- Update parameter file (servian.parameters.asg.json) with the keypair name previously created. Setup postgreSQL database username and password.

#Command

aws cloudformation create-stack --stack-name Servian --template-body file://servian.json --parameters file://servian.parameters.asg.json --region ap-southeast-2

- Monitor cloudformation stack creation from AWS console

- Once stack is completed check the outbputs tab to view the loadblancer PUBLIC URL.

- Monitor Loadbalancer target to become healthy. Takes about 10 mins after stack is completed.

3. Cleanup Stack

# Command

aws cloudformation delete-stack --stack-name Servian
