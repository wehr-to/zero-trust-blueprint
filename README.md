# 🛡️ Zero Trust Blueprint

This repository simulates a modern Zero Trust architecture across identity, device posture, network segmentation, access control, and telemetry. Through labs, Terraform examples, and policy walkthroughs, it demonstrates what it means to enforce security **without relying on implicit trust, at any layer**.

## 🎯 Why This Repo?

Most environments still operate on perimeter-based assumptions. This project flips that model and walks through how to:

- Enforce identity- and context-aware access
- Validate device posture before granting access
- Isolate workloads with granular network segmentation
- Log and verify every access request and action

## 🧱 What's Covered

| Area                     | Description                                                                 |
|--------------------------|-----------------------------------------------------------------------------|
| `identity-layer/`        | MFA, SSO, IAM role assumptions, conditional access policies                 |
| `device-posture/`        | Managed vs BYOD device checks, EDR simulations, posture signals             |
| `network-segmentation/`  | NACLs vs SGs, subnet-level isolation, lateral movement simulation           |
| `access-control/`        | RBAC vs ABAC models, just-in-time access provisioning                       |
| `telemetry-and-detection/` | Identity-aware logging, audit baselines, log forwarding to SIEM          |
| `labs-and-scenarios/`    | Breach response workflows, vendor access cases, least privilege drills      |
| `case-studies/`          | Real-world breakdowns of ZT implementations and migration strategies        |

## 🧪 Example Lab: Just-in-Time Access for Vendors

- Identity-based condition grants temporary access to scoped resource
- Access restricted based on device posture and IAM tag
- Role session automatically expires after X minutes
- All actions logged and exported to SIEM

## 🔧 Sample Terraform: Network Boundary Rule

```hcl
resource "aws_security_group" "zt_web_sg" {
  name        = "zt-web-sg"
  description = "Allow HTTPS only from approved CIDRs"

  ingress {
    from_port   = 443
    to_port     = 443
    protocol    = "tcp"
    cidr_blocks = ["10.0.0.0/16"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}
