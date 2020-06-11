# Self-service ETL Reference Architecture

This reference architecture creates an AWS Service Catalog Portfolio called "Self-service ETL Reference Architecture"  
The Portfolio provides 3 products which will create a full DevOps deployment pipeline from code to ETL pipeline deployment in serverless Fargate.  

### Create the portfolio using the Launchstack with default settings: 
[![CreateStack](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/#/stacks/new?stackName=SC-RA-ECS-Portfolio&templateURL=https://arcdemo2020.s3-ap-southeast-2.amazonaws.com/sc-code/ecs/sc-portfolio-ecs.json)  

1. Once finished, go to [Service Catalog](https://ap-southeast-2.console.aws.amazon.com/servicecatalog/) in your AWS console.
2. Click your login dropdown box, choose [Switch Role](https://signin.aws.amazon.com/switchrole)
3. Input your AWS AccountID, and `ServiceCatalogEndusers` as your Role
4. Launch the product `1-ETL Cluster` with default. Wait until the provision is done. Please ignore a warning message 'A stack name already exists', proceed with the new stack name given by the system.
5. Launch the product `2-Arc Jupyter Service` with default parameters, except the `DataLakeS3Bucket`. Replace it by an existing S3 bucket name in your account. Wait until the provision is done. 
6. Open the notebook URL produced by your Jupyter service. Upload the sample Arc ETL job [SCD Type2 Workshop](app-code/job/) and run each stage of the job.
6. Finally, launch the product `3-Arc Job Service`  and wait until the provision is done. 
7. Follow the instruction in the Jupyter notebook, download it then upload to an S3 bucket `jobtrigger-xxx`. It will trigger an Arc job execution, based on the file drop event.

### Install from your own S3 bucket:
1. clone this git repo:  
  ```git clone git@github.com:melodyyangaws/aws-service-catalog-reference-architectures.git```  
2. Copy everything in the repo to your S3 bucket:  
  ```cd aws-service-catalog-reference-architectures```  
  ```aws s3 cp . s3://[YOUR-BUCKET-NAME-HERE] --exclude "*" --include "*.json" --include "*.yml" --include "*.zip" --recursive```  
3. In the AWS [CloudFormation console](https://console.aws.amazon.com/cloudformation) choose "Create Stack" and supply the Portfolio S3 url:  
  ```https://s3.amazonaws.com/[YOUR-BUCKET-NAME-HERE]/ecs/sc-portfolio-ecs.json```  
5. Set the _LinkedRole1_ and _LinkedRole2_ parameters to any additional end user roles you may want to link to the Portfolio. It must be an existing IAM role in the current account.
6. Set the _CreateEndUsers_ parameter to No if you have already run a Portfolio stack from this repo (ServiceCatalogEndusers already exists).
7. Change the _RepoRootURL_ parameter to your bucket's root url:  
  ```https://s3.amazonaws.com/[YOUR-BUCKET-NAME-HERE]/``` 

