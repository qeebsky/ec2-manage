# ec2-manage

## System requirements
 - Java 1.6 or higher
 - [Amazon EC2 API Tools](http://s3.amazonaws.com/ec2-downloads/ec2-api-tools.zip)

## Configurations
```sh
$ unzip ec2-api-tools.zip
$ ln -s ec2-api-tools-[version]/ ec2-api-tools
$ cat > ec2-api-tools.conf <<EOF
export AWS_ACCESS_KEY="[your AWS access key]"
export AWS_SECRET_KEY="[your AWS seret key]"
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_112.jdk/Contents/Home/jre
export EC2_AMITOOL_HOME=[path to]/ec2-api-tools
export EC2_HOME=[path to]/ec2-api-tools
export EC2_URL="https://ec2.us-west-1.amazonaws.com"
export EC2_REGION="us-west-1"
export EC2_DEFAULT_AMI="ami-af1afbeb"
export EC2_DEFAULT_TYPE="t2.nano"
export EC2_DEFAULT_SECURITY_GROUP="[your default security group]"
export EC2_DEFAULT_KEY_NAME="[your default key name]"
EOF
$ chmod u+x bin/*
```
Set JAVA_HOME environment and so on.

## Usage
### Check instances
```sh
$ bin/ec2_check_instances
[RESERVATION] r-06b6bc09cf43cxxxx 65600820xxxx
[INSTANCE] i-0b26d2b4486fdxxxx ami-af1afbeb ec2-xx-xx-xx-xxx.us-west-1.compute.amazonaws.com ip-172-31-11-246.us-west-1.compute.internal running [key name] 0 t2.nano 2018-01-01T12:34:56+0000 us-west-1a monitoring-disabled xx.xx.xx.xx 172.31.11.246 vpc-9266xxxx subnet-9b77xxxx ebs hvm xen 927f8fbc-a226-4a35-badf-d429ff49xxxx [security group] default false BLOCKDEVICE /dev/sda1 vol-097a58848e7e7xxxx 2018-03-25T03:08:34.000Z true NIC eni-f6afxxxx subnet-9b77xxxx vpc-9266xxxx 65600820xxxx in-use 172.31.11.246 ip-172-31-11-246.us-west-1.compute.internal true NICATTACHMENT eni-attach-ca62xxxx 0 attached 2018-01-01T12:34:56+0900 true NICASSOCIATION xx.xx.xx.xx amazon 172.31.11.246 GROUP [security group] PRIVATEIPADDRESS 172.31.11.246 ip-172-31-11-246.us-west-1.compute.internal ec2-xx-xx-xx-xx.us-west-1.compute.amazonaws.com
```
If instance(s) are already running, Instance information is shown.

### Create new EC2 instance
```sh
$ bin/ec2_start_instances
- starting launch instance
RESERVATION	r-06b6bc09cf43cxxxx	65600820xxxx
INSTANCE	i-0b26d2b4486fdxxxx	ami-af1afbeb		ip-172-31-11-246.us-west-1.compute.internal	pending	[key name]	0		t2.nano	2018-01-01T12:34:56+0000	us-west-1a				monitoring-disabled		172.31.11.246	vpc-9266xxxx	subnet-9b77xxxx	ebs				hvm	xen	927f8fbc-a226-4a35-badf-d429ff49xxxx	[security group]	default	false
NIC	eni-f6afxxxx	subnet-9b77xxxx	vpc-9266xxxx	65600820xxxx	in-use	172.31.11.246	ip-172-31-11-246.us-west-1.compute.internal	true
NICATTACHMENT	eni-attach-ca62xxxx	0	attaching	2018-01-01T12:34:56+0900	true
GROUP	[security group]
PRIVATEIPADDRESS	172.31.11.246	ip-172-31-11-246.us-west-1.compute.internal
- waiting ready ec2 instance....
[INSTANCE] i-0b26d2b4486fdxxxx
[IP ADDRESS] xx.xx.xx.xx
```
will be shown new instance information.  
Login with "ec2-user" account to server instance as normally.

### Stop instance
```sh
$ bin/ec2_stop_instance
instance ID: i-0b26d2b4486fdxxxx # input target Instance ID
INSTANCE	i-0b26d2b4486fdxxxx	running	stopping
```
will stop instance.

### Terminate instance
```sh
$ bin/ec2_terminate_instance
instance ID: i-0b26d2b4486fdxxxx # input target Instance ID
INSTANCE	i-0b26d2b4486fdxxxx	stopped	terminated
```
will terminate instance.
