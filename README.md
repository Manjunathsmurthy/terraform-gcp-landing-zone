# GCP Landing Zone with Terraform

## Overview
Production-ready Terraform modules for Google Cloud Platform enterprise landing zones. Built on 13+ years of multi-cloud experience managing 500+ resources with 99.9% uptime.

## Key Achievements
- **99.9% Uptime**: Multi-region GCP deployments
- **30-40% Cost Savings**: Committed Use Discounts & resource optimization
- **500+ Resources**: Enterprise-scale GCP infrastructure
- **Zero Trust**: Cloud Identity, IAM, VPC Service Controls

## Core Modules

### Organization & Folders
```hcl
module "org_structure" {
  source = "./modules/organization"
  org_id = var.organization_id
  folders = {
    prod = "Production"
    dev  = "Development"
    shared = "Shared Services"
  }
}
```

### VPC Networks
```hcl
module "vpc_prod" {
  source = "./modules/vpc"
  project_id = var.project_id
  network_name = "prod-vpc"
  subnets = [
    {
      name = "prod-subnet"
      ip_cidr_range = "10.0.0.0/24"
      region = "us-central1"
    }
  ]
  enable_flow_logs = true
}
```

### GKE Clusters
```hcl
module "gke" {
  source = "./modules/gke"
  cluster_name = "prod-gke"
  location = "us-central1"
  node_pools = [
    {
      name = "default-pool"
      machine_type = "n1-standard-2"
      min_count = 2
      max_count = 10
    }
  ]
  enable_binary_authorization = true
}
```

### Cloud Armor Security
```hcl
module "cloud_armor" {
  source = "./modules/cloud-armor"
  security_policy = {
    name = "prod-policy"
    rules = [
      {
        priority = 1000
        action = "deny(403)"
        preview = false
        match = {
          versioned_expr = "SRC_IPS_V1"
          config = {
            src_ip_ranges = ["0.0.0.0/0"]
          }
        }
      }
    ]
  }
}
```

## Real-World Examples

### Financial Services
- **Challenge**: PCI-DSS compliant GCP infrastructure
- **Solution**: VPC Service Controls, Cloud Armor, DLP API
- **Result**: 99.95% uptime, passed audit

### E-Commerce Platform
- **Challenge**: Handle 10x traffic spikes
- **Solution**: Auto-scaling GKE, Cloud CDN, Load Balancer
- **Result**: <200ms latency globally

## Security Best Practices
- VPC Service Controls for data exfiltration prevention
- Binary Authorization for container signing
- Cloud Armor for DDoS protection
- Secret Manager for credentials
- Cloud KMS for encryption keys
- Security Command Center monitoring

## Professional Experience
13+ years in cloud architecture:
- Fortune 500 clients across industries
- 500+ cloud resources managed
- 99.9% uptime SLAs
- 30-40% cost optimization

## Contact
📧 [LinkedIn](https://www.linkedin.com/in/manjunaths-murthy/) for consulting

## License
MIT License

---
⭐ Star if helpful!
