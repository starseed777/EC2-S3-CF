This is an AWS cloudformation template that deploys an EC2 instance, an IAM role and a policy for access to list and create buckets in s3 from ec2. Down below will be an in-depth explanation of what each block of code will deploy. Refer to cftest.txt file in this repo for confirmation this code does what it's supposed to do.


- Line 4-8: Starting off with some parameters, our first parameter is going to be a keypair for access into instances. Since this is being done in an automated fashion we will not be hard coding the keypair into code, therefore passing it in as a parameter is for automation purposes.

- Line 9-13: Referring to our existing VPC environment instead of deploying everything from scratch. 

- Line 14-18: Referring to our existing subnet that is already created as mentioned earlier this saves us time from deploying everything from scratch because we can just refer to our already set up VPC environment and configurations.

- Line 19-24: Instance type for ec2- in this case the default value will be t2.micro so we wont have to manually configure these instance configurations.

- Line 25-38: This is how we will ensure that an AMI ID appropriate to the region is specified in this case we have three AMI ID's of the same amazon linux ami but in different regions as shown us-east1, us-east2, us-west-1.

- Line 39-76: This is the deployment of an ec2 instance with its configurations as shown. We are making references to the logical ID's of our instance type, subnet, AMI, security group and tags for naming purposes. This is also where the IAM role will attach itself to the instance so we wont have to manually attach it after creation.

- Line 77-97: This is the creation of the security group for the instance being deployed, as shown it will open port 22 for ssh access to be able to log into the instance.

- Line 98-108: This is the instance profile for specifying which roles it can assume. As shown the role it will refer to is the s3 bucket role (which will be explained below)

- Line 109-131: Here we have the s3 bucket policy that will state the permissions of creating and listing buckets in s3.

- Line 132-152: The s3 bucket role - AWS services can assume a role to obtain temporary security credentials that can be used to make AWS API calls. The "sts:AssumeRole" is for a set of temporary security credentials that you can use to access AWS resources that you might not normally have access to. These temporary credentials consist of an access key ID, a secret access key, and a security token.

- Line 153-179: After stack creation in the cloudformation console we're just speeding up the process by getting the public ipv4 address and keyname necessary for writing out our ssh command to log into the instance that was created.