cloudformation_training
=======================

CloudFormation Training class

This repository contains cloudformation to boot a small synchronous CRUD applicaiton.  

The objective of the lab is to improve upon the templates. 

These templates will boot a VPC with a Public facing ELB that passes traffic to a AutoScaling group running Java Application under Tomcat. 
A Internal ELB will be used for the application to connect to a MySQL Database Master, another instance will be booted as a slave and will monitor the health of the Master and will run a failover if the Master enters a state where it is unreachable.


To boot this environment, Upload the json files to a S3 bucket:  (Remember to replace my_uniq_bucket_name with your bucket name)
`
aws s3 cp Nest.json s3://my_uniq_bucket_name/Nest.json
aws s3 cp Network.json s3://my_uniq_bucket_name/Network.json
aws s3 cp App.json s3://my_uniq_bucket_name/App.json
aws s3 cp DB.json s3://my_uniq_bucket_name/DB.json
`
Then call create stack on the nested template providing parameters to all of the other templates and to a KeyPair you have access to. 
Again don't forget to replace my_uniq_bucket_name with your own bucket.
`
aws cloudformation create-stack --stack-name MyNestedStack1 --template-url https://s3.amazonaws.com/my_uniq_bucket_name/Nest.json \
--parameters \ 
ParameterKey=NetworkCFNURL,ParameterValue=https://s3.amazonaws.com/my_uniq_bucket_name/Network.json \ 
ParameterKey=AppCFNURL,ParameterValue=https://s3.amazonaws.com/my_uniq_bucket_name/App.json \ 
ParameterKey=DatabaseCFNURL,ParameterValue=https://s3.amazonaws.com/my_uniq_bucket_name/DB.json \
ParameterKey=KeyPair,ParameterValue=MyKeyPair \
--capabilities CAPABILITY_IAM
`
If you've finished the lab and everything creates, Test the app by visiting the Sync ELB URL and append :8080/intuit-multi-tier-sync-app/sync/cities. 
This URL will return a sting of cities in JSON.
