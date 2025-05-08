# Client Document Portal on AWS

> A secure cloud-native file sharing backend designed for client-facing teams using S3, IAM, CloudWatch and CloudTrail.

## 1. Overview

This project describes the infrastructure design for a secure and scalable document-sharing backend using AWS.

It suits small-to-medium businesses, such as accounting firms, consultancies, or legal practices, needing secure client document sharing. The goal is to provide stronger control, auditing capabilities and automation compared to services like Google Drive or Dropbox.

The focus is on **fine-grained access control**, **automated monitoring** and **system resilience** using AWS core services: **S3**, **IAM**, **CloudTrail** and **CloudWatch**. Additional services for extended functionality are optional.

This project does not include application code or frontend development. It demonstrates an infrastructure-only approach designed to scale according to evolving business needs.

## 2. Why Not Just Use Google Drive?

While Google Drive and Dropbox are sufficient for basic document sharing, growing businesses with sensitive or regulated information face limitations. Requirements evolve to include:

* **Advanced access control** tailored for individual clients
* **Detailed audit logs** of uploads, downloads and permission changes
* **Automation workflows** including tagging, virus scanning and upload notifications
* **Compliance capabilities** such as encryption, data residency, or retention policies
* **Easy scalability** for numerous clients and documents without manual management

AWS infrastructure addresses these limitations by providing advanced security, flexible automation and comprehensive monitoring.

---

## 3. Architecture Diagram

This project focuses solely on cloud infrastructure design. The following diagram outlines how AWS components integrate for secure file sharing between teams and clients.

> *Architecture diagram placeholder*

### Components Overview

* **S3 Bucket** – Stores documents organized by logical client prefixes (e.g. `clients/client123/`)
* **IAM Roles** – Defines permissions for staff, clients and administrators
* **CloudWatch** – Monitors activities and generates anomaly alerts
* **CloudTrail** – Records API calls for audit and compliance purposes
* *(Optional)* Lambda, SNS, Cognito, CloudFront for added functionality such as automation, notifications, authentication and improved performance

---

## 4. AWS Components

| Service                        | Purpose                                                     |
| ------------------------------ | ----------------------------------------------------------- |
| Amazon S3                      | Secure storage for client documents using structured paths  |
| AWS IAM                        | Role-based access management for various user groups        |
| S3 Bucket Policies             | Controls file-level access using path-based rules           |
| AWS CloudTrail                 | Records detailed API call history                           |
| Amazon CloudWatch              | Provides system monitoring, alerts and metrics tracking    |
| *AWS Lambda (optional)*        | *Enables serverless workflows (file scanning, tagging, etc.)* |
| *Amazon SNS (optional)*        | *Sends notifications about file uploads*                      |
| *Amazon Cognito (optional)*    | *Supports user authentication if adding a frontend*           |
| *Amazon CloudFront (optional)* | *Offers faster file delivery and enhanced security*           |

---

## 5. Security and Permissions

Security relies on IAM roles, S3 bucket policies and optionally pre-signed URLs for temporary file access.

### Roles and Permissions

| Role          | Permissions                                            |
| ------------- | ------------------------------------------------------ |
| Staff         | Upload and view files across all client folders        |
| Client        | Read-only access to files within their assigned folder |
| Administrator | Complete access to all files, logs and configurations |

### Example: S3 Bucket Policy for Client Access

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Client123ReadAccess",
      "Effect": "Allow",
      "Principal": {"AWS": "arn:aws:iam::123456789012:role/Client123Role"},
      "Action": ["s3:GetObject"],
      "Resource": "arn:aws:s3:::client-portal-bucket/clients/client123/*"
    }
  ]
}
```

---

## 6. Monitoring and Alerts

Monitoring and logging are critical for reliability and security.

### CloudWatch Metrics

* Tracking uploads and downloads
* Error rates and response times
* Alerts triggered by unusual activity patterns

### CloudTrail Logging

* Comprehensive logging of S3 API activities (who, when, what and from where)
* Logs stored separately for long-term auditing

### Optional Notifications

* Combining S3 Event Notifications with Lambda and SNS can:

  * Alert teams when files are uploaded
  * Enforce naming conventions or automatic file tagging

---

## 7. Optional Enhancements

The modular design easily allows enhancements as requirements evolve:

* **CloudFront Integration** – Faster global file access with added security
* **File Scanning via Lambda** – Antivirus or file validation upon uploads
* **Lifecycle Management** – Automatic archival or deletion of older files
* **Authentication via Cognito** – User login and identity management
* **Infrastructure as Code** – Reusable deployment with Terraform or CloudFormation

---

## 8. Learning Goals

This project helps build practical AWS skills by:

* Designing secure IAM roles and policies
* Implementing granular file access control in S3
* Utilizing CloudWatch and CloudTrail for monitoring and audit logging
* Making informed decisions about cloud-native solutions versus commercial software
* Clearly documenting and justifying infrastructure design choices

---

## 9. Demonstration

### Folder Structure Example

```
s3://client-docs-portal/
├── clients/
│   ├── client123/
│   ├── client456/
│   └── client789/
```

### Architecture Diagram

*\[diagram placeholder]*

---

## 10. Resources

### AWS Documentation

* [Amazon S3 Best Practices](https://docs.aws.amazon.com/AmazonS3/latest/userguide/best-practices.html)
* [IAM Policies and Permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html)
* [S3 Bucket Policy Examples](https://docs.aws.amazon.com/AmazonS3/latest/userguide/example-bucket-policies.html)
* [CloudWatch Overview](https://docs.aws.amazon.com/cloudwatch/)
* [CloudTrail Logging Guide](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-user-guide.html)

### Learning Links

* [AWS Cloud Practitioner Exam Guide](https://aws.amazon.com/certification/certified-cloud-practitioner/)
* [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/)
* [IAM Policy Simulator](https://policysim.aws.amazon.com/)
