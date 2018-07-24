# Anchore Engine Demo

## Overview

The included [Amazon Web Services](https://aws.amazon.com) (AWS) [CloudFormation](https://aws.amazon.com/cloudformation/) templates setup a 2-subnet Availability Zone (AZ) [Virtual Private Cloud](https://aws.amazon.com/vpc/) (VPC) in which a single instance [Elastic Container Service](https://aws.amazon.com/ecs/) (ECS) cluster is deployed. Along with the ECS cluster, a single PostgreSQL [Relational Database Service](https://aws.amazon.com/rds/) (RDS) instance is launched to support the Anchore Engine service itself.

The default RDS instance size (db.t2.micro) qualifies for the AWS Free Tier service; however the default ECS
instance size (t2.large) does not qualify.

### Let's Begin! Launch the CloudFormation Stack

1\. To begin this workshop, **click one of the 'Deploy to AWS' buttons below for the region you'd like to use**. This is the AWS region where you will launch resources for the duration of this workshop. This will open the CloudFormation template in the AWS Management Console for the region you select.

Region | Launch Template
------------ | -------------
**N. Virginia** (us-east-1) | [![Launch Anchore Engine Stack into Virginia with CloudFormation](/Images/deploy-to-aws.png)](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=anchore-engine-demo&templateURL=https://s3.amazonaws.com/anchore-engine-demo-us-east-1/master.yaml)
**N. California** (us-west-1) | [![Launch Anchore Engine Stack into California with CloudFormation](/Images/deploy-to-aws.png)](https://console.aws.amazon.com/cloudformation/home?region=us-west-1#/stacks/new?stackName=anchore-engine-demo&templateURL=https://s3-us-west-1.amazonaws.com/anchore-engine-demo-us-west-1/master.yaml)

*If you have CloudFormation launch FAILED issues, please try launching in us-east-1 (Virginia)*

2\. Once you have chosen a region and are inside the AWS CloudFormation Console, you should be on a screen titled "Select Template". We are providing CloudFormation with a template on your behalf, so click the blue **Next** button to proceed.

3\. On the following screen, "Specify Details", your Stack is pre-populated with the name "anchore-engine-demo". You can customize that to a name of your choice **less than 15 characters in length** or leave as is. For the parameters section, if you want to change the size of the RDS or ECS instances you may specify a different value for **RDSInstanceType** and/or **ECSInstanceType** respectively. If you want to specify different RDS values for database name, user or password you may specify a different values for **DatabaseName**, **DatabaseUsername** or **DatabasePassword**. Otherwise, leave them as default. The user launching the stack (you) must already have the necessary permissions. Click **Next**.

4\. On the "Options" page, leave the defaults and click **Next**.

5\. On the "Review" page, verify your selections, then scroll to the bottom and select the checkbox **I acknowledge that AWS CloudFormation might create IAM resources**. Then click **Create** to launch your stack.

6\. Your stack will take about 3 minutes to launch and you can track its progress in the "Events" tab. When it is done creating, the status will change to "CREATE_COMPLETE".

7\. Click the "Outputs" tab in CloudFormation and find the values for "AnchoreCliUrl", "AnchoreCliUser" and "AnchoreCliPass". These will be your environment variables for ANCHORE_CLI_URL, ANCHORE_CLI_USER and ANCHORE_CLI_PASS respectively for the anchore-cli utility. Leave this tab open so you can come back to it later if needed.

## Demo Cleanup

1\. Go to the CloudFormation console and find the Stack that you launched in the beginning of the demo, select it, and click **Delete Stack**.

* When the stack has been successfully deleted, it should no longer display in the list of Active stacks. If you run into any issues deleting stacks, contact [AWS Support](https://console.aws.amazon.com/support/home) for additional assistance.
