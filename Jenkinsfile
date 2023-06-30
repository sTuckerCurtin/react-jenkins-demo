pipeline {
    agent any
    stages{

        stage('Build') {
            steps {
                script{
                    def nodejsTool = tool name: 'node-20-tool', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
                    env.PATH = "${nodejsTool}/bin:${env.PATH}"
                }
                sh '''
                echo "Building the application..."
                npm install
                npm run-script build
                '''
            }
        }

        stage('Docker'){
            steps{
                script{
                    def dockerTool = tool name: 'docker-latest-tool', type: 'org.jenkinsci.plugins.docker.commons.tools.DockerTool'
                    env.PATH = "${dockerTool}/bin:${env.PATH}"
                }
                sh 'echo "Dockerizing the application.."'
                sh 'docker --version'
                sh 'docker images'
            }
        }
    }
}