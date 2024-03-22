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
                bat 'mvn -f hello-app/pom.xml -B -DskipTests clean package'
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
                bat 'mvn -f hello-app/pom.xml findbugs:findbugs'
            }
        }
        stage('Static Code Analysis - PMD') {
            steps {
                // Run PMD analysis
                bat 'mvn -f hello-app/pom.xml pmd:pmd'
            }
        }
        stage('Test') {
            steps {
                // Run tests
                bat 'mvn -f hello-app/pom.xml test'
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
