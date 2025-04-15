 pipeline {
     agent any
    environment {
        TOMCAT_USER = 'admin'
        TOMCAT_PASS = 'admin'
        TOMCAT_URL = 'http://54.219.93.233:9090/manager/status'
    }

    tools {
        maven 'Maven' // Use your Maven name from Jenkins config
    }

    stages {
        stage('Clone Repo') {
            steps {
                git credentialsId: 'github-creds',
                    url: 'https://github.com/arulmurugan001/jenkinstest.git',
                    branch: 'main'
            }
        }

        stage('Build WAR') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy WAR to Tomcat') {
            steps {
                script {
                    def warFile = 'target/02-Maven-WebApp.war' // replace with your actual WAR file
                    sh """
                        curl -u $TOMCAT_USER:$TOMCAT_PASS -T $warFile "$TOMCAT_URL/deploy?path=/02-Maven-WebApp&update=true"
                    """
                }
            }
        }
    }
}