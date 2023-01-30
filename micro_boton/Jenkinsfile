pipeline {
    agent any
        stage('Build') {
          when {
                branch '*'
            }
            steps {
                sh './gradlew build'
            }
        }
    }
}
