
---

# build-steps.md

```markdown
# Build Steps - EC2 Web Server + IAM Role + CloudWatch Monitoring

## Goal
Deploy an EC2 web server, attach an IAM role, configure CloudWatch monitoring, and send SNS alerts for CPU and disk usage.

---

## Step 1 - Launch EC2 Instance
1. Opened the EC2 console
2. Clicked Launch Instance
3. Entered the instance name: `ec2-iam-cloudwatch-lab`
4. Selected an Amazon Linux AMI
5. Chose a micro instance type
6. Selected or created a key pair
7. Configured networking:
   - Enabled public IP
   - Allowed SSH from my IP
   - Allowed HTTP from Anywhere
8. Launched the instance
9. Waited for the instance to reach `Running` and pass status checks

---

## Step 2 - Install Apache Web Server
Connected to the EC2 instance and ran:

```bash
sudo dnf update -y
sudo dnf install -y httpd
sudo systemctl enable httpd
sudo systemctl start httpd
echo "<h1>EC2 Web Server + IAM Role + CloudWatch Lab</h1>" | sudo tee /var/www/html/index.html