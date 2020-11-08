pipeline {
    agent any
     tools {
    maven 'maven'
  }
   triggers {
        pollSCM '* * * * *'
    }
      environment {
        registryCredential = 'nexus-user-credentials'
        registry = "http://172.17.0.4:8081" /*be sure to include trailing slash*/
        docker_img =  ''

    }
}
    stages {
          stage('Checkout') {
      checkout scm
    }

                stage ('Build Application') {
            steps {
                sh 'mvn -Dmaven.test.failure.ignore=true install' 
            }
            post {
                success {
                    junit 'target/reports/**/*.xml' 
                }
            }
        }

        stage ('build') {
            steps {
                dir('Toy0Store'){
                sh "mvn clean install"
                
                }
            }
        }
        stage ('build docker') {
            steps {
                dir('Toy0Store'){
                sh "docker build -t testimg ."
      
                }
                
            }
        }
        stage ('push') {
            steps {
                 sh 'docker login -u user -p password registry'
                 sh 'docker push NexusDockerRegistryUrl/Imagename}'
                 sh 'docker logout NexusDockerRegistryUrl'
                    }
         
            }
        }
    }
}