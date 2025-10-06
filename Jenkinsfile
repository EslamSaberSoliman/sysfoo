pipeline {
    agent any
    tools {
      maven: 'Maven 3.9.11'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Compiling sysfoo app...'
                sh 'mvn compile'
            }
        }
        stage('Test') {
            steps {
                echo 'Running unit tests....'
                sh 'mvn clean test'
            }
        }
        stage('Package') {
            steps {
                echo 'Packaging the application....'
                sh 'mvn package -DskipTests' 
            }
        }
    }
    post{
        always{
            echo "Pipeline is completed!"
        }
    }
}
