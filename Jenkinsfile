pipeline {
  environment {
        DOCKERHUB_CREDENTIALS=credentials('haleema-dockerhub')
    }
  agent none
  stages {
    stage('On-Edge2-Run') {
          agent any
          steps {
           // sh 'echo "edge2"'
            //sh 'imagename='haleema/docker-edge1:latest''
            //sh 'docker stop $(docker ps | awk -v image=$imagename '$2 == image {print $1}')'
            sh 'docker stop  e44668a36d06'
           //sh 'docker stop  haleema/docker-edge1; docker rm  haleema/docker-edge1'
            //sh 'echo "login to dockerhub" '
            //sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
          }
    }
    //stage('Login to Dockerhub') {
     // agent any
       //   steps {
         //   sh 'echo "login to dockerhub" '
           // sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
          //}
        //}
       
stage('Run b/w  Edge2 & cloud') {
      parallel {
    
    stage('On-Edge2-Run') {
          agent any
          steps {
            sh 'echo "edge2"'
            git branch: 'main', url: 'https://github.com/HaleemaEssa/jenkins-edge2.git'
            //sh 'docker stop  a56987f86712; docker rm  a56987f86712'
            sh 'docker build -t haleema/docker-edge2:latest .'
            sh 'docker run -v "${PWD}:/data" -t haleema/docker-edge2'
          }
    }
    stage('On-Cloud-Run') {
      agent {label 'aws'}
          steps {
            sh 'echo "cloud" '
            git branch: 'main', url: 'https://github.com/HaleemaEssa/jenkins-cloud.git'
           // sh 'docker build -t haleema/docker-cloud:latest .'
            sh 'docker run -v "${PWD}:/data" -t haleema/docker-cloud'
          }
    }
      }
    }

    
  }
}
