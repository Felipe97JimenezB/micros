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
                  sh 'java -version'
                  sh './gradlew clean build'
            }
        }
        stage('Test-sonar'){
        when {
                branch 'main'
                branch 'desarrollo'
                branch 'qa'
            }
            steps {
                sh 'make check'
                junit 'reports/**/*.xml'
            }
        }
         stage('Test-veracode'){
        when {
                branch 'main'
                branch 'desarrollo'
                branch 'qa'
            }
            steps {
                sh 'make check'
                junit 'reports/**/*.xml'
            }
        }
        stage('Test-publicar'){
            steps {
                sh 'make check'
                junit 'reports/**/*.xml'
            }
        }
        stage('public-toDockerhub') {
        when {
                branch 'desarrollo'
            }
            steps {
        withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: jenkins_registry_cred_id, usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
              sh "docker login -e ${docker_email} -u ${env.USERNAME} -p ${env.PASSWORD} ${docker_registry_url}"
            }
            }
        }
       stage('Deploy-qa') {
        when {
                branch 'qa' 
            }
            steps {
                sh 'echo publish'
                sh 'kubeclt apply -f ingress/ingress.yaml'
            }
        } 
    }
}

