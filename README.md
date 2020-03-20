# Ansible-aws-challenge
This repository contains an ansible deployment for the following architecture
![arch](img/architecture.png)

# Requirements 
- Ansible >= 2.9
- Python >= 3.0.0
- boto-core
- boto3
- openshift >= 0.6

# Assumptions
- AWS credentials must be configured in the environment.
- ECR is configured and contains an image of the application

# Execution
- Go to repo root directory

`$ cd ansible-aws-challenge`

- Execute main playbook

`$ ansible-playbook site.yml`

# TO-DOs
- Jenkins CI/CD is ready but configured manually.

Manual configuration include: 

For Jenkins: 

- Install Github plugin
- Install AWS-CLI plugin
- Configure credentilas for AWS CLI (this could use role-based auth)
- Create CI/CD pipeline with: 
   - Trigger besed on Github repository: 
   - Configure the following pipeline:
    ```
    node {

        stage('Clone repository'){
            git branch: "master", url: "https://<url_project>"
        }
        
        stage('Image build'){
        docker.build('<account_id>.dkr.ecr.<aws_region>.amazonaws.com/<repo_name>')
        }

        stage('Push image'){
            docker.withRegistry('https://<account_id>.dkr.ecr.<region>.amazonaws.com', 'ecr:<<region>:<id_credentisas_jenins>') {
                docker.image('<accunt_id>.dkr.ecr.<region>.amazonaws.com/<repo_name>').push('latest')
            }
        }
        
        stage('Deploy image to cluster'){
        sh "kubectl set image deployment/hello-deployment hello=hello:latest --record --kubeconfig=$JENKINS_HOME/.kube/config.json " 
        }
    
    }
    ```
      
   - Configure repository hook on Github.

On the Jenkins instance:
- Install docker on the instance
- Configure docker for jenkins user
- Install packeges: botocore , boto3
- Copy generated kubectl configuration file to $JENKINS_HOME/.kub/config.json on the instance
  (improvement: create profile for jenkins in kubernetes auth)


