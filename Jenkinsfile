pipeline {
agent any

stages {
stage('Clone Repo') {
            steps {
                git credentialsId: 'github-creds',
                    url: 'https://github.com/arulmurugan001/jenkinstest.git',
                    branch: 'main'
            }
        }

stage(‘Build’) {
steps {
sh ‘mvn clean package’
}
}

stage(‘Deploy’) {
environment {
TOMCAT_URL = ‘http://54.193.90.100:9090'
TOMCAT_USER = ‘admin’
TOMCAT_PASSWORD = ‘admin’
CONTEXT_PATH = ‘/myapp’
}

steps{
sh “curl — upload-file target/02-Maven-WebApp.war ${TOMCAT_URL}/manager/html/deploy?path=${CONTEXT_PATH} -u ${TOMCAT_USER}:${TOMCAT_PASSWORD}”
}
}
}
}
