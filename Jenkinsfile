pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
    }

    stages {
        stage('Checkout Repository') {
            steps {
                script {
                    try {
                        checkout([$class: 'GitSCM', 
                                  branches: [[name: '*/main']], 
                                  userRemoteConfigs: [[url: 'https://github.com/Sajith46/terraform-aws-vpc.git']]
                        ])
                    } catch (Exception e) {
                        error "Git Checkout Failed: ${e.message}"
                    }
                }
            }
        }

        stage('Setup AWS Credentials') {
            steps {
                withCredentials([string(credentialsId: 'AWS_ACCESS_KEY_ID', variable: 'AWS_ACCESS_KEY_ID'),
                                 string(credentialsId: 'AWS_SECRET_ACCESS_KEY', variable: 'AWS_SECRET_ACCESS_KEY')]) {
                    script {
                        sh 'echo AWS credentials configured'
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
                script {
                    try {
                        sh 'terraform plan -out=tfplan'
                    } catch (Exception e) {
                        error "Terraform Plan Failed: ${e.message}"
                    }
                }
            }
        }

        stage('Apply Infrastructure') {
            steps {
                script {
                    try {
                        sh 'terraform apply -auto-approve tfplan'
                    } catch (Exception e) {
                        error "Terraform Apply Failed: ${e.message}"
                    }
                }
            }
        }
    }
}
