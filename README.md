# IP_addr-linux-AWS
The code spits the IP address of the device (Rpi/dragonboard running linux) to the dynamoDB on AWS. This is quite helpful when running the device in the headless mode or when HDMI cable/monitor is not available.

The ipaws.py uses wlan0 (wifi) and a special number for USB-ethernet device. You can change this in the code if you have a different ethernet adaptor (wifi should work as is though)

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
2. <pre>pip install boto3</pre>
3. <pre>pip install awscli</pre>
4. <pre>sudo aws configure</pre> and use the credentials (from above steps)

#Get and running the code
1. Clone the code
   <pre>git clone https://github.com/TusharChugh/IP_addr-linux-AWS.git</pre>
2. Change the path of the ipaws.py file in ip_aws script (currently it is /home/linaro/Desktop/IP_addr-linux-AWS/)
3. Paste the ipaws script in /etc/network/if-up.d/
   <pre>cp ipaws /etc/network/if-up.d/</pre>
4. Give the required permissions to run the script when the network restarts
  <pre>chmod +x ipaws</pre>

#Test the code
1. In /etc/network/if-up.d/. 
   <pre>sh ipaws</pre>
2. You should see an entry in the device info table on dynamoDB
3. If it worked, then try restarting the board and see if that works as well
4. Congratulations, you are done!
