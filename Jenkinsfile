pipeline {
    agent any 
    environment {
        dockerImage = ''
        registry = "anishmoktan/jenkins_25_dh"
        // registry = "test123"

        // //- update your credentials ID after creating credentials for connecting to Docker Hub
        registryCredential = 'dockerhub_id'
        
    }
    
    stages {
        stage('Cloning Git') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '', url: 'https://github.com/anishmoktan/jenkins_25']]])       
            }
        }
    
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
    
    //  // Stopping Docker containers for cleaner Docker run
    //  stage('docker stop container') {
    //      steps {
    //         sh 'docker ps -f name=mypythonappContainer -q | xargs --no-run-if-empty docker container stop'
    //         sh 'docker container ls -a -fname=mypythonappContainer -q | xargs -r docker container rm'
    //      }
    //   }
    
    
    // // Running Docker container, make sure port 8096 is opened in 
    // stage('Docker Run') {
    //  steps{
    //      script {
    //         dockerImage.run("-p 8096:5000 --rm --name mypythonappContainer")
//     //      }
//       }
//     }
   }
}