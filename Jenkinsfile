def img
pipeline {
    // setting up dockhub information needed to push image.
    environment {
        registry = "ecarmona1992/project1"
        registrycredential = 'docker-hub-login'
        dockerimage = ''
    }
    agent any
    // first step is to download git file
    stages {
        stage('download') {
            steps {
                git 'https://github.com/ecarmona1992/SimpleFlaskUI.git'
                echo 'Finshed downloading git'
                // force stop docker and clean up images
                sh "docker system prune -af"
            }
        }

        stage('Test File') {
           steps {
                // Run venv
                sh "python3 -m venv .venv"
                // Run pip install
                sh "pip3 install -r requirements.txt"
                sh 'python3 -m pytest -x test.py'
          }
        }
        
        stage('Build Image') {
            steps {
                script {
                    img = registry + ":${env.BUILD_ID}"
                    println ("${img}")
                    dockerImage = docker.build("${img}")
                }
            }
        }

        stage('Push To DockerHub') {
            steps {
                script {
                    docker.withRegistry( 'https://registry.hub.docker.com ', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }

    }
}