pipeline {
    agent any

    parameters {
        choice(name: 'ENV', choices: ['QA', 'UAT'], description: 'Select the environment')
    }

    triggers {
        pollSCM '* * * * *'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh '/home/isha/Documents/DevOps_software/apache-maven-3.9.6/bin/mvn install'
            }
        }
        stage('Deployment') {
            steps {
                script {
                    if (env.ENV == 'QA') {
                        sh 'cp target/netflix4.war /home/isha/Documents/DevOps_software/apache-tomcat-9.0.88/webapps'
                        echo "Deployment has been COMPLETED on QA!"
                    } else if (env.ENV == 'UAT') {
                        sh 'cp target/netflix4.war /home/isha/Documents/DevOps_software/apache-tomcat-9.0.88/webapps'
                        echo "Deployment has been done on UAT!"
                    }
                }
         stage('Slack') {
             steps {
                 slackSend baseUrl: 'https://hooks.slack.com/services/', channel: 'devops-1', color: 'good', notifyCommitters: true, teamDomain: 'slack-devops'
        }
    }
}}}}

