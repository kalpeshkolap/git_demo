pipeline {
    agent any

    stages {
        stage('git checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/kalpeshkolap/git_demo.git']]])
            }
        }
        stage('building jar') {
            agent { docker 'maven:3.8.1-adoptopenjdk-11' }
            steps {
                sh '''
                cd sample
                mvn clean install'''
            }
        }
        stage('deploying') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://35.90.170.52:8080/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
