# Self-service ETL Reference architecture

This reference architecture creates an AWS Service Catalog Portfolio called "Service Catalog Containers Reference Architecture"  
The Portfolio provides 3 products which will create a full DevOps deployment pipeline from code to container deployment in Fargate.  

### Create the portfolio using the Launchstack: 
[![CreateStack](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/#/stacks/new?stackName=SC-RA-ECS-Portfolio&templateURL=https://arcdemo2020.s3-ap-southeast-2.amazonaws.com/sc-code/ecs/sc-portfolio-ecs.json)  

1. Once above is finished, go to [Service Catalog](https://ap-southeast-2.console.aws.amazon.com/servicecatalog/) in AWS console
2. Click your login dropdown box, choose [Switch Role](https://signin.aws.amazon.com/switchrole)
3. Input your AWS AccountID, and `ServiceCatalogEndusers` as your Role
4. Launch product `1-ETL Cluster` without change any settings. Wait for couple of minutes until the provision is completed.
5. Launch product `2-Arc Jupyter Service`, no change on settings, wait until the provision is done.
6. Finally, launch product `3-Arc Job Service`, wait until the provision is done.

### Install from your own S3 bucket:
1. clone this git repo:  
  ```git clone git@github.com:melodyyangaws/aws-service-catalog-reference-architectures.git```  
2. Copy everything in the repo to your S3 bucket:  
  ```cd aws-service-catalog-reference-architectures```  
  ```aws s3 cp . s3://[YOUR-BUCKET-NAME-HERE] --exclude "*" --include "*.json" --include "*.yml" --recursive```  
3. In the AWS [CloudFormation console](https://console.aws.amazon.com/cloudformation) choose "Create Stack" and supply the Portfolio S3 url:  
  ```https://s3.amazonaws.com/[YOUR-BUCKET-NAME-HERE]/ecs/sc-portfolio-ecs.json```  
5. Set the _LinkedRole1_ and _LinkedRole2_ parameters to any additional end user roles you may want to link to the Portfolio.
6. Set the _CreateEndUsers_ parameter to No if you have already run a Portfolio stack from this repo (ServiceCatalogEndusers already exists).
7. Change the _RepoRootURL_ parameter to your bucket's root url:  
  ```https://s3.amazonaws.com/[YOUR-BUCKET-NAME-HERE]/``` 

