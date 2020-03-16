# Ansible-aws-challenge
This repository contains an ansible deployment for the following architecture
![arch](img/architecture.png)

# Requirements 
- Ansible >= 2.9
- Python >= 3.0.0
- boto-core
- boto3

# Assumptions
AWS credentias must be configured in the e

# Execution
Go to repo root directory
`$ cd ansible-aws-challenge`
execute main playbook
`$ ansible-playbook infra.yml`

# TO-DOs
- Deploy EKS with a toy web app
- Configure ALB connection with EKS
- Create and configure CI/CD process


