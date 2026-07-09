pipeline {
    agent any

    tools {
        terraform 'terraform'
    }
    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
    }

    stages {

        stage('Git Clone') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/ashrafff452/aws-terraform.git'
            }
        }

       stage('Terraform Init') {
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws_credentials'
                ]]) {

                    sh 'terraform init'
                }
            }
        }

        stage('Terraform Plan') {
            steps {
                sh 'terraform plan'
            }
        }

        stage('Terraform Apply') {
            steps {
                sh 'terraform apply -auto-approve'
            }
        }
    }

    post {
        success {
            echo 'Terraform deployment successful'
        }

        failure {
            echo 'Terraform deployment failed'
        }
    }
}
