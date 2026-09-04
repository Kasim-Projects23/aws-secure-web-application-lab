# AWS Secure Web Application Lab

## Overview

This project is a hands-on AWS environment designed and deployed to demonstrate cloud infrastructure, networking, security, identity and monitoring.

The infrastructure was initially built through the AWS Management Console, with each component configured and tested individually. The project focuses on how the different AWS services work together, how the environment is secured, and how the configuration is validated.

## Architecture

```text
                           Internet
                              |
                              v
                      Internet Gateway
                              |
                              v
                    VPC: 10.0.0.0/16
                              |
                              v
                 Public Subnet: 10.0.1.0/24
                              |
                              v
                    EC2 Linux Web Server
                       |              |
                       |              |
                       v              v
                  IAM Role        CloudWatch
                       |
                       v
               Private S3 Bucket
                       |
                       v
              Application Asset
```

## Architecture Scope

The environment is built around a single EC2 instance in a public subnet, providing a clear view of how the core AWS components connect and work together.

The architecture is intentionally scoped for this lab rather than designed for high availability or large-scale workloads. A production environment would typically use private subnets, multiple Availability Zones, load balancing, Auto Scaling, HTTPS/TLS, and more extensive monitoring and logging.

This approach keeps the focus on the underlying AWS infrastructure while still allowing the architecture to be extended as additional requirements are introduced.

## Infrastructure

| Component        | Configuration                 |
| ---------------- | ----------------------------- |
| Region           | Europe (London) – `eu-west-2` |
| VPC              | `10.0.0.0/16`                 |
| Subnet           | `10.0.1.0/24` public subnet   |
| Internet Gateway | `My-Lab-IGW`                  |
| Route Table      | `My-Lab-RouteTable`           |
| Security Group   | `My-Lab-SecurityGroup`        |
| EC2              | Amazon Linux 2023, `t3.micro` |
| Web Server       | Nginx                         |
| Storage          | Amazon S3                     |
| Identity         | EC2 IAM Role                  |
| Monitoring       | Amazon CloudWatch             |

## Security

Security controls were applied across the environment.

* SSH access is restricted to my public IP address.
* HTTP access is permitted on port 80 for the web server.
* The S3 bucket has Block Public Access enabled.
* S3 Object Ownership is configured with bucket owner enforced.
* S3 versioning is enabled.
* Server-side encryption uses SSE-S3.
* The EC2 instance uses an IAM role rather than long-term AWS credentials.
* The IAM policy follows least-privilege principles by restricting access to the specific S3 object required by the workload.

A negative IAM test was also performed to confirm that the EC2 instance could access the permitted object but could not perform an operation outside the policy, such as listing the bucket.

## Testing

The environment was validated throughout the deployment.

Testing included:

* EC2 instance status checks
* SSH connectivity
* Nginx service status
* HTTP access to the web application
* EC2 IAM role verification
* Successful S3 object access
* Denied S3 bucket listing
* S3 encryption and versioning verification
* AWS resource and configuration checks

Detailed testing evidence and screenshots are available in the project documentation.

## Documentation

Detailed configuration, screenshots and testing notes are available in:

* [Networking](documentation/networking.md)
* [EC2 Web Server](documentation/ec2.md)
* [S3](documentation/s3.md)
* [IAM and Least Privilege](documentation/iam.md)
* [CloudWatch Monitoring](documentation/monitoring.md)

## Skills Demonstrated

* AWS cloud infrastructure
* VPC and subnet design
* CIDR addressing
* Route tables and Internet Gateways
* Security Groups
* Amazon EC2
* Linux administration
* Nginx
* Amazon S3
* IAM and least privilege
* Workload identity
* CloudWatch
* Infrastructure troubleshooting
* Security testing
* Cost awareness
* Technical documentation

## Future Improvements

Potential extensions to the environment include:

* Terraform-based infrastructure
* Private application subnets
* Application Load Balancer
* Auto Scaling and multi-AZ deployment
* HTTPS/TLS
* Containerisation
* Kubernetes/EKS
* Expanded monitoring, logging and alerting

## Conclusion

The project demonstrates an AWS environment spanning networking, compute, storage, identity and monitoring, with security and operational considerations incorporated throughout.

The architecture provides a foundation that can be expanded towards a more resilient and production-oriented cloud environment as additional requirements are introduced.
