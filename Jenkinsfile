pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') {
         when {
                branch '*'
            }
            steps {
                  sh 'build'
            }
        }
}
}
