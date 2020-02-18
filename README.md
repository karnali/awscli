# Python version 3 check 
Note: Python3 breaks backwards compatibility

Edit and add ~/.bash_profile and source ~/.bash_profile	
```
$ nano ~/.bash_profile  
alias python='/usr/local/bin/python3'
```
Check python version and path
```
$ python --version
Python 3.7.3
```
```
$ which python3
/usr/local/bin/python3
```
# install python version 3
```
$ brew install python
```

# awscli: Install AWS CLI Version 2. 
Using the macOS command line. Make sure you are sudo.
```
$ curl "https://awscli.amazonaws.com/AWSCLIV2.pkg" -o "AWSCLIV2.pkg"
$ sudo installer -pkg ./AWSCLIV2.pkg -target /

$ which aws
/usr/local/bin/aws

$ aws --version
aws-cli/2.0.0 Python/3.7.4 Darwin/18.7.0 botocore/2.0.0dev4
```

# Configure AWSCLI.  
Make sure you create these in AWS IAM first.

```
$ aws configure
AWS Access Key ID [None]: A******************W
AWS Secret Access Key [None]: m******************Yg
Default region name [None]: us-east-1
Default output format [None]: json
```

# You will see those cred. file created here.
```
$ cd /Users/jsmith/.aws
```

# Check if aws cli is working.
```
$ aws s3 ls
```

# Optional: Add this aws shortcuts 
Add below code at the end of your ~/.bash_profile file then source ~/.bash_profile.    
Just type helpaws.

```
$ nano ~/.bash_profile
```
```
#### helpaws alias #### 
function helpaws()
{
echo "******************************************************************************"
echo "*  helpaws alias - aws cli helpaws menu.                                     *"
echo "******************************************************************************"
echo "* 1. aws-list-s3                                  - Lists all s3 buckets.    *"
echo "* 2. aws-list-ec2                                 - Lists all ec2 instances. *"
echo "* 3. aws-list-vol                                 - Lists all disk volumes.  *"
echo "* 4. aws-list-snap                                - Lists all snapshots.     *"
echo "* 5. aws-describe-ec2                             - Describe ec2 instance.   *"
echo "* 6. aws-stop-ec2                                 - Stop ec2 instance.       *"
echo "* 7. aws-start-ec2                                - Start ec2 instance.      *"
echo "* 8. aws-terminate-ec2                            - Terminate ec2 instance.  *"
echo "***********************s3 commands.*******************************************"
echo "* aws s3 ls s3://bucket-name                      - List content of bucket.  *"
echo "* aws s3 ls s3://bucket-name/path/                - List content bucket path *"
echo "* aws s3 rb s3://bucket-name                      - Delete bucket            *"
echo "* aws s3 rb s3://bucket-name --force              - Force delete bucket.     *"
echo "* aws s3 rm s3://my-bucket/path/file.txt          - Delete file              *"
echo "* aws s3 rm s3://my-bucket/path --recursive       - Delete all contents.     *"
echo "* aws s3 cp /Users/jsmith/file.txt s3://my-bucket/path/                      *"
echo "******************************************************************************"
}

#### List all aws ec2 #### 
function aws-list-ec2() 
{
aws ec2 describe-instances --query 'Reservations[].Instances[].{AZ:Placement.AvailabilityZone,InstanceId:InstanceId,Name:Tags[?Key==`Name`]|							
[0].Value,BStatus:State.Name,IPPriv:PrivateIpAddress,PublicIP:PublicIpAddress,Type:InstanceType,XKey:KeyName}' --output table
}

####  List all aws volume #### 
function aws-list-vol() 
{
aws ec2 describe-volumes --query 'Volumes[*].[VolumeId, Attachments[0].InstanceId, AvailabilityZone, Size, FakeKey, State, VolumeType, Encrypted, Tags[?Key==`Name`] | [0].Value]' --output table
}

####  List all aws snapshots #### 
function aws-list-snap() 
{
aws ec2 describe-snapshots --owner-ids 265197127965 --query 'Snapshots[*].[SnapshotId, VolumeSize, FakeKey, State, VolumeId, Progress, Tags[?Key==`Name`] | [0].Value]' --output table
}

#### aws describe ec2 instance #### 
function aws-describe-ec2() 
{
aws ec2 describe-instances --query 'Reservations[].Instances[].{InstanceId:InstanceId,PrivateIP:PrivateIpAddress,Name:Tags[?Key==`Name`]|[0].Value,Status:State.Name}' --output table
echo To describe ec2, enter InstanceId from above table:
read instanceid
aws ec2 describe-instances --instance-ids $instanceid
}

####  stop aws ec2 instance #### 
function aws-stop-ec2() 
{
aws ec2 describe-instances --query 'Reservations[].Instances[].{InstanceId:InstanceId,PrivateIP:PrivateIpAddress,Name:Tags[?Key==`Name`]|[0].Value,Status:State.Name}' --output table
echo To stop ec2, enter InstanceId from above table:
read instanceid
aws ec2 stop-instances --instance-ids $instanceid
}

####  start aws ec2 instance #### 
function aws-start-ec2() 
{
aws ec2 describe-instances --query 'Reservations[].Instances[].{InstanceId:InstanceId,PrivateIP:PrivateIpAddress,Name:Tags[?Key==`Name`]|[0].Value,Status:State.Name}' --output table
echo To start ec2, enter InstanceId from above table:
read instanceid
aws ec2 start-instances --instance-ids $instanceid
}

####  terminate aws ec2 instance #### 
function aws-terminate-ec2() 
{
aws ec2 describe-instances --query 'Reservations[].Instances[].{InstanceId:InstanceId,PrivateIP:PrivateIpAddress,Name:Tags[?Key==`Name`]|[0].Value,Status:State.Name}' --output table
echo To terminate ec2, enter InstanceId from above table:
read instanceid
aws ec2 terminate-instances --instance-ids $instanceid
}

#### lsit s3 #### 
function aws-list-s3() 
{
aws s3 ls
}
```

# Uninstall awscli
```
$ which aws
/usr/local/bin/aws

$ ls -l /usr/local/bin/aws
lrwxrwxrwx 1 ec2-user ec2-user 49 Oct 22 09:49 /usr/local/bin/aws -> /usr/local/aws-cli/aws

$ sudo rm /usr/local/bin/aws
$ sudo rm /usr/local/bin/aws_completer
$ sudo rm -rf /usr/local/aws-cli
```
