cloudformation_training
=======================

CloudFormation Training class

This repository contains cloudformation to boot a small synchronous CRUD applicaiton.  

The objective of the lab is to improve upon the templates. 

These templates will boot a VPC with a Public facing ELB that passes traffic to a AutoScaling group running Java Application under Tomcat. 
A Internal ELB will be used for the application to connect to a MySQL Database Master, another instance will be booted as a slave and will monitor the health of the Master and will run a failover if the Master enters a state where it is unreachable.

If you've finished the lab and everything creates, Test the app by visiting the Sync ELB URL and append :8080/intuit-multi-tier-sync-app/sync/cities. 
This URL will return a sting of cities in JSON.
