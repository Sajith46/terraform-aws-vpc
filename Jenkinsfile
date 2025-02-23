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
        stage('Initialize Terraform') {
            steps {
                sh '''
                terraform init
                '''
            }
        }
        stage('Plan Infrastructure') {
            steps {
                sh '''
                terraform plan -out=tfplan
                '''
            }
        }
        stage('Apply Infrastructure') {
            steps {
                sh '''
                terraform apply -auto-approve
                '''
            }
        }
    }
}

