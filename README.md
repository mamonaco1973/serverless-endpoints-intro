# Serverless HTTP Endpoint - AWS Lambdas, Azure Functions and GCP Cloud Functions

This video series complements the [Scaling in the Cloud](https://github.com/mamonaco1973/cloud-scaling-intro/blob/main/README.md) project. In that series, we deployed a simple microservice using Python and the Flask framework.

In this series, we will deploy Python-based serverless functions in **AWS**, **Azure**, and **GCP**. These are referred to as *Flask-like* or *flasky* throughout the project documentation. The goal is to deploy an identical API from the Cloud Scaling series using the native serverless features of each cloud provider.

By the end of this series, you will learn how to deploy simple Python-based HTTP endpoints as serverless functions across all three major cloud platforms using Terraform.

We will walk through the following tasks:

1. **Deploy Python Code** for microservices using serverless technologies:
   - **Lambdas** for AWS
   - **Azure Functions** for Azure
   - **Cloud Functions** for GCP

2. **Use a document database** for microservice data storage:
   - **DynamoDB** for AWS
   - **CosmosDB** for Azure
   - **Firestore** for GCP

3. **Configure HTTP endpoints** to invoke the serverless code:
   - **API Gateway** for AWS
   - **Function App** for Azure
   - **Cloud Run** for GCP

4. **Secure the HTTP endpoints**:
   - **IAM Integration** for AWS
   - **Function Keys** for Azure
   - **Simple OIDC** for GCP

5. **Clean up resources** by destroying all infrastructure created during the process.
   
## Introduction to Scaling

AWS Auto Scaling, Azure Virtual Machine Scale Sets (VMSS), and Google Cloud Managed Instance Groups (MIGs) are cloud-native solutions designed to ensure scalability, fault tolerance, and efficiency for virtual machine workloads. They share the core purpose of automatically adjusting the number of virtual machines to meet demand.

**AWS Auto Scaling** excels in its deep integration with the AWS ecosystem, providing granular control over scaling policies and seamless compatibility with services like CloudWatch and Elastic Load Balancer. It supports dynamic scaling based on metrics, scheduled scaling, and predictive scaling, making it ideal for highly variable workloads, batch processing, and multi-region failover solutions. Auto-healing capabilities ensure instances are replaced automatically when issues arise, and configurations are defined using Launch Templates or Launch Configurations.

**Azure VM Scale Sets** are designed for enterprise-grade applications, particularly in environments already leveraging Azure's extensive suite of tools. They simplify the scaling and management of VMs, offering easy integration with Azure Load Balancer, Application Gateway, and Traffic Manager. Azure VMSS also supports advanced features like rolling upgrades and fault domain management, ensuring high availability. 

Google Cloud **Managed Instance Groups** provide a streamlined, globally scalable solution that integrates seamlessly with GCP’s innovative services like Cloud Monitoring and HTTP(S) Load Balancers. MIGs are particularly well-suited for distributed applications and microservices architectures, offering straightforward configuration and strong support for regional and global deployments. With features like automatic health checking, rolling updates, and support for preemptible VMs, GCP MIGs cater to modern, cost-sensitive cloud-native applications.

[Detailed Feature Comparison](./Comparison.md)

## *Flasky* Endpoint Summary

- [AWS Source Code](https://github.com/mamonaco1973/aws-flasky-lambdas/tree/main/01-lambdas/code)
- [Azure Source Code](https://github.com/mamonaco1973/azure-flasky-function-app/blob/main/02-flasky/function_app.py)
- [GCP Source Code](https://github.com/mamonaco1973/gcp-flasky-cloud-functions/blob/main/01-cloudfunctions/code/main.py)

### `/gtg` (GET)
- **Purpose**: Health check.
- **Response**: 
  - `{"connected": "true", "instance-id": <instance_id>}` (if `details` query parameter is provided).
  - 200 OK with no body otherwise.

### `/candidate/<name>` (GET)
- **Purpose**: Retrieve a candidate by name.
- **Response**: 
  - Candidate details (JSON) with status `200`.
  - `"Not Found"` with status `404` if no candidate is found.

### `/candidate/<name>` (POST)
- **Purpose**: Add or update a candidate by name.
- **Response**: 
  - `{"CandidateName": <name>}` with status `200`.
  - `"Unable to update"` with status `500` on failure.

### `/candidates` (GET)
- **Purpose**: Retrieve all candidates.
- **Response**: 
  - List of candidates (JSON) with status `200`.
  - `"Not Found"` with status `404` if no candidates exist.

## AWS Solution

![AWS diagram](aws-flask-asg.png)

## Azure Solution

![AWS diagram](azure-flask-vmss.png)

## GCP Solution

![AWS diagram](gcp-flask-mig.png)
