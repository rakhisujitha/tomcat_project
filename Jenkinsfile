
pipeline {
    agent any
    tools{
        maven "Maven_Home"
    }
    parameters {
       choice choices: ['Mumbai', 'Virginia', 'Ohio'], description: 'Choose the your Region', name: 'region'
    }

    stages {
        stage('git clone') {
            steps {
               git branch: 'main', url: 'https://github.com/rakhisujitha/tomcat_project.git'
            }
        }
        stage('Build'){
            steps {
                script {
                   if (params.region == 'Ohio') {
                       sh 'mvn clean install'
                    } else if (params.region == 'Mumbai') {
                         sh 'mvn clean install'
                    } else if (params.region == 'Virginia') {
                         sh 'mvn clean install'
                    }
                }
            }
        }
        stage('Test'){
            steps {
                sh 'mvn test'
            }
        }
    }
    post{
        success{
            echo 'Build and test successful! Deploying...'
            script{
                sh 'sudo scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/pipeline/webapp/target/webapp.war root@10.0.3.86:/var/lib/tomcat9/webapps'
            }
        }
        failure{
            echo 'Build or test failed. Deployment aborted.'
        }
    }
}
