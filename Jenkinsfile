pipeline {
    agent{label 'Devops' }
    enviorment {
        project = 'expense'
        component = 'backend'
    }
    options {
        disableConcurrentBuilds()
        timeout(time: 10, unit: 'SEC')
    }
    parameters{
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')

        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')

        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')

        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')

        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')

    }
    stages{
        stage('Build') {
            steps {
                script{
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
        }
        stage('Test') {
            steps {
                script{
                    sh """
                     echo "Hello this is test"
                    """ 
                }
            }
        }
        stage ('Deploy') {
            steps {
                script {
                    when {
                        enviorment name: 'DEPLOY_TO', value:'Production'
                    }
                    steps {
                        sh """
                        echo "Hello this is Deploy"
                        """
                    }
                }
            }
        }
    }
    post {
        always {
            echo 'I will always says hello'
    }
    failure {
        echo 'I will run when pipeline is failed'
    }
    success {
        echo 'I will run pipeline is success'
    }
    }
     
}