pipeline { 
agent any
    stages { 
        stage ('Build docker') {
            steps {
                echo 'Finished cloning git repo'
            }
        }
        stage ('Testing docker container') {
            steps {
                echo 'testing file'
                sh "pip3 install -r requirements.txt"
                sh 'python3 -m pytest test.py'
            }

        }
        stage ('Deploy new docker') {
            steps{
                sh 'docker image build -t flask_docker .  '
                echo 'Deployed'
            }
        }
 
    }           
 }