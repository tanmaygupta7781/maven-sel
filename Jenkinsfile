pipeline {
    agent any  // Use any available agent

    tools {
        maven 'Maven'
        gradle 'Gradle'  // Ensure this matches the name configured in Jenkins
        jdk 'JDK'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/tanmaygupta7781/maven-sel.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'  // Run Maven build
            }
        }

       stage('Test') {
           steps {
               sh 'mvn compile'  // Run unit tests
           }
        }

              
        stage('Run Application') {
            steps {
                // Start the JAR application
                sh 'mvn run'
            }
        }

        
    }

    post {
        success {
            echo 'Build and deployment successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
