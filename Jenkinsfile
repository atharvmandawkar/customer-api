pipeline {
    agent any

    parameters {
        choice(name: 'ENVIRONMENT', choices: ['dev', 'qa', 'prod'], description: 'Choose environment')
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out the source code'
                script {
                    env.APP_NAME = 'customer-api'
                    env.APP_VERSION = '1.0.0'
                    env.TARGET_ENV = params.ENVIRONMENT

                    echo "Application name: ${env.APP_NAME}"
                    echo "Environment: ${env.TARGET_ENV}"
                    echo "Version: ${env.APP_VERSION}"
                }
            }
        }

        stage('Build') {
            steps {
                echo "Building ${env.APP_NAME} version ${env.APP_VERSION}"
            }
        }

        stage('Test') {
            steps {
                echo 'Tests have started'
                script {
                    def envList = ['dev', 'qa', 'prod']
                    envList.each { item ->
                        echo "Processing environment: ${item}"
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    if (env.TARGET_ENV == 'dev') {
                        echo 'Development deployment started'
                    } else if (env.TARGET_ENV == 'qa') {
                        echo 'QA deployment started'
                    } else if (env.TARGET_ENV == 'prod') {
                        echo 'Production deployment requires approval'
                    } else {
                        error 'Wrong environment. Use dev, qa or prod.'
                    }
                }
            }
        }
    }
}
