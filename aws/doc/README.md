# Overview

AWS CloudFormation Servian Template Servian_Multi_AZ: Servian is a web-based application for TechChallenge. This template installs a highly-available, scalable servian deployment using a multi-az Amazon RDS database instance for storage. It demonstrates using the AWS CloudFormation bootstrap scripts to install the packages and files at instance launch time.

#Configuration

conf.toml is updated based on the AWS postgreSQL RDS instance created and hostname is updated accordingly.

Database username and password need to be pass as parameters within parameter json file.


#Resources

Following core resources are created as a part of stack.

- SecurityGroups for LoadBalancer, WEB & Database
- EC2 instances.
- AWs PostgreSQL Database (9.6.21)
- Classic Load balancer
- LaunchConfigurationName
- AutoScalingGroup


#Deployment Architecture

- Master git repo is pulled within stack as a part of userdata and extracted to EC2 instances.
- Golang packages gets deployed as a part of LaunchConfiguration. This is mainly to Demonstrate, that prerequisites for solution can be included and solution can be build.
- Conf.toml is transformed.
- Loadbalancer is created to allow public traffic on http port 80 and forward traffic to web instance on port 3000. LoadBalancer are      configured using 3 public availability zone for High availability.
- Target instances get created as a part of autoscaling group and register as targets for loadbalancer.
- Auto scaling group is created for Resiliency.
- PostgreSQL RDS database is created with master password supplied in parameter json file.
- Solution is build within instances using "go build".
- DB is updated with "-s" for RDS instance, and server start using serve in background.

# Future Improvements

- Customise Network stack using specific CIDR ranges instead of default VPC.
- CI pipeline to allow builds outside of AWS instances which triggers on git check ins.
- Trigger auto deployments if builds are successful.
- Application on HTTPS.
- Customise autoscaling policy and scale in and out based on IO stats.
