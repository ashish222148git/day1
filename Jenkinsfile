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

        stage('Terraform') {
            steps {
                script {
                    def envName = params.ENVIRONMENT

                    echo "Selected Environment: ${envName}"

                    sh '''
                        terraform version
                        terraform init
                        terraform apply -auto-approve
                    '''
                }
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
