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
                git 'https://github.com/ecarmona1992/flask-jenkins'
                echo 'Finshed downloading git'
                sh "docker stop project1"
                // force stop docker and clean up images
                sh "docker system prune -af"
            }
        }
        stage('testing') {
            steps {
                sh "python3 test.py"
            }
        }

        stage('Build Image') {
            steps {
                script {
                    // img = registry + ":${env.BUILD_ID}"
                    img = registry + ":${env.BUILD_ID}"
                    dockerImage = docker.build("${img}")
                }
            }
        }

        stage('Run Docker') {
           steps {
                // Run venv
                echo 'Running test'
                // sh "docker run -d -p 5000:5000 ${img}"
                sh "docker run -d --name project1 -p 5000:5000 ${img}"
                sh "curl localhost:5000"
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

    post {
        always {
            emailext body: 'A Test EMail', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: 'Test'
        }
    }
}