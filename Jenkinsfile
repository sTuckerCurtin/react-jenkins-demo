pipeline {
    agent any

    environment{
        def nodejsTool = tool name: 'node-20-tool', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
        def dockerTool = tool name: 'docker-latest-tool', type: 'org.jenkinsci.plugins.docker.commons.tools.DockerTool'
        PATH = "${nodejsTool}/bin:${dockerTool}/bin:${env.PATH}"
    }  

    stages{
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Create Production Build') {
            steps {
              
                sh 'npm run-script build'
                
            }
        }
        stage('Build Docker Image '){
            steps{
                sh '''
                    docker build -t tucker245/react-jenkins-docker:latest .
                    docker images
                '''
        
            }
        }


        stage('Push Docker Image'){
            steps{
                 withCredentials([usernamePassword(credentialsId: 'personal-docker-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]){
                  sh "echo \$DOCKER_USERNAME"
                }
                 sh 'docker --version'
                echo 'Building image and pushing to Docker Hub...'

                
            }
        }
        stage ('Deploy New Image '){
            steps {

            }
        }
    }
}