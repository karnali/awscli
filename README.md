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
