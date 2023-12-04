# Guidance for Telco observability on AWS

The Guidance for Telco observabiklity on AWS creates 3 Amazon CloudWatch Dashboards at different levels to allow the visualization of the traffic and metrics for telco customers.

All the dashboards use customer widgets that allow you to navigate from one level to the next.

## Table of Content

1. [Overview](#overview)
2. [Prerequisites](#prerequisites)
3. [Deployment Steps](#deployment-steps)
4. [Deployment Validation](#deployment-validation)
5. [Running the Guidance](#running-the-guidance)
6. [Next Steps](#next-steps)
7. [Cleanup](#cleanup)


## Overview

While there are traditional IT/DevOps focused uses cases are solved by traditional Observability use cases, this solution is designed to address Observability in the Telecom industry which naturally happens to have high-cardinality metrics involved due to the very nature of the vast number of hardware devices, endpoints, services and software involved.

![](/assets/RA.png)

## Prerequisites

These deployment instructions include a lambda function that generates the metrics the Amazon CloudWatch dashboard consumes. You can change the input to your CloudWatch Dashboards for your own following the format included in the sample.

## Deployment Steps

1. Download the [demo.yaml](./source/demo.yaml) AWS CloudFormation template from the source folder or clone the repo using the command: 

```bash
git clone https://github.com/aws-solutions-library-samples/guidance-for-telco-observability-on-aws.git
```

2. Open the file and **replace** '<accountId>' with the account ID you are going to deploy the solution through the template (total 13 occurances). Save the updated file.

2. Sign in AWS Console and open [CloudFormation console](https://us-east-1.console.aws.amazon.com/cloudformation/home) (This defaults to us-east-1, but select the region you want to deploy your solution to)

3. Select “Create Stack” and then select “With new resources (standard)”

4. In the “Specify template” option, select “Upload a template file”. Select “Choose file” and select the above saved CloudFormation template.

5. Give the stack a name, for example: *telco-kpi-dashboard-sample*. Select “Next” until the confirmation page.

6. **Acknowledge** the checkbox in bottom left. And Click Submit

7. Wait for the stack to complete its deployment. It will take a few minutes.

## Deployment Validation

1. Once the stack is deployed, navigate to the resources tab in the Cloudformation stack. Find the AWS Lambda function **“EMFLambda”** and open it. Invoke the function a few times to generate data into your CloudWatchDashboard.

> This initial trigger will let the setup have initial data as later EventBridge will be triggering this Lambda function periodically every 5 minutes. This Lambda function simply logs the application logs in EMF format.

2. Once Data is generated, go back to the resources tab in your CloudFormation Stack, and open Level 1 Dashboard: “USA-Telcom-demo”.

> In order to see the widget, you will need to allow the widget to run on the left side of the screen.


## Next Steps

To use these dashboards for your telcom network, send your logs directly to Amazon CloudWatch in the EMF Format, and the the dashboards will consume and display the information for you.

You can replicate and extend these dashboards based on your needs and requirements.


## Cleanup

- Delete the AWS CloudFormation Stack deployed, and all the resources will be deleted.
- Delete the /aws/lambda/EMFLambda Amazon CloudWatch Log Group.

## Notices

*Customers are responsible for making their own independent assessment of the information in this Guidance. This Guidance: (a) is for informational purposes only, (b) represents AWS current product offerings and practices, which are subject to change without notice, and (c) does not create any commitments or assurances from AWS and its affiliates, suppliers or licensors. AWS products or services are provided “as is” without warranties, representations, or conditions of any kind, whether express or implied. AWS responsibilities and liabilities to its customers are controlled by AWS agreements, and this Guidance is not part of, nor does it modify, any agreement between AWS and its customers.*


