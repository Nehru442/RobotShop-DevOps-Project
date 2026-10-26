# Robot Shop on AWS EKS with Helm

A microservices e-commerce application (Stan's Robot Shop) deployed on **Amazon EKS** in `ap-south-1` (Mumbai) using **eksctl** and **Helm**, exposed to the internet through the **AWS Load Balancer Controller**.

> **Project type:** Hands-on learning project. The original application is [Instana Robot Shop](https://github.com/instana/robot-shop). The Helm chart and walkthrough are credited to [uniquesreedhar/RobotShop-Project](https://github.com/uniquesreedhar/RobotShop-Project). AWS resources were deleted after testing to avoid ongoing costs.

## Project Overview

Deployed and tested a microservices application on Amazon EKS, including the application services, data stores, and messaging components.

- **Kubernetes:** Amazon EKS
- **Region:** Asia Pacific (Mumbai) — `ap-south-1`
- **Cluster provisioning:** `eksctl`
- **Application deployment:** Helm
- **External access:** AWS Load Balancer Controller and Kubernetes Ingress
- **Storage:** Amazon EBS CSI driver
- **Identity:** IAM OIDC provider and IAM roles for service accounts

## Architecture

```text
User Browser
     |
AWS Load Balancer
     |
Kubernetes Ingress
     |
Amazon EKS Cluster
     |
Robot Shop Microservices
     |
MongoDB | MySQL | Redis | RabbitMQ
```

## Implementation Steps

1. **Prerequisites:** Prepare AWS access and the required command-line tools.
2. **EKS cluster:** Create the cluster and managed node group using `eksctl`.
3. **IAM OIDC:** Associate an IAM OIDC provider with the cluster.
4. **AWS Load Balancer Controller:** Configure its IAM permissions and Helm deployment.
5. **EBS CSI driver:** Configure IAM permissions and the EKS add-on for persistent volumes.
6. **Helm deployment:** Deploy Robot Shop into the `robot-shop` namespace.
7. **Ingress configuration:** Expose the application through an AWS load balancer.
8. **Validation:** Verify the pods, services, ingress, storage, and application order flow.
9. **Cleanup:** Delete AWS resources after testing to avoid unnecessary costs.

## Repository Structure

```text
RobotShop-DevOps-Project/
├── EKS/
│   ├── 01-prerequisites.md
│   ├── 02-eks-cluster-setup.md
│   ├── 03-oidc-IAM.md
│   ├── 04-alb-configuration.md
│   ├── 05-ebs-csi-driver.md
│   └── helm/
│       ├── Chart.yaml
│       ├── README.md
│       ├── ingress.yaml
│       ├── values.yaml
│       └── templates/
├── README.md
└── LICENSE
```

*This is the intended project-focused structure; retain any additional application directories required by the Helm chart.*

## Challenges and Lessons Learned

- Selected suitable EC2 node sizes for application and Kubernetes system workloads.
- Configured IAM permissions for the AWS Load Balancer Controller and EBS CSI driver.
- Troubleshot shell command syntax and AWS CloudShell session expiration.
- Learned to validate Kubernetes workloads, ingress resources, and persistent volume claims.
- Identified cost and reliability improvements, including consolidating load balancers, enabling HTTPS, and improving database persistence.

## Security and Cost Considerations

- AWS resources were deleted after project testing.
- The sample application uses demo-oriented defaults and is not production-ready without additional security hardening.
- Production deployments should consider HTTPS, Kubernetes Secrets or an appropriate secrets manager, network policies, and durable database storage.

## Future Enhancements

- Provision AWS infrastructure using Terraform.
- Implement CI/CD using GitHub Actions.
- Explore GitOps with Argo CD.
- Add monitoring with Prometheus and Grafana.
- Configure HTTPS using AWS Certificate Manager.

## Credits

- Original application: [Instana Robot Shop](https://github.com/instana/robot-shop)
- Helm chart and walkthrough: [uniquesreedhar/RobotShop-Project](https://github.com/uniquesreedhar/RobotShop-Project)

This repository documents a learning project and the implementation steps performed during deployment.