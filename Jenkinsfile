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
        stage('Clean Previous Chrome Sessions') {
            steps {
                sh '''
                    echo "Cleaning up old Chrome sessions..."
                    pkill chrome || true
                    pkill chromedriver || true
                    rm -rf /tmp/profile_* || true
                '''
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'  // Run Maven build
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
                sh 'java -jar target/maven-selapp-1.0-SNAPSHOT.jar'
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
