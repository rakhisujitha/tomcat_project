pipeline {
    agent any

    stages {
        stage('clone from github') {
            steps {
                git branch: 'main', url: 'https://github.com/mohammedashiqu/jenkins_tomcat_jacoco_project.git'
            }
        }
        stage('build war file') {
            steps {
                sh "mvn clean install package"
            }
        }
        stage('jacoco test') {
            steps {
                jacoco()
            }
        }
        stage('deploy to tomcat') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcat-server', path: '', url: 'http://65.0.205.121:8080')], contextPath: 'webapp', war: '**/*.war'
            }
        }
    }
}
