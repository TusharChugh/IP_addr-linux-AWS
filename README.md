# IP_addr-linux-AWS
The code spits the IP address of the device (Rpi/dragonboard running linux) to the dynamoDB on AWS. This is quite helpful when running the device in the headless mode or when HDMI cable/monitor is not available

#Steps involved

#Create a table on AWS Dynamo db
1. Create AWS account if you don't have one. Go to https://console.aws.amazon.com/dynamodb/ and click on create table
2. Fill following items (with your values) 
  a. Table name: devicesinfo
  b. Primary partition key: deviceid (Number)
  c. Primary sort key	ipaddr (String)

#Get AWS credentials
1. Go to AWS IAM: https://console.aws.amazon.com/iam/
2. Create new user
3. Go to security credentials tab -> create access key 
4. Note down/save the credentials

#Configure AWS on hardware
1. <pre>sudo apt-get install python-pip</pre>
2. <pre>$pip install boto3</pre>
3. <pre>$pip install awscli</pre>
4. <pre>$sudo aws configure</pre> and use the credentials (from above steps)

#Get and running the code
1. Clone the code
