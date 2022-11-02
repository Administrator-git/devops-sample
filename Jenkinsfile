pipeline {
    agent { 
      docker { image 'paramesh321/jenkins-slave:v2' { label 'docker-slave1' } } }
    stages {
        stage('test') {
            steps {
                sh 'mvn --version'
            }
        }
    }
}
