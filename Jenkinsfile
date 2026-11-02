
pipeline {
    agent {
        label 'build-node-1'
    }

    environment {
        PATH = "/opt/maven/bin:${env.PATH}"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Maven Version') {
            steps {
                sh 'java -version'
                sh 'mvn -version'
            }
        }

        stage('Compile') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Build WAR') {
            steps {
                sh 'mvn package'
            }
        }
stage('Deploy to Tomcat') {
    steps {
        sh 'cp target/myapp.war /opt/tomcat/webapps/myapp.war'
        echo 'WAR deployed to Tomcat successfully!'
    }
}
        stage('Archive WAR') {
            steps {
                archiveArtifacts artifacts: 'target/*.war',
                    fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed. Check Console Output.'
        }
    }
}

