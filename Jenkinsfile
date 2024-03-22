pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Checkout your code from Git
                git url: 'https://github.com/abdulsamadilyas82/my_app', branch: 'main'
            }
        }
        stage('Build') {
            steps {
                // Build your project (e.g., Maven build)
                bat 'mvn clean install'
            }
            post {
                success {
                    echo "Now Archiving the Artifacts....."
                    archiveArtifacts artifacts: '**/*.jar'
                }
            }
        }
        stage('Static Code Analysis - FindBugs') {
            steps {
                // Run FindBugs analysis
                bat 'mvn findbugs:findbugs'
            }
        }
        stage('Static Code Analysis - PMD') {
            steps {
                // Run PMD analysis
                bat 'mvn pmd:pmd'
            }
        }
        stage('Test') {
            steps {
                // Run tests
                bat 'mvn test'
            }
            post {
                always {
                    junit 'hello-app/target/surefire-reports/*.xml'
                }
            }
        }
        // Other stages...
    }
}
