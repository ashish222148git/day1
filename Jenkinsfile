pipeline {
    agent {
        label 'dev'
    }

    parameters {
        choice(
            name: 'ENVIRONMENT',
            choices: ['sit', 'ppte', 'prod'],
            description: 'Select the environment'
        )
    }

    stages {

        stage('Terraform Init') {
            steps {
                script {
                    def envName = params.ENVIRONMENT

                    echo "Selected Environment: ${envName}"

                    sh '''
                        terraform version
                        terraform init
                    '''
                }
            }
        }

        stage('Terraform Plan') {
            steps {
                sh '''
                    terraform plan
                '''
            }
        }

        stage('Approval') {
            steps {
                input(
                    message: "Do you want to apply Terraform changes for ${params.ENVIRONMENT}?",
                    ok: 'Apply'
                )
            }
        }

        stage('Terraform Apply') {
            steps {
                sh '''
                    terraform apply -auto-approve
                '''
            }
        }

        stage('Output') {
            steps {
                sh '''
                    terraform output
                '''
            }
        }
    }
}
