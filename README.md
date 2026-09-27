# EC2 User Data Automation

## Project Overview

This project demonstrates how Amazon EC2 User Data can automate server configuration during instance launch.

The EC2 instance was configured to automatically update Amazon Linux, install Apache, start and enable the web server, and deploy a custom webpage without requiring manual post-launch configuration.

This project demonstrates cloud automation, repeatable provisioning, Linux administration, and infrastructure initialization concepts.

## Architecture

![Architecture Diagram](architecture/08-architecture-diagram.png)

### Architecture Flow

Administrator → EC2 Instance → User Data Script → Apache Web Server

The EC2 instance executes the User Data script during launch using cloud-init. The script installs and configures Apache automatically and creates the webpage.

## AWS Services and Technologies Used

- Amazon EC2
- EC2 User Data
- Amazon Linux 2023
- Apache HTTP Server
- cloud-init
- Bash
- SSH

## Automation Script

```bash
#!/bin/bash
dnf update -y
dnf install -y httpd

systemctl start httpd
systemctl enable httpd

cat <<'EOF' > /var/www/html/index.html
<!DOCTYPE html>
<html>
<head>
    <title>EC2 User Data Automation</title>
</head>
<body>
    <h1>EC2 User Data Automation Successful!</h1>
    <p>This Apache web server was automatically configured at launch using EC2 User Data.</p>
</body>
</html>
EOF
