pipeline {
  agent none
  stages {
    stage('Build') {
      agent {
        docker {
          image 'maven:3.9-eclipse-temurin-21-alpine'
          args '-v $HOME/.m2:/root/.m2'
        }

      }
      steps {
        echo 'Compiling sysfoo app...'
        sh 'mvn compile'
      }
    }

    stage('Test') {
      agent {
        docker {
          image 'maven:3.9-eclipse-temurin-21-alpine'
          args '-v $HOME/.m2:/root/.m2'
        }

      }
      steps {
        echo 'Running unit tests....'
        sh 'mvn clean test'
      }
    }

    stage('Package') {
      agent {
        docker {
          image 'maven:3.9-eclipse-temurin-21-alpine'
          args '-v $HOME/.m2:/root/.m2'
        }

      }
      steps {
        echo 'Packaging the application....'
        sh 'mvn package -DskipTests'
        sh '''# Truncate the GIT_COMMIT to the first 7 characters
GIT_SHORT_COMMIT=$(echo $GIT_COMMIT | cut -c 1-7)

# Set the version using Maven
mvn versions:set -DnewVersion="$GIT_SHORT_COMMIT"
mvn versions:commit'''
        archiveArtifacts '**/target/*.jar'
      }
    }

  }
  tools {
    maven 'Maven 3.9.11'
  }
  post {
    always {
      echo 'Pipeline is completed!'
    }

  }
}
