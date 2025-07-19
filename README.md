
```markdown
# 🌐 Terraform AWS Medicare Infrastructure

A production-ready **Infrastructure as Code (IaC)** project using **Terraform** to provision scalable AWS infrastructure for the **MediCare web application**. This setup includes **VPC**, **EC2**, **S3**, and remote state management using **S3 + DynamoDB**.

---

---

## 🚀 Features

- ✅ Modular Terraform structure (VPC, EC2, S3)
- ✅ Remote state management with S3 & DynamoDB locking
- ✅ EC2 instance provisioned with `nginx` via `remote-exec`
- ✅ Public & private subnets with routing tables
- ✅ Secure infrastructure practices
- ✅ Compatible with AWS Free Tier

---

## 🧩 Terraform Modules

| Module | Description                            |
|--------|----------------------------------------|
| `vpc`  | Creates VPC, public subnets, and routes |
| `ec2`  | Provisions EC2 with SSH + NGINX         |
| `s3`   | Creates S3 bucket for app or state      |

---

## 🔧 Usage

### 1. ✅ Initialize

```bash
cd terraform/dev
terraform init
````

### 2. 🔍 Preview Changes

```bash
terraform plan
```

### 3. 🚀 Apply Infrastructure

```bash
terraform apply
```

### 4. 🧨 Destroy Resources

```bash
terraform destroy
```

---

## 🔐 Security Notes

* The `.pem` key is **not committed** to the repository.
* Add it to `.gitignore`:

  ```
  *.pem
  *.tfstate
  .terraform/
  ```

---

## 🗃️ Remote Backend Setup

Before using this infrastructure, ensure your **S3 bucket** and **DynamoDB table** for state locking exist.

### Example:

```hcl
resource "aws_s3_bucket" "tf_state" {
  bucket = "medicare-terraform-state-bucket"
  acl    = "private"
  versioning {
    enabled = true
  }
}

resource "aws_dynamodb_table" "tf_lock" {
  name         = "terraform-lock-table"
  billing_mode = "PAY_PER_REQUEST"
  hash_key     = "LockID"
  attribute {
    name = "LockID"
    type = "S"
  }
}
```

---

## 🌍 Outputs

```hcl
output "vpc_id" {
  value = module.vpc.vpc_id
}

output "instance_ip" {
  value = module.ec2.public_ip
}
```

---

## 📸 Preview

![Architecture](https://raw.githubusercontent.com/yourusername/yourrepo/main/infra-architecture.png)

*(Optional diagram showing EC2, VPC, S3, Internet Gateway, etc.)*

---

## 👨‍💻 Author

**Hannan**
DevOps & Frontend Developer
[LinkedIn Profile]([https://linkedin.com/in/your-profile](https://www.linkedin.com/in/hannanahmed100/))

---

## 📜 License

MIT License - free to use with attribution.

```


```
