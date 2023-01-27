pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                git url: 'https://github.com/Nerack15/micro.git'
            }
        }
        stage('Build') {
          when {
                branch '*'
            }
            steps {
                sh 'cd rest'
                sh './gradlew clean build'
            }
        }
    }
}
