pipeline {
    agent any
    environment {
        AWS_REGION = "us-east-1"
    }
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Sajith46/terraform-aws-vpc.git'
            }
        }
        stage('Setup AWS Credentials') {
            steps {
                withCredentials([
                    string(credentialsId: 'aws-access-key', variable: 'AWS_ACCESS_KEY_ID'),
                    string(credentialsId: 'aws-secret-key', variable: 'AWS_SECRET_ACCESS_KEY')
                ]) {
                    sh 'echo "AWS credentials configured"'
                }
            }
        }
        stage('Initialize Terraform') {
            steps {
                sh 'terraform init'
            }
        }
        stage('Validate Terraform') {
            steps {
                sh 'terraform validate'
            }
        }
        stage('Plan Infrastructure') {
            steps {
                sh 'terraform plan -out=tfplan'
            }
        }
        stage('Apply Infrastructure') {
            steps {
                sh 'terraform apply -auto-approve tfplan'
            }
        }
    }
}
