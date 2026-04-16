pipeline {
    agent any

    parameters {
        choice(
            name: 'ACTION',
            choices: ['plan', 'apply', 'destroy'],
            description: 'Select Terraform action'
        )
        choice(
            name: 'ENV',
            choices: ['dev', 'stage', 'prod'],
            description: 'Select Environment'
        )
        string(
            name: 'BRANCH',
            defaultValue: 'master',
            description: 'Enter branch name (e.g. master, feature/vpc)'
        )
    }

    environment {
        AWS_DEFAULT_REGION = 'ap-south-1'
    }

    stages {

        stage('Checkout') {
            steps {
                script {
                    echo "Building from branch: ${params.BRANCH}"
                    git branch: "${params.BRANCH}",
                        url: 'https://github.com/pratikzende882002-hash/Terraform-all-repo.git'
                }
            }
        }

        stage('Terraform Init') {
            steps {
                dir('terraform-root') {
                    sh 'terraform init'
                }
            }
        }

        stage('Terraform Action') {
            steps {
                dir('terraform-root') {
                    script {
                        if (params.ACTION == 'plan') {
                            sh "terraform plan -var-file=envs/${params.ENV}.tfvars"
                        }
                        else if (params.ACTION == 'apply') {
                            sh "terraform apply -auto-approve -var-file=envs/${params.ENV}.tfvars"
                        }
                        else if (params.ACTION == 'destroy') {
                            sh "terraform destroy -auto-approve -var-file=envs/${params.ENV}.tfvars"
                        }
                    }
                }
            }
        }
    }
}
