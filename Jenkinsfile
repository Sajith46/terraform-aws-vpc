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
                    bat '''
                    set AWS_ACCESS_KEY_ID=%AWS_ACCESS_KEY_ID%
                    set AWS_SECRET_ACCESS_KEY=%AWS_SECRET_ACCESS_KEY%
                    echo AWS credentials configured
                    '''
                }
            }
        }
        stage('Check Terraform Installation') {
            steps {
                bat 'terraform version'
            }
        }
        stage('Initialize Terraform') {
            steps {
                bat 'terraform init'
            }
        }
        stage('Validate Terraform') {
            steps {
                bat 'terraform validate'
            }
        }
        stage('Plan Infrastructure') {
            steps {
                bat 'terraform plan -out=tfplan'
            }
        }
        stage('Apply Infrastructure') {
            steps {
                bat 'terraform apply -auto-approve'
            }
        }
    }
}
