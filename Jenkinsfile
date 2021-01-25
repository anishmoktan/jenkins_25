pipeline {
    agent any 
    environment {
        dockerImage = ''
        registry = "anishmoktan/jenkins_25_dh"
        // registry = "test123"

        // //- update your credentials ID after creating credentials for connecting to Docker Hub
        registryCredential = 'dockerhub_id'
        
    }
    
    // stages {
    //     stage('Cloning Git') {
    //         steps {
    //             checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '', url: 'https://github.com/anishmoktan/jenkins_25']]])       
    //         }
    //     }
    
    // Building Docker images
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry
        }
      }
    }
    
     // Uploading Docker images into Docker Hub
    stage('Uploading Image') {
     steps{    
         script {
            docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
            }
        }
      }
    }
    
}