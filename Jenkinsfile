pipeline {
    agent any
    tools {
        maven 'Maven3'  // Ensure Maven is installed
        jdk 'JDK21'     // Ensure JDK is installed
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/eetuam1/DiceRoll.git'  // Update the URL to your repository
            }
        }
        stage('Build') {
            steps {
                bat 'mvn clean package'  // Use 'sh' instead of 'bat' if on a Unix/Linux system
            }
        }
        stage('Run Unit Tests') {
            steps {
                bat 'mvn test'  // Use 'sh' instead of 'bat' if on a Unix/Linux system
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'  // Capture test reports
                }
            }
        }
        stage('Code Coverage Report') {
            steps {
                bat 'mvn jacoco:report'  // Use 'sh' instead of 'bat' if on a Unix/Linux system
            }
            post {
                always {
                    jacoco execPattern: 'target/jacoco.exec'  // Capture JaCoCo coverage
                }
            }
        }
    }
}
