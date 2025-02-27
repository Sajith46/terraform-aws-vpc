pipeline {
    agent any
    
    environment {
        AWS_ACCESS_KEY_ID = credentials('aws-terraform')
        AWS_SECRET_ACCESS_KEY = credentials('aws-terraform')
    }
    
    stages {
        stage('Checkout Repository') {
            steps {
                git 'https://github.com/Sajith46/terraform-aws-vpc.git'
            }
        }
        
        stage('Setup AWS Credentials') {
            steps {
                script {
                    withCredentials([aws(credentialsId: 'aws-terraform', variable: 'AWS')]) {
                        sh 'echo "AWS credentials configured"'
                    }
                }
            }
        }

        stage('Check Terraform Installation') {
            steps {
                sh 'terraform version'
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
                input message: 'Apply changes?', ok: 'Apply'
                sh 'terraform apply tfplan'
            }
        }
    }
}
