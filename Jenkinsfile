pipeline {
  agent any
  tools {
     maven 'M2_HOME'
  }
  environment {
    registry = "wassiou10/mlop-pipeline"
    registryCredential = 'DockerImage'
}
  stages {
    stage('Build'){
      steps {
        sh 'mvn clean'
        sh 'mvn install'
        sh 'mvn package'
      }
    }
     stage('test'){
      steps {
       echo "test step"
        sh 'mvn test'
      }
    }
     stage('Building image'){
      steps {   
        script {
        dockerImage = docker.build registry + ":$BUILD_NUMBER"
      }
    }
   }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
  }
}
