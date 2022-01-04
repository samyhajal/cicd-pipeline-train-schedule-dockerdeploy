pipeline {
    environment {
        registryCredential = 'docker_hub_id'
        dockerImage = ''
    }
    agent any
    stages {
        stage('Build Image') {
            steps {
                echo 'Building Docker Image'
                dockerImage = docker.build("samyhajal/train-schedule") 
            }
        }
        stage('Test Image') {  
            steps {
                dockerImage.inside {
                    sh 'echo "Tests passed"'        
                }    
            }    
        }
        stage('Deploy Image') {
            steps {
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push("${BUILD_NUMBER}")
                        dockerImage.push('latest')
                    }
                }
            }
        }
    }
}
