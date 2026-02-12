# ☁️ AWS EC2 CLI Study Guide (Beginner → Practical)

This document explains how to create and manage **AWS EC2 instances using AWS CLI**.  
It is designed for learning, revision, and real-world DevOps preparation.

---

# 📌 1. What is AWS EC2?

Amazon EC2 (Elastic Compute Cloud) provides:
- Virtual servers in the cloud
- Scalable compute power
- Pay-as-you-go infrastructure

You can use EC2 for:
- Hosting web apps
- Running backend servers
- Testing environments
- DevOps automation
- CI/CD pipelines

---

# 📌 2. What is AWS CLI?

AWS CLI allows you to:
- Manage AWS services using terminal
- Automate infrastructure
- Integrate with scripts
- Build Infrastructure as Code workflows

---

# 🛠 3. Configure AWS CLI

## 🔹 Step 1: Configure Credentials
```bash
aws configure
```

You will enter:
- Access Key
- Secret Key
- Region
- Output format

---

## 🔹 Step 2: Verify Login
```bash
aws sts get-caller-identity
```

✅ Confirms that AWS CLI is authenticated.

---

# 🔑 4. Create Key Pair

Key pair is used to securely SSH into EC2.

```bash
aws ec2 create-key-pair \
--key-name vockey \
--query 'KeyMaterial' \
--output text > vockey.pem
```

---

## 🔹 Set Proper Permission
```bash
chmod 400 vockey.pem
```

Required for SSH security.

---

# 🧱 5. Get Latest Ubuntu AMI

AMI = Amazon Machine Image  
It is the OS template used for instance creation.

```bash
aws ec2 describe-images \
--owners 099720109477 \
--filters "Name=name,Values=ubuntu/images/hvm-ssd-gp3/ubuntu-noble-24.04-amd64-server-*" \
"Name=state,Values=available" \
--query 'reverse(sort_by(Images, &CreationDate))[0].ImageId' \
--output text
```

✅ Returns latest Ubuntu AMI ID.

---

# 🔐 6. Create Security Group

Security group works like firewall rules.

```bash
aws ec2 create-security-group \
--group-name ubuntu-sg \
--description "Ubuntu SG"
```

---

## 🔹 Allow SSH Access
```bash
aws ec2 authorize-security-group-ingress \
--group-name ubuntu-sg \
--protocol tcp \
--port 22 \
--cidr YOUR_IP/32
```

⚠ Always restrict SSH to your IP for security.

---

# 🚀 7. Launch EC2 Instance

```bash
aws ec2 run-instances \
--image-id ami-XXXXXXXX \
--instance-type t3.micro \
--key-name vockey \
--security-groups ubuntu-sg \
--associate-public-ip-address \
--tag-specifications "ResourceType=instance,Tags=[{Key=Name,Value=Ubuntu-CLI-VM},{Key=Env,Value=DEV}]"
```

---

# 🌐 8. Get Public IP Address

```bash
aws ec2 describe-instances \
--query "Reservations[*].Instances[*].PublicIpAddress" \
--output text
```

---

# 🔐 9. SSH Into Instance

```bash
ssh -i vockey.pem ubuntu@PUBLIC_IP
```

---

# 🔄 10. Instance Lifecycle Management

## 🔹 Stop Instance
```bash
aws ec2 stop-instances --instance-ids INSTANCE_ID
```

---

## 🔹 Start Instance
```bash
aws ec2 start-instances --instance-ids INSTANCE_ID
```

---

## 🔹 Terminate Instance
```bash
aws ec2 terminate-instances --instance-ids INSTANCE_ID
```

⚠ Termination permanently deletes instance.

---

# 🧠 11. Understanding Key Concepts

## 🔹 AMI
Template containing:
- OS
- Software
- Configurations

---

## 🔹 Security Groups
Acts like firewall:
- Controls inbound/outbound traffic
- Attached to instances

---

## 🔹 Key Pair
Used for:
- Secure SSH login
- Instance authentication

---

## 🔹 Instance Types
Example:
- t3.micro → Free tier / lightweight
- t3.medium → Moderate workloads
- c-series → Compute optimized

---

# 🧪 12. Real Practice Workflow

### Full Flow

1. Configure AWS CLI
2. Create key pair
3. Fetch AMI
4. Create security group
5. Launch instance
6. SSH into instance
7. Manage lifecycle

---

# ⚠️ Common Mistakes

❌ Forgetting chmod 400 for key  
❌ Opening SSH to entire internet  
❌ Using wrong AMI ID  
❌ Forgetting instance cleanup (cost risk)  
❌ Not tagging resources  

---

# 💰 Cost Awareness

Always terminate unused instances.

AWS charges for:
- Running instances
- Storage volumes
- Public IP usage

---

# 🔍 13. Useful AWS CLI Extras

## 🔹 Wait Until Instance Running
```bash
aws ec2 wait instance-running --instance-ids INSTANCE_ID
```

---

## 🔹 List Instances
```bash
aws ec2 describe-instances
```

---

## 🔹 Filter Instances by Tag
```bash
aws ec2 describe-instances \
--filters "Name=tag:Env,Values=DEV"
```

---

# 🔐 14. Security Best Practices

✅ Restrict SSH by IP  
✅ Use IAM roles instead of access keys  
✅ Rotate credentials regularly  
✅ Never upload `.pem` files to GitHub  
✅ Use environment variables for secrets  

---

# 🚀 15. DevOps Real-World Use Cases

EC2 CLI is used in:

- CI/CD deployment scripts
- Infrastructure automation
- Container hosting
- Microservices backend hosting
- Load testing environments

---

# 📚 16. Suggested Next Learning Topics

To go deeper in AWS + DevOps:

### Must Learn
- IAM roles & policies
- VPC & networking
- Elastic IP
- Auto Scaling
- Load Balancers
- CloudWatch monitoring

---

### Advanced DevOps Stack
- Terraform
- Docker + EC2
- GitHub Actions deployment
- Kubernetes

---

# 🧪 17. Mini Assignment (Team Practice)

Try creating script:

```
setup-ec2.sh
```

Script should:
- Create key pair
- Create security group
- Launch EC2
- Print Public IP
- SSH automatically

---

# 📌 18. Why Learn AWS CLI?

Because:

- Industry DevOps standard
- Automation friendly
- Faster than AWS Console
- Required for production deployments

---

# ✨ Summary

This guide covered:

- AWS CLI setup
- EC2 creation workflow
- Security groups
- Instance lifecycle
- Real-world best practices
- DevOps usage

---

Happy Cloud Learning ☁️🚀
