pipeline {
    agent { label 'Devops' }

    environment {
        PROJECT = 'expense'
        COMPONENT = 'backend'
        DEPLOY_TO = "production"
    }

    options {
        disableConcurrentBuilds()
        timeout(time: 10, unit: 'SECONDS')
    }

    parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    }

    stages {
        stage('Build') {
            steps {
                sh """
                echo "hello this is build"
                echo "project: $PROJECT"
                echo "Hello ${params.PERSON}"
                echo "Biography: ${params.BIOGRAPHY}"
                echo "Toggle: ${params.TOGGLE}"
                echo "Choice: ${params.CHOICE}"
                echo "Password: ${params.PASSWORD}"
                """
            }
        }

        stage('Unit Test') {
            steps {
                sh "echo 'Hello this is unit test'"
            }
        }

        stage('Integration Test') {
            steps {
                sh "echo 'Hello this is integration test'"
            }
        }

        stage('Deploy') {
            when {
                environment name: 'DEPLOY_TO', value: 'production'
            }
            steps {
                sh "echo 'Hello this is Deploy'"
            }
        }

        stage('Parallel Stages') {
            parallel {
                stage('STAGE-1') {
                    steps {
                        sh "echo 'Hello this is parallel stage-1'; sleep 15"
                    }
                }
                stage('STAGE-2') {
                    steps {
                        sh "echo 'Hello this is parallel stage-2'"
                    }
                }
                stage('STAGE-3') {
                    steps {
                        sh "echo 'Hello this is parallel stage-3'"
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'I will always say hello'
        }
        failure {
            echo 'I will run when pipeline fails'
        }
        success {
            echo 'I will run when pipeline succeeds'
        }
    }
}
