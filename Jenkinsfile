pipeline {
    agent { label 'docker-slave1' }
    parameters {
        string(name: 'Hello', defaultvalue: 'World', description: 'prints universal message')
    }
    stages {
        stage('test') {
            steps {
                sh('echo ${STATEMENT}')
            }
        }
    }
}
