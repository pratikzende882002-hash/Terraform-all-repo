pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/your-repo.git'
            }
        }

        stage('Terraform Init') {
            steps {
                dir('terraform-root') {
                    sh 'terraform init'
                }
            }
        }

        stage('Terraform Plan') {
            steps {
                dir('terraform-root') {
                    sh 'terraform plan -var-file=envs/dev.tfvars'
                }
            }
        }

        stage('Terraform Apply') {
            steps {
                dir('terraform-root') {
                    sh 'terraform apply -auto-approve -var-file=envs/dev.tfvars'
                }
            }
        }
    }
}
