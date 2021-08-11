pipeline {
    environment {
    registry = "kesav778/nodejs_hello"
    registryCredential = 'dockerhub'
    dockerImage = ''
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/kmohan778/Nodejs.git'
      }
    }
    
      stage("Build image") {
            steps {
                script {
                  dockerImage = docker.build registry + ":latest"
                }
            }
        }
    
      stage("Push image") {
            steps {
                script {
                    docker.withRegistry( '', registryCredential ) {
                    dockerImage.push()
                    }
                }
            }
        }

    
    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "hello.yaml", kubeconfigId: "k8s")
        }
      }
    }

  }

}
